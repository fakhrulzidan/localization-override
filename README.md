# localization-override

Sumber JSON untuk fitur online localization (Kantorku HRIS mobile app) — override translation copy tanpa perlu rebuild app.

## Format

Satu file per flavor, isi kedua locale sekaligus:

- `localization_dev.json`
- `localization_staging.json`
- `localization_prod.json`

Bentuknya:

```json
{
  "en_US": { "someKey": "Some text", ... },
  "id_ID": { "someKey": "Beberapa teks", ... }
}
```

**Penting:** key locale di level atas HARUS pakai format underscore (`en_US`, `id_ID`) — bukan format hyphen yang dipakai di nama file sumber l10n app (`en-US_1.json`). Kalau salah pakai hyphen, override akan tersimpan di key yang tidak pernah dibaca app — kelihatan "jalan" tapi efeknya nol, tanpa error apa pun.

## Isi awal

Di-seed dari isi bundled JSON app saat ini (`resources/lib/l10n/json/en-US_*.json` + `id-ID_*.json`, digabung). Isinya sama persis di ketiga file flavor untuk sekarang — silakan edit sesuai kebutuhan testing per environment.

## Cara app fetch ini

App fetch `https://raw.githubusercontent.com/<owner>/<repo>/main/localization_<flavor>.json` lalu merge isinya di atas bundled translation (partial override, key yang tidak ada di sini tetap pakai bundled text).
