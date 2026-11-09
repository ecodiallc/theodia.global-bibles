# Suggested Next Global Bibles to Add

Derived by cross-referencing:

- Supported languages in `/Volumes/MOVESPEED/dev2/TheodiaWeb` (one folder per
  locale: `ar bg bn cs da de el es fa fr he hi id it ja ko mr nl pa pl pt ro
  ru sv sw ta te th tl tr uk ur vi zh zh-Hant`).
- Bibles already packaged in this repo (`index.json` / `README.md`): `ar`,
  `de`, `es` (three), `pl`, `uk`.
- Public-domain / open-license source pool recorded in `notes/bible-sources.md`
  (Zefania XML on SourceForge: `projects/zefania-sharp/files/Bibles/`, plus
  `ph4.org/b4_mobi.php?q=zefania`).

Each candidate below is available as a Zefania XML download in the folder
indicated; the license/attribution status of any given translation must still be
verified before packaging (public-domain claims in Zefania are not always
audited). Prefer translations whose copyright has clearly lapsed or which carry
an open license, and record provenance in `Details.Information` + `README.md`
per `notes/dev-notes.md`.

Status legend: ⬜ to do · 🔄 in progress · ✅ done.

## Already covered (skip)

`ar`, `de`, `es`, `pl`, `uk`.

## High-priority candidates (language in web app, source available on Zefania)

| Status | Locale | Web language | Zefania folder | Candidate translation(s) |
| --- | --- | --- | --- | --- |
| ✅ | `cs` | Czech | `CZE/` | Czech BKR; Bible Kralická (1613) |
| ✅ | `da` | Danish | `DAN/` | Danish Version; Danish OT 1931 / NT 1907 (original orthography) |
| ✅ | `fr` | French | `FRE/` | French Louis Segond; French Darby; Bible de Genève 1669; Bible Ostervald 1877; Bible Martin; French Bible Bovet-Bonnet 1900 |
| ✅ | `it` | Italian | `ITA/` | Giovanni Diodati 1649 |
| ⬜ | `ja` | Japanese | `JPN/` | Japanese Kougou-Yaku 1954/55; Japanese Bungo 1953 |
| ✅ | `nl` | Dutch | `NL/` | Dutch Statenvertaling |
| ✅ | `pt` | Portuguese | `POR/` | Portuguese Corrigida Fiel (1753) |
| ✅ | `ro` | Romanian | `RUM/` | Cornilescu (1928); orthographically corrected Cornilescu |
| ✅ | `ru` | Russian | `RUS/` | Russian Synodal Translation |
| ✅ | `tl` | Tagalog | `TGL/` | Ang Dating Biblia |
| ⬜ | `vi` | Vietnamese | `VIE/` | Vietnamese Version |
## Medium priority candidates (language already covered in theodia.bibles or global-bibles)

These languages already have at least one Bible packaged in
`theodia.bibles` or this repo, so additional translations are useful but less
urgent than filling the gaps above.

| Status | Locale | Web language | Zefania folder | Candidate translation(s) |
| --- | --- | --- | --- | --- |
| ⬜ | `he` | Hebrew (OT) | `HEB/` | Westminster Leningrad Codex; Aleppo Codex; Open Scriptures Hebrew Bible (+ morphological); Miqra al pi ha-Mesorah; Biblia Hebraica; Delitzsch Hebrew NT (NT, Hebrew); Modern Hebrew Bible |
| ⬜ | `hi` | Hindi | `HIN/` | Hindi Indian Revised Version Bible |
| ⬜ | `zh` | Chinese (Simplified) | `CHI/` | Chinese Union Version — Simplified; New Chinese Version (Simplified) |
| ⬜ | `zh-Hant` | Chinese (Traditional) | `CHI/` | Chinese Union Version (traditional); (traditional NC V variant if present) |

## Low priority candidates (not sure of public-domain status)

Translations whose copyright status is unclear or which are almost certainly
still under copyright. Re-verify licensing (and obtain a grant where needed)
before packaging.

