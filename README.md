# localization-override

Sumber JSON untuk fitur online localization — override translation copy tanpa perlu rebuild app. Repo ini dipakai lebih dari 1 app, dipisah per folder per app.

## Struktur

```
KantorKu/       # HRIS mobile app (Kantorku)
  localization_dev.json
  localization_staging.json
  localization_prod.json
Dealls/         # Dealls Jobs app (belum ada isinya, nanti ditambahkan)
  ...
```

Satu file per flavor per app, isi kedua locale sekaligus:

```json
{
  "en_US": { "someKey": "Some text", ... },
  "id_ID": { "someKey": "Beberapa teks", ... }
}
```

**Penting:** key locale di level atas HARUS pakai format underscore (`en_US`, `id_ID`) — bukan format hyphen yang dipakai di nama file sumber l10n app (`en-US_1.json`). Kalau salah pakai hyphen, override akan tersimpan di key yang tidak pernah dibaca app — kelihatan "jalan" tapi efeknya nol, tanpa error apa pun.

## Isi awal (`KantorKu/`)

Di-seed dari isi bundled JSON app HRIS (`resources/lib/l10n/json/en-US_*.json` + `id-ID_*.json`, digabung).

## Cara app fetch ini

App fetch `https://raw.githubusercontent.com/<owner>/<repo>/main/<AppFolder>/localization_<flavor>.json` lalu merge isinya di atas bundled translation (partial override, key yang tidak ada di sini tetap pakai bundled text).
