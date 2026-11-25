# Panduan Pengolahan CSV

Repo ini berisi dua notebook untuk mengolah file CSV. Notebook dibuat agar Anda cukup mengganti beberapa pengaturan di bagian atas, lalu menjalankannya dari atas ke bawah.

## Isi repo

- **Notebook 1 - Join DB.ipynb** — menggabungkan beberapa file CSV yang memiliki ID yang sama, misalnya ID pelanggan atau kode produk.
- **Notebook 2 - Erase Column.ipynb** — membuang kolom yang tidak diperlukan dari sebuah file CSV. Secara bawaan, notebook ini membaca hasil dari Notebook 1.

## Persiapan

1. Siapkan file CSV yang ingin diolah.
2. Buat folder bernama `data` di dalam folder repo, lalu letakkan file sumber di sana.
3. Buka notebook dengan Jupyter Notebook, JupyterLab, atau Visual Studio Code.
4. Jalankan sel dari bagian paling atas ke bawah. Jika diminta memilih kernel, pilih Python 3.

Notebook membutuhkan Python dan pustaka `pandas`. Jika notebook memberi pesan bahwa `pandas` belum tersedia, minta bantuan untuk memasangnya pada lingkungan Python yang digunakan.

## Notebook 1 — Gabungkan file CSV

1. Buka **Notebook 1 - Join DB.ipynb**.
2. Pada bagian **KONFIGURASI**, ganti `FILE_UTAMA` dengan nama file utama Anda. Contoh: `data/pelanggan.csv`.
3. Isi `ID_UTAMA` dengan nama kolom ID pada file utama. Nama kolom harus sama persis dengan judul kolom di CSV.
4. Pada `FILE_JOIN`, isi nama/path file tambahan dan nama kolom ID-nya. Tambahkan satu baris untuk setiap file yang ingin digabungkan.
5. Pilih jenis gabungan pada `how`:
   - `left` mempertahankan semua baris dari file utama.
   - `inner` hanya mempertahankan ID yang ada di kedua file.
   - `outer` mempertahankan semua ID dari kedua file.
   - `right` mempertahankan semua baris dari file tambahan.
6. Jika CSV menggunakan titik koma untuk memisahkan kolom, ganti `sep` dari `,` menjadi `;`.
7. Jalankan semua sel. Hasilnya disimpan di `output/hasil_join.csv`.

Pastikan ID memang mewakili hal yang sama di semua file. Jika sebuah ID muncul beberapa kali di file tambahan, hasil gabungan dapat memiliki baris lebih banyak.

## Notebook 2 — Buang kolom

1. Buka **Notebook 2 - Erase Column.ipynb**.
2. Secara bawaan, `INPUT_PATH` mengarah ke `output/hasil_join.csv` dari Notebook 1. Jika ingin mengolah file lain, ganti path tersebut.
3. Cara paling aman adalah mengisi `KEEP_COLUMNS` dengan daftar kolom yang ingin disimpan, misalnya `["id", "nama"]`. Kolom lain akan dibuang.
4. Jika lebih mudah, biarkan `KEEP_COLUMNS = None`, lalu isi `DROP_COLUMNS` dengan nama kolom yang ingin dibuang.
5. Jika CSV menggunakan pemisah titik koma, ubah `INPUT_SEP` menjadi `;`.
6. Jalankan semua sel. Hasilnya disimpan di `output/tabel_trim.csv`.

File sumber tidak ditimpa. Notebook membuat file hasil baru di folder `output`.

## Jika hasil tidak sesuai

- Pastikan nama file dan nama kolom ditulis persis seperti yang ada di CSV.
- Pastikan path file benar dan file berada di folder yang disebutkan.
- Periksa pemisah CSV: biasanya koma (`,`) atau titik koma (`;`).
- Pastikan Notebook 1 sudah dijalankan sebelum Notebook 2 jika ingin memangkas hasil join.
