# 📋 GEMINI-SPEC

> **Orkestrator Perencanaan & Penentuan Spesifikasi Tunggal untuk Google Antigravity**

[![Kompatibel Antigravity](https://img.shields.io/badge/Antigravity-Plugin-4285F4?style=flat-square&logo=google)](https://github.com/diinggos/gemini-spec)
[![Lisensi: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)

**`gemini-spec`** menyatukan seluruh alur perencanaan bawaan Antigravity (`/grill-me`, `/plan`, `research`, dan `bypass`) ke dalam satu pintu masuk cerdas yang dipicu lewat perintah **`/spec`**.

Alih-alih Anda harus bingung menebak kapan harus mengetik `/grill-me`, `/plan`, atau meriset dokumentasi secara manual, `/spec` secara otomatis mengevaluasi kelengkapan prompt Anda dan mengaktifkan alur bawaan Antigravity yang paling tepat—**selalu berhenti untuk Anda baca dan tinjau sebelum ada satu pun kode yang dieksekusi**.

---

## 🏛 Gambaran Arsitektur

```
                                  [Prompt Pengguna Diterima]
                                             │
                                             ▼
                                     [Mode Auto /spec]
                             (HANYA MEMILIH JALUR PERSIAPAN)
                                             │
            ┌───────────────────┬────────────┴────────────┬───────────────────┐
            ▼                   ▼                         ▼                   ▼
        [bypass]           [grill-me]                  [plan]             [research]
      Tugas sepele,       Kebutuhan ambigu,        Spesifikasi detail,  Library/API baru,
      tanpa planning      wawancara pohon          langsung buatkan     kumpulkan fakta
                          keputusan (/grill-me)    blueprint (/plan)    sumber primer
            │                   │                         │                   │
            │                   └────────────┬────────────┘                   │
            │                                │                                │
            │                                ▼                                ▼
            │                     [DOKUMEN BLUEPRINT PLAN]           [HASIL RISET TEKNIS]
            │                                │                                │
            ▼                                └────────────────┬───────────────┘
     Langsung siap                                            ▼
       eksekusi                                        ⛔ SELALU BERHENTI ⛔
                                                  GERBANG REVIEW WAJIB OLEH MANUSIA
                                              (Nol eksekusi kode otomatis!)
```

---

## ⚡ 4 Mode Perencanaan Native

| Mode | Sinyal Pemicu | Alur Native Antigravity yang Dipanggil | Output (Wajib Dibaca) |
| :--- | :--- | :--- | :--- |
| **`bypass`** | Tugas mikro ($\le 2$ file, typo, ubah config lokal, pertanyaan Q&A). | Melewati tahap perencanaan; langsung siap dieksekusi. | Tidak ada dokumen (Respon instan). |
| **`grill-me`** | Fitur baru atau kompleks dengan **kebutuhan masih abstrak / ambigu** (banyak cabang arsitektur terbuka). | Memicu protokol bawaan **`/grill-me`** (`ask_question` berbasis *Design Tree Frontier*) sampai seluruh cabang tuntas $\rightarrow$ otomatis menyusun blueprint plan. | Pertanyaan interaktif & dokumen rencana final. |
| **`plan`** | Tugas kompleks di mana **spesifikasi teknis sudah lengkap sejak awal** (schema, endpoint, dan library sudah disebut user). | Melewati wawancara. Langsung memicu bawaan **`/plan`** untuk menyusun roadmap implementasi bertahap dengan checklist `[ ]`. | Dokumen artefak rencana kerja bertahap. |
| **`research`** | Tugas yang melibatkan **library baru, API pihak ketiga yang belum dikenal, atau perubahan breaking changes** yang belum ada di repo. | Memicu skill bawaan **`research`** untuk mengumpulkan fakta resmi ke dokumen markdown sebelum planning dimulai. | Dokumen ringkasan hasil riset teknis. |

---

## 🛡️ Gerbang Peninjauan Wajib (Anti-Eksekusi Otomatis)

> [!IMPORTANT]
> **Mode `auto` pada `/spec` HANYA bertugas menentukan jalur perencanaan mana yang aktif. Plugin ini TIDAK AKAN PERNAH mengeksekusi kode secara otomatis.**

1. **Aturan Berhenti Mutlak (*Stop Condition*):** Begitu dokumen blueprint plan, sesi wawancara, atau hasil riset selesai disajikan di layar, **AGEN WAJIB BERHENTI**.
2. **Nol Modifikasi Diam-diam:** Agen dilarang keras membuat atau memodifikasi file kode produksi di belakang layar tanpa persetujuan eksplisit dari Anda (melalui konfirmasi chat atau klik tombol **Proceed** pada artefak rencana).

---

## 🕹️ Panduan Perintah Slash & Override Manual

### 1. Kontrol Utama
* `/spec` (atau `/spec on` / `/spec auto`): Mengaktifkan auto-klasifikasi dinamis *(default)*.
* `/spec off`: Menonaktifkan `/spec` dan kembali ke perilaku bawaan asisten.

### 2. Override Alur Kerja Manual
* `/spec plan`: Memaksa pembuatan blueprint plan bertahap secara langsung tanpa interview.
* `/spec grill-me`: Memaksa wawancara keputusan desain via bawaan `/grill-me`.
* `/spec research`: Memaksa riset sumber dokumentasi teknis via bawaan `research`.
* `/spec bypass`: Memaksa eksekusi langsung (melewati tahap planning).

---

## 📋 Protokol Badge Status

Ketika aktif, baris pertama dari setiap respons akan menampilkan mode persiapan yang sedang aktif:
* `> 📋 **gemini-spec: [AUTO: plan]**`
* `> 📋 **gemini-spec: [AUTO: grill-me]**`
* `> 📋 **gemini-spec: [AUTO: research]**`
* `> 📋 **gemini-spec: [AUTO: bypass]**`

*Komposisi dengan plugin lain:*
Ketika berjalan bersamaan dengan `gemini-mode-argon` dan `token-saver`:
```text
> 🟢 **gemini-mode-argon [AUTO: engineer] [high]** | 📋 **gemini-spec: [AUTO: plan]**
```

---

## 💡 Contoh Skenario Nyata

### Contoh 1: Fitur Ambigu $\rightarrow$ Mengarah ke `grill-me`
> **Prompt Pengguna:** *"Buatkan sistem audit log untuk semua aksi admin."*

Prompt hanya menyebutkan tujuan abstrak tanpa spesifikasi teknis (database mana, retensi data, sinkron/asinkron, struktur log).
```text
> 📋 gemini-spec: [AUTO: grill-me]

[Mengaktifkan wawancara native /grill-me via kartu ask_question]:
1. Di mana log audit ingin disimpan?
   - (Recommended) Tabel PostgreSQL terpisah
   - ElasticSearch / OpenSearch cluster
   - Object storage S3 / GCS
2. Apakah pencatatan log bersifat sinkron atau asinkron?
   - (Recommended) Asinkron melalui background worker
   - Sinkronus dalam transaksi database
```
*Setelah pengguna menjawab:* Merangkum keputusan ke dalam blueprint plan final $\rightarrow$ **BERHENTI untuk ditinjau**.

---

### Contoh 2: Fitur Berspesifikasi Lengkap $\rightarrow$ Mengarah ke `plan`
> **Prompt Pengguna:** *"Tambahkan tabel audit log `audit_logs` (id, user_id, action, ip_address, created_at) via Prisma migration, buat middleware AuditLogger di `src/middleware/audit.ts`, dan pasang di semua route `/admin/*`."*

Prompt sudah mencantumkan nama tabel, struktur field, path file, dan route secara jelas. Melakukan wawancara hanya akan membuang waktu.
```text
> 📋 gemini-spec: [AUTO: plan]

[Menyusun rencana implementasi bertahap]:
- Tahap 1: Buat migrasi Prisma untuk tabel audit_logs
- Tahap 2: Implementasi middleware AuditLogger dengan ekstraksi IP
- Tahap 3: Pasang middleware pada router /admin
- Tahap 4: Tes verifikasi di audit.test.ts

[Menyajikan artefak rencana lengkap dengan tombol Proceed] -> BERHENTI untuk ditinjau.
```

---

## 📦 Panduan Instalasi

Pasang ke dalam direktori plugin Antigravity lokal Anda:

```bash
git clone https://github.com/diinggos/gemini-spec.git ~/.gemini/config/plugins/gemini-spec
```

Mulai ulang Antigravity atau buka percakapan baru. Plugin akan terdeteksi dan dimuat secara otomatis.

---

## 📄 Lisensi

Proyek ini dilisensikan di bawah [Lisensi MIT](LICENSE) - lihat file LICENSE untuk detailnya.
