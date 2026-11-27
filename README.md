# UTS_DAM_2501010174 — Data Acquisition & Management

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME_GITHUB/UTS_DAM_2501010174/blob/main/UTS_DAM_2501010174.ipynb)


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
| 1 | Unduh dataset | Dinas Pariwisata Provinsi Bali — Buku Statistik Pariwisata Bali 2025 (berkas `Table-24-31-Final-5.xls`) | Halaman: https://disparda.baliprov.go.id/buku-statistik-pariwisata-bali-tahun-2025 · Berkas: https://cloud-ng.baliprov.go.id/disparda/2026/04/Table-24-31-Final-5.xls | Excel (.xls) |
| 2 | API | Open-Meteo Historical Weather API | https://archive-api.open-meteo.com/v1/archive | JSON |
| 3 | Web scraping | Dinas Pariwisata Provinsi Bali — halaman Data Statistik (listing dokumen statistik) | https://disparda.baliprov.go.id/data-statistik | HTML / listing (judul dan URL dokumen) |

**Catatan:**
- Lisensi dataset: hak cipta Pemerintah Provinsi Bali; dilarang mereproduksi atau menggandakan isi buku untuk tujuan komersial tanpa izin tertulis. Data dipakai non-komersial untuk tugas kuliah dengan mencantumkan sumber.
- Open-Meteo: CC BY 4.0 (atribusi). Tanggal akses, ukuran berkas, dan hash MD5 setiap sumber tercatat pada `docs/provenance.csv`.
- Bukti pemeriksaan `robots.txt` ada di `docs/robots_check_dataset.json` (portal dataset) dan `docs/robots_check.json` (halaman scraping).
- Tidak ada data dari Wikipedia, Booking.com, Agoda, Traveloka, tiket.com, Airbnb, Tripadvisor, Google Maps, maupun media sosial.

## 3. Goal / Tujuan

Topik yang digunakan adalah **Pariwisata Bali per Kabupaten/Kota**. Tujuan pengerjaan adalah:
1. mengakuisisi dataset statistik pariwisata resmi Disparda Bali (jumlah restoran/rumah makan, bar, dan daya tarik wisata per kabupaten/kota, 2019–2025);
2. mengambil data cuaca harian 2025 (suhu rata-rata dan curah hujan) di ibu kota 9 kabupaten/kota melalui API Open-Meteo;
3. men-scrape listing dokumen statistik dari halaman statis Disparda Bali dengan memeriksa `robots.txt` terlebih dahulu;
4. menggabungkan data berkas dan data API berdasarkan kunci wilayah (`kunci_wilayah`, nama kabupaten/kota ternormalisasi) dengan `merge(validate="one_to_one")`, lalu menghasilkan tabel analisis dan visualisasi.

Ringkasan dataset berkas: 8 sheet, 4 sheet memuat data per kabupaten/kota (TAB 24, 25, 29, 31), diubah menjadi tabel long 201 baris, 9 kabupaten/kota Bali, cakupan waktu 2019–2025, ukuran berkas ± 0,12 MB. Estimasi storage 1 tahun (× 12 bulan + cadangan 30%) ± 1,93 MB.

## 4. Data Raw

Folder `data/raw/` digunakan untuk menyimpan seluruh hasil akuisisi mentah tanpa perubahan.

| Jenis Data | Format | Keterangan |
|---|---|---|
| Dataset unduhan | Excel (.xls) | `Table-24-31-Final-5.xls` dari Disparda Bali, asli tanpa diubah |
| Data API | JSON | Respons mentah Open-Meteo per kabupaten/kota (`cuaca_openmeteo_<wilayah>.json`) dan `cuaca_openmeteo_semua.json` |
| Data scraping | HTML | `halaman_data_statistik_disparda.html`, HTML asli halaman Data Statistik Disparda |

## 5. Process

Folder `Process/` digunakan untuk menyimpan data hasil pembacaan, normalisasi, pembersihan, penggabungan, dan visualisasi.

| Hasil Proses | Format |
|---|---|
| Dataset berkas bersih (tabel long per kabupaten/kota) | CSV (`dataset_berkas_long.csv`) |
| Data API ternormalisasi (harian, 3.285 baris) | CSV / JSON (`cuaca_harian_bersih`) |
| Data scraping terstruktur (listing dokumen statistik) | CSV / JSON (`listing_statistik_pariwisata`) |
| Hasil penggabungan berkas + API per kabupaten/kota | CSV / JSON / HTML (`gabungan_pariwisata_bali`) |
| Visualisasi hasil gabungan | PNG (`visual_gabungan.png`) |

## 6. Dokumentasi

Folder `docs/` berisi:

| Berkas | Isi |
|---|---|
| `provenance.csv` | URL, tanggal akses, lisensi, metode, ukuran, dan MD5 tiap sumber |
| `data_ethics_checklist.csv` | Data Ethics Checklist 9 butir beserta bukti |
| `klasifikasi_pii.csv` | Klasifikasi kolom (PII / quasi-identifier / non-PII) dan hasil pemindaian pola PII |
| `robots_check_dataset.json`, `robots_check.json` | Bukti pemeriksaan `robots.txt` portal dataset dan halaman scraping |
| `estimasi_storage.csv` | Perhitungan estimasi storage 1 tahun |
| `metadata_gabungan.json` | Metadata hasil merge (sumber, kunci, tipe merge, jumlah baris, MD5) |

## 7. Cara Menjalankan

1. Buka notebook `UTS_DAM_2501010174.ipynb` melalui Google Colab atau Jupyter.
2. Siapkan email untuk User-Agent. Notebook akan memintanya saat dijalankan (`input`), atau bisa diisi lewat variabel `EMAIL_KAMPUS` di file `.env` jika dijalankan lokal. Email tidak ditulis di dalam notebook. Petunjuk soal meminta email kampus; jika tidak tersedia, notebook hanya memberi peringatan dan penggunaannya perlu dikonfirmasi ke dosen.
3. Jalankan seluruh sel notebook secara berurutan. Saat diminta, unggah berkas `Table-24-31-Final-5.xls` (unduh dari halaman Buku Statistik Pariwisata Bali 2025 di Disparda Bali) dan tempel URL berkasnya.
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

**Dataset utama:** data statistik pariwisata resmi dari [Dinas Pariwisata Provinsi Bali](https://disparda.baliprov.go.id/buku-statistik-pariwisata-bali-tahun-2025), berkas Excel `Table-24-31-Final-5.xls` (restoran/rumah makan, bar, kawasan dan daya tarik wisata per kabupaten/kota). Notebook memvalidasi minimal 100 baris dan minimal 5 kabupaten/kota Bali sebelum melanjutkan.

**Keterbatasan:** hanya 9 wilayah sehingga korelasi bersifat deskriptif dan bukan bukti sebab-akibat; cuaca diambil di titik ibu kota kabupaten/kota; periode data berkas Disparda dan cuaca (2025) dapat berbeda.
