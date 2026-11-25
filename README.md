# Panduan Pengolahan Dataset CSV

Repo ini adalah kumpulan notebook untuk pekerjaan CSV, dari tugas sehari-hari sampai pencocokan data yang lebih rumit. Setiap notebook berdiri sendiri: buka notebook sesuai kebutuhan, ubah bagian **KONFIGURASI** di dekat atas, lalu jalankan sel dari atas ke bawah.

File sumber di folder `Input` tidak ditimpa. Semua hasil disimpan di folder `Output`; menjalankan ulang notebook dapat mengganti hasil lama dengan nama yang sama. Notebook 11 akan berhenti jika file hasil sudah ada, kecuali Anda mengaktifkan penggantian secara khusus.

## Mulai cepat

1. Letakkan semua file CSV masukan di folder `Input`, sejajar dengan notebook. Simpan hasil notebook di folder `Output` yang juga sejajar dengan notebook.
2. Buka notebook dengan Jupyter Notebook, JupyterLab, atau Visual Studio Code.
3. Di sel konfigurasi paling atas, sesuaikan nama file, kolom, dan pilihan proses.
4. Jalankan notebook dari atas ke bawah.
5. File hasil akan muncul di folder `Output`. Folder ini dibuat otomatis jika belum ada.

Untuk file yang berada di tempat lain, Anda boleh menulis path lengkap. Jika CSV memakai titik koma sebagai pemisah kolom, ubah pengaturan `SEP` atau `INPUT_SEP` dari `,` menjadi `;`.

## Pilih notebook sesuai kebutuhan

| No. | Notebook | Gunakan untuk |
|---:|---|---|
| 1 | **Notebook 1 - Join DB** | Menggabungkan kolom dari beberapa file berdasarkan ID yang sama. |
| 2 | **Notebook 2 - Erase Column** | Memilih kolom yang disimpan atau membuang kolom tertentu. |
| 3 | **Notebook 3 - Append CSV** | Menumpuk baris dari beberapa file, misalnya data per bulan. |
| 4 | **Notebook 4 - Clean Data** | Merapikan spasi, penanda kosong, tanggal, dan angka. |
| 5 | **Notebook 5 - Remove Duplicates** | Menemukan dan menghapus baris duplikat. |
| 6 | **Notebook 6 - Split Dataset** | Membagi data menjadi train, validation, dan test. |
| 7 | **Notebook 7 - Reshape Table** | Mengubah tabel lebar menjadi panjang atau sebaliknya. |
| 8 | **Notebook 8 - Compare CSV** | Membandingkan dua versi CSV: baris baru, hilang, dan berubah. |
| 9 | **Notebook 9 - Data Quality Audit** | Membuat laporan nilai kosong, duplikat, dan nilai di luar aturan. |
| 10 | **Notebook 10 - Fuzzy Match** | Mencari nama yang mirip meski ejaannya tidak persis sama. |
| 11 | **Notebook 11 - Large CSV** | Memproses file besar sedikit demi sedikit agar lebih hemat memori. |

## Alur yang paling umum

Untuk menggabungkan file, lalu merapikan kolom:

1. Jalankan **Notebook 1**. Atur file utama, kolom ID, file tambahan, dan jenis join. Hasil bawaan: `hasil_join.csv` di folder `Output`.
2. Jalankan **Notebook 2**. Hasil join tadi sudah menjadi sumber bawaan. Isi `KEEP_COLUMNS` untuk menyimpan kolom tertentu, atau gunakan `DROP_COLUMNS` untuk membuang beberapa kolom. Hasil bawaan: `hasil_trim_kolom.csv` di folder `Output`.

## Catatan pemakaian

### Join berdasarkan ID

Simpan file masukan di folder `Input` dan hasil akan ditulis ke folder `Output`. Kedua folder berada pada tingkat yang sama dengan semua notebook. Path bawaan sudah menunjuk ke folder tersebut.

Di Notebook 1, `left` mempertahankan semua baris dari file utama, sedangkan `inner` hanya mempertahankan ID yang ditemukan di kedua file. `outer` mempertahankan seluruh ID dari kedua sisi. Pastikan ID memang mengacu pada orang/barang yang sama di semua file. Jika sebuah ID muncul berulang, join bisa menghasilkan lebih banyak baris.

### Memilih atau membuang kolom

Di Notebook 2, cara paling aman untuk menyimpan hanya beberapa kolom adalah mengisi `KEEP_COLUMNS`, misalnya `['id', 'nama']`. Jika `KEEP_COLUMNS` diatur ke `None`, daftar `DROP_COLUMNS` yang digunakan untuk membuang kolom.

### Pembersihan dan konversi

Notebook 4 dapat mengubah teks tanggal menjadi format tahun-bulan-hari dan mengubah kolom angka. Periksa hasilnya karena nilai yang tidak cocok dengan format akan menjadi kosong.

### Pembagian dataset

Notebook 6 dapat membagi baris secara acak dengan hasil yang dapat diulang. Jika baris dari orang atau dokumen yang sama tidak boleh tersebar ke beberapa bagian, isi `GROUP_COLUMN`. Nilai grup yang kosong perlu dibereskan terlebih dahulu.

### Fuzzy matching

Notebook 10 hanya menghasilkan kandidat kemiripan untuk diperiksa. Jangan langsung menganggap nama dengan skor tinggi sebagai orang/barang yang sama. Notebook ini memerlukan pustaka tambahan `rapidfuzz`; bila belum terpasang, jalankan `pip install rapidfuzz` pada lingkungan Python notebook. Untuk file besar, cobalah sampel terlebih dahulu lewat `LIMIT_ROWS`.

### File besar

Notebook 11 membaca CSV per bagian (`CHUNK_SIZE`). Jika hasil dengan nama yang sama sudah ada, notebook berhenti untuk mencegah penggantian yang tidak sengaja. Untuk menggantinya, ubah `OUTPUT_PATH` atau set `OVERWRITE_OUTPUT = True` setelah memastikan file lama memang boleh ditimpa.

## Kebutuhan Python

Notebook 1–9 dan 11 menggunakan `pandas`. Notebook 6 juga menggunakan `numpy` (sering sudah tersedia bersama pandas). Notebook 10 memerlukan `rapidfuzz`. Jika pustaka belum ada, minta bantuan untuk memasangnya di lingkungan Python yang dipakai Jupyter.

## Jika hasil tidak sesuai

- Pastikan path file benar dan nama file sama persis.
- Pastikan nama kolom pada konfigurasi sama persis dengan judul kolom di CSV.
- Periksa pemisah kolom CSV: koma atau titik koma.
- Periksa pesan ringkasan pada notebook sebelum memakai hasilnya.
- Jika ID berubah atau tidak cocok, ingat bahwa notebook membaca nilai sebagai teks agar nol di depan ID tetap terjaga.
