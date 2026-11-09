# Dev Notes — Creating `.bible.zip` Files

This document captures practical tips for producing a new Bible translation
package for the `ecodiallc/global-bibles` repository. The resulting files are
consumed by the Theodia app at `/Users/adam.ecodia/dev/TheodiaApp`.

## Package layout

A `.bible.zip` contains a single SQLite database whose filename matches the
zip's stem:

- `NTBT.bible.zip` → contains `NTBT.bible` (SQLite DB)
- `Biblia-Gdańska.bible.zip` → contains `Biblia-Gdańska.bible`

Naming convention for new files: use a human-readable title with hyphens instead
of spaces, e.g. `My-Bible.bible.zip`.

## Database schema

Create the database with exactly this schema (matches existing packages):

```sql
CREATE TABLE Details (
    Title NVARCHAR(100),
    Abbreviation NVARCHAR(50),
    Information TEXT,
    Version INT,
    OldTestament BOOL,
    NewTestament BOOL,
    Apocrypha BOOL,
    Strongs BOOL
);

CREATE TABLE Bible (Book INT, Chapter INT, Scripture TEXT);
CREATE TABLE Verses (Book INT, Chapter INT, Verse INT, Scripture TEXT);
CREATE TABLE Notes (Book INT, Chapter INT, Verse INT, ID TEXT, Note TEXT);

CREATE INDEX idx_bible_book_chapter ON Bible (Book, Chapter);
CREATE INDEX idx_verses_book_chapter ON Verses (Book, Chapter);
CREATE INDEX idx_verses_book_chapter_verse ON Verses (Book, Chapter, Verse);
```

- `Details` holds exactly one row.
- `Version`, `OldTestament`, etc. are stored as integers (`0`/`1`).
- Books are numbered `1` (Genesis) through `66` (Revelation), in order.
- `Bible` is chapter-level text (one row per chapter).
- `Verses` is verse-level text (one row per verse).
- `Notes` holds footnotes; may be empty.

## Verse text format

- Plain text for `Verses.Scripture` (no markup), e.g. `En el principio creó…`.
- The chapter-level `Bible.Scripture` is HTML: verse numbers wrapped as
  `<verse><vid id="v{book}.{chapter}.{verse}" onclick="luV({book})">{verse} </vid>…</verse>`,
  with section headings as `<h3>…</h3>`. Cross-reference ranges may appear as
  additional `<h3>` blocks. Match the formatting used by existing packages
  (inspect a known-good file such as `NTBT.bible.zip`) before generating.

## Strongs

Set `Strongs = 0` unless the translation ships Strong's numbers. When enabled,
verse text typically includes markup such as `<sup s="H1234">…</sup>`.

## Apocrypha

Set `Apocrypha = 0` for the standard 66-book canon. Only set it to `1` if the
translation genuinely includes deuterocanonical books; in that case the book
numbering scheme must be agreed with the app consumer first.

## Building a new package (step-by-step)

1. **Obtain source text.** Secure a legally usable source. Record provenance and
   attribution in `Details.Information` and in `README.md` (see NTBT entry for
   the required attribution style).
2. **Create the SQLite DB.**
   ```bash
   sqlite3 NewTitle.bible < schema.sql
   ```
3. **Populate `Details`.** One row:
   ```sql
   INSERT INTO Details VALUES ('Title','ABBR','Information text',1,1,1,0,0);
   ```
4. **Populate `Verses` and `Bible`.** Use a script (Python with `sqlite3` is
   typical) to insert chapters/verses. Validate counts:
   - Verses total should be ~31,102 for a full canon (minor variants ok).
   - `Bible` should have 1,189 chapter rows.
5. **Create indexes** (included in schema above).
6. **Verify integrity.**
   ```bash
   sqlite3 NewTitle.bible "PRAGMA integrity_check;"
   sqlite3 NewTitle.bible "SELECT count(*) FROM Verses; SELECT count(*) FROM Bible;"
   ```
7. **Zip it.** The zip filename and the DB filename must match:
   ```bash
   zip NewTitle.bible.zip NewTitle.bible
   ```
8. **Strip macOS metadata junk** (required before committing):
   ```bash
   zip -d NewTitle.bible.zip "__MACOSX/*"
   zip -d NewTitle.bible.zip "*/.DS_Store"
   ```
9. **Verify the zip contains only the `.bible` file.**
   ```bash
   unzip -l NewTitle.bible.zip
   ```

## Registering in the catalog

Update both catalog files so consumers discover the new package.

### README.md

Add a row to the ID/Name table (keep alphabetical order) and a bullet under
`## Sources`:

```markdown
| `mybible` | My Bible |
...
- `mybible`: My Bible — English translation.
```

### index.json

Append an entry to `packages`:

```json
{
  "id": "mybible",
  "type": "bible",
  "path": "My-Bible.bible.zip",
  "name": "My Bible",
  "description": "My Bible — English translation.",
  "code": "MYBIBLE",
  "locale": "en",
  "version": "1.0.0",
  "storageName": "MYBIBLE"
}
```

Conventions:

- `id` is lowercase kebab-case (used as the catalog key).
- `code` / `storageName` are uppercase identifiers used by the app for local storage; keep them unique and stable (changing them breaks installed users' data).
- `locale` is a BCP 47 language tag.
- `version` follows SemVer; bump it on any content change.

## Licensing / attribution

- Only package translations whose license permits redistribution. Record the
  source and any required attribution in `Details.Information` and README.
- For restricted texts (e.g. NTBT), include the publisher's exact attribution
  string and link. See the NTBT entry for the template.

## Common pitfalls

- **Mismatched filenames.** The DB basename must equal the zip basename, otherwise
  consumers can't locate it.
- **Forgotten `__MACOSX` cleanup.** CI/merge checks reject junk; always run
  `zip -d ... "__MACOSX/*"`.
- **Wrong book numbering.** Books must be `1..66`; off-by-one breaks chapter lookups.
- **Empty `Bible` table.** Some consumers render chapter HTML from `Bible`; if you
  only fill `Verses`, chapter views will be blank.
- **Integers stored as strings.** Keep `Version`, `OldTestament`, etc. as ints.
- **Not updating `index.json`.** The app reads `index.json` to discover packages;
  a missing entry means the Bible won't appear.
- **Changing `code`/`storageName` after release.** Breaks existing installs.
