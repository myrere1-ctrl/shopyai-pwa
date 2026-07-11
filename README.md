# ShopyAI — Affiliate Content Engine

PWA (Progressive Web App) untuk generate konten affiliate Shopee dengan bantuan AI. 100% jalan di browser — tidak ada server backend, tidak ada API key bawaan. Setiap pengguna wajib memasukkan API key mereka sendiri lewat menu **Pengaturan** di dalam aplikasi.

## Cara Deploy (untuk pembeli)

### Opsi 1 — Pakai langsung via GitHub Pages ini
Buka: `https://<username>.github.io/<nama-repo>/`

### Opsi 2 — Deploy ke akun GitHub sendiri
1. Fork repo ini (atau download ZIP dan buat repo baru).
2. Buka **Settings → Pages** di repo Anda.
3. Pilih **Source: Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Tunggu 1–2 menit, situs akan aktif di `https://<username>.github.io/<nama-repo>/`.

### Opsi 3 — Hosting statis lain
Semua file di folder ini (`index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`) bisa langsung di-upload ke hosting statis apa pun (Netlify, Vercel, Cloudflare Pages, dll) — tidak perlu build step.

## Cara Setup API Key

Aplikasi tidak menyertakan API key apa pun. Buka menu **Pengaturan (⚙️)** di dalam aplikasi setelah dibuka, lalu isi:

1. **Anthropic API Key** (wajib, untuk generate teks/deskripsi produk)
   - Daftar di [console.anthropic.com](https://console.anthropic.com) → API Keys → Create Key
   - Format key: `sk-ant-api03-xxxxxxxx`
2. **Replicate API Key** (opsional, untuk generate gambar produk)
   - Daftar di [replicate.com](https://replicate.com/account/api-tokens)

Key disimpan **hanya di browser pengguna** (localStorage), tidak pernah dikirim ke server pihak ketiga selain langsung ke Anthropic/Replicate. Setiap install/browser perlu isi key sendiri-sendiri.

## Install sebagai App (PWA)

Karena sudah punya `manifest.json` + `sw.js`, situs ini bisa di-"Install" dari browser (Chrome/Edge: ikon install di address bar; Android: "Add to Home Screen"; iOS Safari: Share → "Add to Home Screen"). Setelah install, bisa dipakai offline untuk UI-nya (generate AI tetap butuh koneksi internet karena memanggil API langsung dari browser).

## Struktur File

```
pwa-deploy/
├── index.html      # Aplikasi utama (React bundle, single-file)
├── manifest.json    # PWA manifest
├── sw.js            # Service worker (cache static assets, network-first untuk HTML)
├── icon-192.png     # Icon PWA 192x192
└── icon-512.png     # Icon PWA 512x512
```

## Catatan Keamanan

- Tidak ada API key hardcoded di source code.
- Semua panggilan AI dilakukan langsung dari browser pengguna ke API resmi (Anthropic/Replicate) — pastikan pengguna memahami bahwa biaya penggunaan API ditanggung oleh pemilik key masing-masing.
