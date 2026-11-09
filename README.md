# Analisis Kepuasan Penumpang Maskapai

Proyek ini menganalisis data kepuasan penumpang maskapai dan membangun model klasifikasi untuk memprediksi kolom `Satisfaction`. Seluruh analisis pada branch `master` dijalankan menggunakan Python dan scikit-learn pada CPU.

## Isi repositori

- `my-uts.ipynb` — notebook utama berisi eksplorasi data, visualisasi, preprocessing, pemodelan, evaluasi, feature importance, dan tuning hyperparameter.
- `jlab.yml` — spesifikasi environment Conda untuk menjalankan notebook.
- `dataset/airline_passenger_satisfaction.csv` — dataset input lokal. Direktori `dataset/` diabaikan Git; pastikan CSV tersedia di path tersebut.

Notebook membandingkan Logistic Regression, LinearSVC, dan Random Forest dalam dua alur: direct modeling dengan encoding, serta alur preprocessing yang menangani nilai kosong, encoding kategori, scaling fitur numerik, dan sampling kelas. Bagian optimasi menggunakan GridSearchCV dengan validasi silang 5-fold untuk tuning ketiga model.

## Persiapan environment

Buat dan aktifkan environment dari file YAML:

```bash
conda env create -f jlab.yml
conda activate jlab
```

Jika environment `jlab` sudah ada, perbarui dengan `conda env update -n jlab -f jlab.yml --prune`.

## Menjalankan notebook

Dari direktori utama repository, jalankan:

```bash
jupyter lab
```

Buka `my-uts.ipynb`, pilih kernel environment `jlab`, lalu jalankan semua sel berurutan. Notebook membaca dataset dengan path relatif `dataset/airline_passenger_satisfaction.csv`. Output mencakup ringkasan data, grafik EDA, metrik evaluasi, confusion matrix, feature importance, dan perbandingan model sebelum/sesudah preprocessing serta tuning.

## Catatan

Tidak ada aplikasi build atau test suite otomatis. Hasil notebook bergantung pada tersedianya dataset lokal dan versi library dalam environment. Untuk perubahan analisis, jalankan ulang notebook dari awal dan periksa tabel, grafik, serta metrik yang dihasilkan.
