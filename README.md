# localization-override

Sumber JSON untuk fitur online localization — override translation copy tanpa perlu rebuild app. Repo ini dipakai lebih dari 1 app, dipisah per folder per app.

## Struktur

```
KantorKu/       # HRIS mobile app (Kantorku)
  en-US_dev.json
  en-US_staging.json
  en-US_prod.json
  id-ID_dev.json
  id-ID_staging.json
  id-ID_prod.json
Dealls/         # Dealls Jobs app (belum ada isinya, nanti ditambahkan)
  ...
```

Satu file per locale per flavor — sengaja konsisten dengan struktur file source l10n bundled app-nya (`resources/lib/l10n/json/en-US_*.json`, `id-ID_*.json`): nama file pakai locale bentuk hyphen (`en-US`, `id-ID`), isinya **flat** (langsung translation key, tanpa wrapper locale):

```json
{
  "someKey": "Some text",
  "anotherKey": "Teks lainnya"
}
```

App fetch 2 file (satu per locale) tiap kali cek update, lalu digabung jadi 1 struktur internal — locale key yang dipakai di dalam app sendiri bentuknya underscore (`en_US`, `id_ID`), konversi itu ditangani di kode app, bukan di file ini.

## Isi awal (`KantorKu/`)

Di-seed dari isi bundled JSON app HRIS (`resources/lib/l10n/json/en-US_*.json` + `id-ID_*.json`, digabung per locale).

## Cara app fetch ini

App fetch `https://raw.githubusercontent.com/<owner>/<repo>/main/<AppFolder>/<locale>_<flavor>.json` (2x per cek, satu per locale) lalu merge isinya di atas bundled translation (partial override, key yang tidak ada di sini tetap pakai bundled text).
