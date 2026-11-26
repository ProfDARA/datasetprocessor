# Panduan Notebook Pengolahan CSV

Proyek ini berisi notebook untuk berbagai pekerjaan CSV, seperti menggabungkan file, membersihkan data, membandingkan versi file, dan mencari nama yang mirip. Setiap notebook bisa dijalankan sendiri. Pilih notebook yang dibutuhkan, sesuaikan pengaturannya di bagian atas, lalu jalankan sel dari atas ke bawah.

Secara bawaan, notebook membaca file dari `Input` dan menyimpan hasil ke `Output`, sehingga file masukan tetap utuh. Jika nama file hasil sudah ada, beberapa notebook akan menggantinya. Notebook 11 berhenti jika file hasil dengan nama yang sama sudah ada. Ganti `Output_CSV` atau aktifkan `Timpa_File_Output` untuk melanjutkan. Berkas di folder `Input`, `Output`, dan `output` tidak disertakan ke Git agar dataset dan hasil kerja tetap lokal.

## Persiapan awal

Buka terminal di folder proyek, lalu pasang semua kebutuhan dengan satu perintah:

```powershell
python -m pip install -r requirements.txt
```

Buka Jupyter dari lingkungan Python yang sama dengan perintah tadi menggunakan `python -m notebook`. Jika memakai Visual Studio Code, pilih lingkungan Python tersebut sebagai kernel notebook. Paket yang dipasang meliputi `pandas`, `numpy`, `rapidfuzz`, dan Jupyter Notebook.

## Mulai Operasi CSV

1. Simpan file CSV yang akan diolah di folder `Input`.
2. Buka notebook yang sesuai dengan pekerjaan Anda.
3. Ubah pengaturan di bagian **PENGATURAN YANG BISA DIUBAH**, seperti nama file, kolom, dan pilihan proses.
4. Jalankan sel notebook dari atas ke bawah.
5. Ambil file hasilnya dari folder `Output`.

Folder `Output` akan dibuat otomatis jika belum ada. Jika file CSV Anda berada di lokasi lain, isi pengaturan file dengan alamat lengkapnya.

Pemisah kolom bawaan adalah koma. Jika CSV Anda memakai titik koma, ubah baris `Separator_CSV = ","` menjadi `Separator_CSV = ";"` di notebook yang digunakan.

## Pilih notebook

| No. | Notebook | Cocok untuk |
|---:|---|---|
| 1 | **Notebook 1 - Join DB** | Menggabungkan beberapa CSV berdasarkan kolom ID. |
| 2 | **Notebook 2 - Erase Column** | Memilih kolom yang ingin disimpan atau dibuang. |
| 3 | **Notebook 3 - Append CSV** | Menumpuk baris dari beberapa CSV, misalnya data bulanan. |
| 4 | **Notebook 4 - Clean Data** | Merapikan spasi, penanda kosong, tanggal, dan angka. |
| 5 | **Notebook 5 - Remove Duplicates** | Menemukan dan menghapus baris duplikat. |
| 6 | **Notebook 6 - Split Dataset** | Membagi data menjadi bagian latih, validasi, dan uji. |
| 7 | **Notebook 7 - Reshape Table** | Mengubah bentuk tabel dari lebar ke panjang, atau sebaliknya. |
| 8 | **Notebook 8 - Compare CSV** | Membandingkan dua CSV untuk melihat baris yang baru, hilang, atau berubah. |
| 9 | **Notebook 9 - Data Quality Audit** | Memeriksa nilai kosong, duplikat, dan nilai yang tidak sesuai aturan. |
| 10 | **Notebook 10 - Fuzzy Match** | Mencari nama yang ejaannya mirip untuk diperiksa. |
| 11 | **Notebook 11 - Large CSV** | Mengolah CSV besar per bagian agar lebih hemat memori. |

## Contoh alur kerja: gabungkan lalu pilih kolom

1. Di Notebook 1, atur file utama, kolom ID, dan file tambahan. Hasilnya mengikuti nama di `Output_CSV`.
2. Di Notebook 2, arahkan `Input_CSV` ke hasil Notebook 1. Isi `Pertahankan_Kolom` jika hanya kolom tertentu yang ingin disimpan. Jika ingin membuang beberapa kolom, biarkan `Pertahankan_Kolom = None` lalu isi `Hapus_Kolom`.

## Catatan penggunaan

### Menggabungkan berdasarkan ID

Pilih kolom ID yang merujuk pada objek yang sama di semua file. Pilihan jenis gabung `left` mempertahankan semua baris dari file utama, sedangkan `inner` hanya menyimpan ID yang ada di kedua file. Pilihan `outer` mempertahankan semua ID dari kedua sisi. Jika sebuah ID muncul berulang, hasil gabungan bisa memiliki lebih banyak baris.

### Membersihkan data

Notebook 4 bisa mengubah teks tanggal menjadi format tahun-bulan-hari dan mengubah isi kolom menjadi angka. Nilai yang tidak cocok dengan format akan menjadi kosong, jadi periksa hasilnya sebelum digunakan.

### Membagi data

Notebook 6 membagi baris secara acak dan hasilnya bisa diulang. Isi `Kolom_Grup` jika baris dari orang atau dokumen yang sama harus tetap berada di bagian yang sama. Pastikan kolom grup tidak memiliki nilai kosong.

### Mencari nama yang mirip

Notebook 10 menghasilkan daftar kandidat untuk ditinjau; notebook ini tidak menentukan sendiri bahwa dua nama adalah orang yang sama. Untuk mengolah banyak baris, isi `Batas_Baris` dengan jumlah sampel terlebih dahulu.

### Mengolah CSV besar

Notebook 11 membaca file sedikit demi sedikit sesuai `Ukuran_Bagian`. Jika file hasil dengan nama yang sama sudah ada, notebook akan berhenti. Ganti `Output_CSV`, atau atur `Timpa_File_Output = True` jika file lama memang boleh diganti.

## Paket yang digunakan

Semua paket yang diperlukan tercantum di [`requirements.txt`](requirements.txt). `pandas` dipakai semua notebook, `numpy` dipakai Notebook 6, `rapidfuzz` dipakai Notebook 10, dan `notebook` menyediakan aplikasi Jupyter Notebook.

## Jika menemui kendala

- Pastikan nama dan lokasi file di pengaturan sudah benar.
- Pastikan nama kolom sama persis dengan judul kolom di CSV.
- Periksa `Separator_CSV`; sesuaikan dengan pemisah kolom pada file.
- Pastikan notebook memakai lingkungan Python tempat paket di `requirements.txt` dipasang.
- Baca pesan ringkasan dan peringatan yang muncul sebelum memakai file hasil.
- ID dibaca sebagai teks agar angka nol di depan, seperti pada `00123`, tidak hilang.
- Misal masih menemui kendala boleh tanya saya langsung di email, akan dibantu saat waktu senggang dan diluar jam kerja
