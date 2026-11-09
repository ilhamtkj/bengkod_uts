# Analisis Kepuasan Penumpang Maskapai

Branch `gpu` berisi dua notebook untuk analisis dan klasifikasi kepuasan penumpang. Notebook CPU menjadi pembanding, sedangkan notebook GPU mengulang alur pemodelan dengan cuML dan mengukur waktu pemrosesan pada CPU, transfer data, serta operasi GPU.

## Isi repositori

- `my-uts.ipynb` — EDA, analisis missing values, duplikasi, distribusi target, outlier, dan korelasi; dilanjutkan direct modeling, preprocessing, sampling kelas, evaluasi, feature importance, dan tuning scikit-learn.
- `my-uts_gpu.ipynb` — alur analisis yang sama dengan Logistic Regression, LinearSVC, dan Random Forest cuML. Preprocessing tetap memakai scikit-learn di CPU; data lalu ditransfer ke GPU. Notebook mengukur waktu preprocessing, transfer, fit, prediksi, dan transfer hasil secara terpisah. Grid search dilakukan pada GPU dengan 5-fold CV berurutan.
- `cuml_jlab.yml` — spesifikasi Conda untuk environment RAPIDS/cuML.
- `dataset/airline_passenger_satisfaction.csv` — dataset yang dibaca notebook dari path relatif. Folder `dataset/` diabaikan Git, jadi sediakan file ini secara lokal.

## Environment GPU

Environment cuML memerlukan Linux atau WSL2, GPU NVIDIA, dan driver yang mendukung versi CUDA terpilih. File `cuml_jlab.yml` saat ini menetapkan Python 3.14 dan `cuda-version=13.5`. Sebelum membuat environment, sesuaikan `cuda-version` dengan versi yang didukung RAPIDS dan driver pada mesin Anda (misalnya 13.3 atau 12.9). Hapus juga baris `prefix:` yang menunjuk ke path lokal jika file akan digunakan di komputer lain.

Setelah YAML disesuaikan:

```bash
conda env create -f cuml_jlab.yml
conda activate cuml_jlab
python -m ipykernel install --user \
  --name cuml_jlab \
  --display-name "Python (cuML GPU)"
jupyter lab
```

Pilih kernel **Python (cuML GPU)** untuk `my-uts_gpu.ipynb`. Pastikan `nvidia-smi` dapat melihat GPU dan jalankan sel notebook secara berurutan dari direktori repository.

Untuk membuat lockfile setelah spesifikasi environment dapat di-resolve:

```bash
conda install -n cuml_jlab -c conda-forge conda-lock
conda-lock -f cuml_jlab.yml -p linux-64
```

## Membaca perbandingan

Notebook CPU dan GPU memakai implementasi solver yang tidak identik, sehingga skor model tidak harus sama. Direct modeling GPU menunjukkan bahwa LR dan LinearSVC memerlukan scaling agar konvergen dengan baik pada fitur yang skalanya berbeda jauh. Bandingkan durasi bersama metrik kualitas model; waktu transfer dan waktu training tersedia terpisah di notebook GPU.

Pada output yang tersimpan, tuning cuML memerlukan sekitar 6,5 detik untuk Logistic Regression, 3,2 detik untuk LinearSVC, dan 267 detik untuk Random Forest. Angka ini adalah hasil pada perangkat dan sesi eksekusi saat notebook disimpan, bukan jaminan waktu pada perangkat lain.

## Menjalankan dan memverifikasi

Tidak ada aplikasi build atau test suite otomatis. Untuk memverifikasi perubahan, restart kernel yang sesuai dan jalankan notebook dari awal sampai akhir. Pastikan dataset lokal tersedia dan periksa tabel, grafik, metrik, serta timestamp eksekusi sel.