| Status | Locale | Web language | Zefania folder | Candidate translation(s) |
| --- | --- | --- | --- | --- |
| ⬜ | `bg` | Bulgarian | `BUL/` | Verens Contemporary Bible |
| ⬜ | `cs` | Czech | `CZE/` | Český studijní překlad; Czech Ekumenický překlad; Nova Bible Kralická (NKB); Preklad 21 |
| ⬜ | `fr` | French | `FRE/` | French Darby 2006; La Bible de Jérusalem; La Bible Augustin Crampon 1923; La Bible Machaira 2012; La Bible Pirot-Clamer |
| ⬜ | `it` | Italian | `ITA/` | Italian Version (Riveduta-ish); La Nuova Diodati 1991; Riveduta 1990; La Bibbia CEI '74 |
| ⬜ | `ko` | Korean | `KOR/` | Korean Revised Version 1952–1961; Korean Version |
| ⬜ | `mr` | Marathi | `MAR/` | Marathi Indian Revised Version Bible |
| ⬜ | `pt` | Portuguese | `POR/` | Portuguese Version |
| ⬜ | `ru` | Russian | `RUS/` | Russian Version; Russian NT with Strong's |
| ⬜ | `sv` | Swedish | `SWE/` | Svenska Folkbibeln (1998) |
| ⬜ | `ta` | Tamil | `TAM/` | Tamil (BSI); Tamil Bible (2024) |
| ⬜ | `th` | Thai | `THA/` | KJV-Thai (hybrid; verify it is actually a Thai translation and not an English gloss) |
| ⬜ | `tr` | Turkish | `TUR/` | Turkish; Southern Azeri Translation |
| ⬜ | `vi` | Vietnamese | `VIE/` | New Vietnamese Bible (2002) |
| ⬜ | `el` | Greek (Modern) | `GRE/` | Tischendorf Greek NT (19th-century critical text; copyright/licensing not verified) |

## No Zefania source currently listed (needs another provider)

These web-app languages have no matching folder in the Zefania index at the
time of writing. Suggest sourcing from an alternative (OTSeng corpus at
`/Volumes/external/otseng.bibles`, or a publisher grant):

| Status | Locale | Web language | Suggested fallback |
| --- | --- | --- | --- |
| ⬜ | `bn` | Bengali | Ph4 candidate: Bengali Bible: Easy-to-Read (World Bible Translation Center) — verify rights. |
| ⬜ | `fa` | Persian / Farsi | Ph4 candidates: Farsi Bible; Today's Persian Version (United Bible Societies) — verify rights. |
| ⬜ | `id` | Indonesian | Ph4 candidates: Bahasa Indonesia Sehari-hari (Wycliffe/IBS); Terjemahan Baru (LAI) — verify rights. |
| ⬜ | `pa` | Punjabi | Ph4 candidate: Punjabi New Testament Easy-to-Read (WBTC) — NT only; not a full canon |
| ⬜ | `te` | Telugu | Ph4: Telugu Bible; Telugu Bible Easy-to-Read (WBTC) — verify rights. |
| ⬜ | `ur` | Urdu | No ph4 candidate found; license required. |

## Licensing / packaging reminders

- Every candidate above is only a *candidate* until its license is verified.
  Prefer texts whose US copyright has lapsed (pre-1930 publications in
  practice) or which carry an explicit open license. Post-1929 translations
  (CEI '74, New Chinese Version, Riveduta '90, etc.) usually still carry
  copyright — do **not** package them without a written grant.
- Arabic (`ar`), German (`de`), Spanish (`es`), Polish (`pl`) and Ukrainian
  (`uk`) are already shipped; do not duplicate them unless a meaningfully
  different edition is being added (bump `version` and use a distinct
  `code`/`storageName`).
- Follow `notes/dev-notes.md` for the SQLite schema, validation counts
  (~31,102 verses / 1,189 chapters), `__MACOSX` stripping, and README /
  `index.json` updates. Keep IDs lowercase kebab-case and language folders
  aligned with BCP 47 tags.
