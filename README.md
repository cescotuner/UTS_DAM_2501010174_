# UTS_DAM_2501010174 — Data Acquisition & Management

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME_GITHUB/UTS_DAM_2501010174/blob/main/UTS_DAM_2501010174.ipynb)

> Setelah repository GitHub dibuat, ganti `USERNAME_GITHUB` dengan username GitHub Anda.

## 1. Data Diri

| Keterangan | Identitas |
|---|---|
| Nama | Francesco Nera Alfi Nanggor |
| NIM | 2501010174 |
| Program Studi | Informatika — Management Data Analyst |
| Kelas | F |
| Mata Kuliah | Data Acquisition & Management |
| Dosen | Dr. I Gede Totok Suryawan, S.Kom., M.T. |

## 2. Sumber / URL

| No. | Metode Akuisisi | Sumber | URL | Bentuk Data |
|---|---|---|---|---|
| 1 | Unduh dataset | Portal data terbuka (data.go.id / katalog.data.go.id) | URL aktual dicatat setelah akuisisi pada `docs/provenance.csv` | CSV / Excel |
| 2 | API | Open-Meteo Historical Weather API | https://archive-api.open-meteo.com/v1/archive | JSON |
| 3 | Web scraping | Halaman tabel statistik BPS Provinsi Bali yang lolos pemeriksaan robots.txt | URL halaman aktual dicatat pada `docs/provenance.csv` dan `docs/robots_check.json` | HTML / tabel |

**Catatan:** URL dataset dan halaman scraping yang benar-benar berhasil diakses harus diverifikasi dari hasil notebook. Jangan mengisi URL atau lisensi berdasarkan perkiraan.

## 3. Goal / Tujuan

Topik yang digunakan adalah **Pariwisata Bali per Kabupaten/Kota**. Tujuan pengerjaan adalah mengakuisisi data pariwisata melalui dataset terbuka, mengambil data cuaca melalui API Open-Meteo, serta mengambil tabel statistik dari halaman pemerintah yang diizinkan. Data dari minimal dua sumber kemudian digabungkan berdasarkan kunci wilayah yang bermakna untuk menghasilkan tabel analisis dan visualisasi.

## 4. Data Raw

Folder `data/raw/` digunakan untuk menyimpan seluruh hasil akuisisi mentah tanpa perubahan.

| Jenis Data | Format | Keterangan |
|---|---|---|
| Dataset unduhan | CSV / Excel | Dataset asli dari portal terbuka, minimal 100 baris |
| Data API | JSON | Respons mentah Open-Meteo |
| Data scraping | HTML | HTML asli halaman BPS yang diizinkan |

## 5. Process

Folder `Process/` digunakan untuk menyimpan data hasil pembacaan, normalisasi, pembersihan, penggabungan, dan visualisasi.

| Hasil Proses | Format |
|---|---|
| Dataset berkas bersih | CSV |
| Data API ternormalisasi | CSV / JSON |
| Data scraping terstruktur | CSV / JSON / HTML |
| Hasil penggabungan | CSV / JSON / HTML |
| Visualisasi hasil gabungan | PNG |

## 6. Dokumentasi

Folder `docs/` berisi catatan provenance, Data Ethics Checklist, bukti pemeriksaan `robots.txt`, klasifikasi PII, estimasi storage, dan metadata hasil penggabungan. Berkas dokumentasi yang dihasilkan notebook akan tersimpan di folder ini.

## 7. Cara Menjalankan

1. Buka notebook `UTS_DAM_2501010174.ipynb` melalui Google Colab atau Jupyter.
2. Isi email pribadi pribadi pada Colab Secrets dengan nama `EMAIL_PRIBADI`, atau file `.env` jika dijalankan secara lokal.
3. Jalankan seluruh sel notebook secara berurutan.
4. Periksa bahwa dataset mentah tersimpan di `data/raw/`, hasil olahan di `Process/`, dan dokumentasi di `docs/`.
5. Pastikan semua sel selesai dijalankan dan hasil akuisisi benar-benar tersedia sebelum repository dibagikan.

## 8. Struktur Folder

```text
UTS_DAM_2501010174/
├── README.md
├── UTS_DAM_2501010174.ipynb
├── requirements.txt
├── .env.example
├── data/
│   └── raw/                 # Data mentah sesuai instruksi UTS
├── Process/                 # Data bersih, hasil merge, dan visualisasi
└── docs/                    # Provenance, checklist, dan bukti robots.txt
```


**Dataset utama:** gunakan data statistik pariwisata resmi dari [Dinas Pariwisata Provinsi Bali](https://disparda.baliprov.go.id/buku-statistik-pariwisata-bali-tahun-2025). Pilih berkas Excel yang memenuhi minimal 100 baris dan memuat sekurang-kurangnya satu kabupaten/kota Bali. Notebook akan memvalidasi syarat ini sebelum melanjutkan.
