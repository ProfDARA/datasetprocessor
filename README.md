# Panduan Pengolahan Dataset CSV

Repo ini adalah kumpulan notebook untuk pekerjaan CSV, dari tugas sehari-hari sampai pencocokan data yang lebih rumit. Setiap notebook berdiri sendiri: buka notebook sesuai kebutuhan, ubah bagian **PENGATURAN YANG BISA DIUBAH** di dekat atas, lalu jalankan sel dari atas ke bawah.

File sumber di folder `Input` tidak ditimpa. Semua hasil disimpan di folder `Output`; menjalankan ulang notebook dapat mengganti hasil lama dengan nama yang sama. Notebook 11 akan berhenti jika file hasil sudah ada, kecuali Anda mengaktifkan penggantian secara khusus. Isi folder `Input`, `Output`, dan `output` diabaikan oleh Git (kecuali file `.gitkeep`) agar dataset dan hasil kerja lokal tidak ikut masuk repo.

## Persiapan awal

Sebelum menjalankan notebook, buka terminal di folder repo lalu pasang semua pustaka yang diperlukan:

```powershell
python -m pip install -r requirements.txt
```

Jalankan Jupyter dari lingkungan Python yang sama dengan perintah tersebut (`python -m notebook`), atau pilih interpreter itu sebagai kernel di Visual Studio Code. Langkah ini memasang `pandas`, `numpy`, `rapidfuzz`, dan Jupyter Notebook.

## Mulai cepat

1. Letakkan semua file CSV masukan di folder `Input`, sejajar dengan notebook. Simpan hasil notebook di folder `Output` yang juga sejajar dengan notebook.
2. Buka notebook dengan Jupyter Notebook, JupyterLab, atau Visual Studio Code.
3. Di bagian pengaturan yang bisa diubah, sesuaikan nama file, kolom, dan pilihan proses.
4. Jalankan notebook dari atas ke bawah.
5. File hasil akan muncul di folder `Output`. Folder ini dibuat otomatis jika belum ada.

Untuk file yang berada di tempat lain, Anda boleh menulis path lengkap. Jika CSV memakai titik koma sebagai pemisah kolom, ubah pengaturan `Separator_CSV` dari `,` menjadi `;`. Pengaturan ini tersedia dengan nama yang sama di setiap notebook.

## Pilih notebook sesuai kebutuhan

| No. | Notebook | Gunakan untuk |
|---:|---|---|
| 1 | **Notebook 1 - Join DB** | Menggabungkan kolom dari beberapa file berdasarkan ID yang sama. |
| 2 | **Notebook 2 - Erase Column** | Memilih kolom yang disimpan atau membuang kolom tertentu. |
| 3 | **Notebook 3 - Append CSV** | Menumpuk baris dari beberapa file, misalnya data per bulan. |
| 4 | **Notebook 4 - Clean Data** | Merapikan spasi, penanda kosong, tanggal, dan angka. |
| 5 | **Notebook 5 - Remove Duplicates** | Menemukan dan menghapus baris duplikat. |
| 6 | **Notebook 6 - Split Dataset** | Membagi data menjadi latih, validasi, dan uji. |
| 7 | **Notebook 7 - Reshape Table** | Mengubah tabel lebar menjadi panjang atau sebaliknya. |
| 8 | **Notebook 8 - Compare CSV** | Membandingkan dua versi CSV: baris baru, hilang, dan berubah. |
| 9 | **Notebook 9 - Data Quality Audit** | Membuat laporan nilai kosong, duplikat, dan nilai di luar aturan. |
| 10 | **Notebook 10 - Fuzzy Match** | Mencari nama yang mirip meski ejaannya tidak persis sama. |
| 11 | **Notebook 11 - Large CSV** | Memproses file besar sedikit demi sedikit agar lebih hemat memori. |

## Alur yang paling umum

Untuk menggabungkan file, lalu merapikan kolom:

1. Jalankan **Notebook 1**. Atur file utama, kolom ID, file tambahan, dan jenis join. Hasil bawaan: `hasil_join.csv` di folder `Output`.
2. Jalankan **Notebook 2**. Atur `Pertahankan_Kolom` untuk menyimpan kolom tertentu, atau gunakan `Hapus_Kolom` untuk membuang beberapa kolom. Hasil bawaan: `hasil_trim_kolom.csv` di folder `Output`.

## Catatan pemakaian

### Join berdasarkan ID

Simpan file masukan di folder `Input` dan hasil akan ditulis ke folder `Output`. Kedua folder berada pada tingkat yang sama dengan semua notebook. Path bawaan sudah menunjuk ke folder tersebut.

Di Notebook 1, `left` mempertahankan semua baris dari file utama, sedangkan `inner` hanya mempertahankan ID yang ditemukan di kedua file. `outer` mempertahankan seluruh ID dari kedua sisi. Pastikan ID memang mengacu pada orang/barang yang sama di semua file. Jika sebuah ID muncul berulang, join bisa menghasilkan lebih banyak baris.

### Memilih atau membuang kolom

Di Notebook 2, cara paling aman untuk menyimpan hanya beberapa kolom adalah mengisi `Pertahankan_Kolom`, misalnya `['id', 'nama']`. Jika `Pertahankan_Kolom` diatur ke `None`, daftar `Hapus_Kolom` digunakan untuk menentukan kolom yang dibuang.

### Pembersihan dan konversi

Notebook 4 dapat mengubah teks tanggal menjadi format tahun-bulan-hari dan mengubah kolom angka. Periksa hasilnya karena nilai yang tidak cocok dengan format akan menjadi kosong.

### Pembagian dataset

Notebook 6 dapat membagi baris secara acak dengan hasil yang dapat diulang. Jika baris dari orang atau dokumen yang sama tidak boleh tersebar ke beberapa bagian, isi `Kolom_Grup`. Nilai grup yang kosong perlu dibereskan terlebih dahulu.

### Fuzzy matching

Notebook 10 hanya menghasilkan kandidat kemiripan untuk diperiksa. Jangan langsung menganggap nama dengan skor tinggi sebagai orang/barang yang sama. Pustaka `rapidfuzz` sudah tercantum di `requirements.txt`; jalankan perintah pemasangan di bagian Persiapan awal sebelum membuka notebook. Untuk file besar, cobalah sampel terlebih dahulu lewat `Batas_Baris`.

### File besar

Notebook 11 membaca CSV per bagian (`Ukuran_Bagian`). Jika hasil dengan nama yang sama sudah ada, notebook berhenti untuk mencegah penggantian yang tidak sengaja. Untuk menggantinya, ubah `Output_CSV` atau set `Timpa_File_Output = True` setelah memastikan file lama memang boleh ditimpa.

## Pustaka yang digunakan

Daftar pustaka ada di [`requirements.txt`](requirements.txt): `pandas` dipakai Notebook 1 sampai 11, `numpy` dipakai Notebook 6, dan `rapidfuzz` dipakai Notebook 10. Paket `notebook` menyediakan aplikasi Jupyter Notebook.

## Jika hasil tidak sesuai

- Pastikan path file benar dan nama file sama persis.
- Pastikan nama kolom pada konfigurasi sama persis dengan judul kolom di CSV.
- Periksa pemisah kolom CSV: koma atau titik koma.
- Periksa pesan ringkasan pada notebook sebelum memakai hasilnya.
- Jika ID berubah atau tidak cocok, ingat bahwa notebook membaca nilai sebagai teks agar nol di depan ID tetap terjaga.
