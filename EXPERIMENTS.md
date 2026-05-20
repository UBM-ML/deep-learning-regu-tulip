# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 |   4    | 256     |   selu     |  adamax   |   0.1  |   128 |  20    |  0.3    |  ~64%    |  ~176s     |
| 2 |  2     | 64      |    tanh    |   adam    | 0.0001 |  16   |   5    |  0.1    |   ~85%   |   ~50s     |
| 3 |   2    | 128     |     tanh   |   adam    |   0.1  |   16  |  20    |  0.1    |    ~10%  |  ~327s     |
| 4 |    4   |  64     |   sigmoid  |    adam   |   0.01 |  32   |    10  |  0.3    |  ~85%    |   ~53s     |
| 5 |   5    | 512     | sigmoid    |  rmsprop  |  0.001 | 512   |   50   |  0.5    |   75.45% |     ~778s  |

> **Eksperimen #0** = baseline (jangan ubah, ini patokan kalian).

---

## 🧪 Detail Setiap Eksperimen

Gunakan template di bawah untuk SETIAP eksperimen.

---

### Eksperimen #1

**Apa yang diubah dari baseline:**
> Mengganti LR dari 0.1 ke 0.0001

**Hipotesis sebelum run:**
> LR yang tinggi dapat menyebabkan model 'melompati' titik optimal selama pelatihan, sehingga model tidak pernah mencapai akurasi terbaiknya, saya mengubah LR 0.0001 agar model lebih optimal dalam pelatihan sehingga mencapai akurasi yang lebih tinggi.

**Hasil:**
- Test accuracy: ~87%
- Train accuracy: ~87%
- Validation accuracy: ~88%
- Train time: ~161 detik
- Apakah overfit/underfit? tidak ada ovefit ataupun underfit dari hasil training model ini.

**Observasi & Insight:**
> LR kecil cocok untuk model ini, karena model menunjukkan bahwa model sedang belajar dengan efektif dan bergerak menuju solusi optimal tanpa overshooting atau kesulitan menemukan arah, hasilnya model dapat menghasilkan akurasi yang lebih tinggi daripada hasil sebelumnya 

**Rencana eksperimen berikutnya:**
> Optimizer saya ubah menjadi adam karena optimizer adam seringkali memberikan kinerja yang sangat baik dalam model yang sudah memberikan akurasi baik, epoch saya naikkan agar model dapat belajar lebih dalam dan memperbaiki kesalahan model, meningkatkan neuron per layer menjadi 512 agar kapasitas pembelajaran model lebih optimal, terakhir saya ubah dropout rate dari 0.3 ke 0.0-0.1 karena tidak adanya over/underfitting.

---

### Eksperimen #2

**Apa yang diubah:**
> Menambah hidden layers dari 1 menjadi 2. Mengganti fungsi aktivasi dari relu menjadi tanh. Mengganti optimizer dari sgd menjadi adam. Menurunkan learning rate dari 0.01 menjadi 0.0001. Mengurangi batch size dari 32 menjadi 16. Mengurangi jumlah epochs dari 10 menjadi 5. Menambahkan dropout rate dari 0.0 menjadi 0.1.

**Hipotesis:**
> Penggunaan optimizer Adam dipadukan dengan learning rate yang jauh lebih kecil (0.0001) akan membuat konvergensi model berjalan lebih stabil dan terarah. Penambahan satu hidden layer bertujuan meningkatkan kapasitas model dalam mempelajari pola, sementara penambahan dropout 0.1 berfungsi sebagai langkah preventif untuk mencegah overfitting meskipun model memiliki arsitektur yang lebih kompleks.

**Hasil:**
- Test accuracy: ~85%
- Train accuracy: ~86%
- Validation accuracy: ~86%
- Train time: ~50 detik
- Apakah overfit/underfit? tidak ada ovefit ataupun underfit dari hasil training model ini.

**Observasi:**
Meskipun epochs dipotong menjadi setengahnya (5 epochs), model berhasil menyamai performa baseline (~85%). Hal ini menunjukkan bahwa kombinasi optimizer Adam dan fungsi aktivasi tanh membuat model belajar dengan cukup efisien. Grafik pergerakan loss dan accuracy terlihat mulus. Kurva antara data train dan validation saling berhimpitan, menandakan bahwa dropout 0.1 berhasil menjaga model agar dapat menggeneralisasi data dengan baik. Karena grafik loss masih menunjukkan tren menurun di akhir epoch ke-5 tanpa tanda-tanda memisah dari kurva validasi, model ini kemungkinan belum mencapai performa maksimalnya. Menambah jumlah epochs pada eksperimen selanjutnya dapat memberikan ruang lebih bagi model untuk mencapai akurasi yang lebih tinggi.

---

### Eksperimen #3

**Apa yang diubah:**
>Mengurangi jumlah hidden layers dari 5 menjadi 2. Mengurangi jumlah neurons per layer dari 512 menjadi 128. Mengganti fungsi aktivasi dari sigmoid menjadi tanh. Mengganti optimizer dari rmsprop menjadi adam. Menaikkan learning rate secara signifikan dari 0.001 menjadi 0.1. Mengurangi batch size dari 512 menjadi 16. Mengurangi jumlah epochs dari 50 menjadi 20. Menurunkan dropout rate dari 0.5 menjadi 0.1.

**Hipotesis:**
>Penggunaan optimizer Adam dan fungsi aktivasi tanh diharapkan dapat mempercepat konvergensi di awal training dibandingkan kombinasi sigmoid dan rmsprop pada baseline. Namun, lonjakan learning rate yang sangat ekstrem (0.1) dipadukan dengan batch size kecil (16) diprediksi akan membuat pembaruan bobot menjadi terlalu agresif dan tidak stabil. Arsitektur yang diperkecil (2 layers, 128 neurons) mungkin akan membatasi kapasitas model, tetapi penurunan dropout menjadi 0.1 dilakukan agar model tidak terlalu terhambat dalam mempelajari pola data yang ada.

**Hasil:**
- Test accuracy: 10.00%
- Train accuracy: 9.87%
- Validation accuracy: 9.85%
- Train time: ~327 detik
- Apakah overfit/underfit? Model mengalami kegagalan belajar total akibat overshooting (underfitting ekstrem).

**Observasi:**
>Hasil akurasi yang tertahan di kisaran ~10% (dengan loss mencapai 4.9323) mengonfirmasi bahwa model sama sekali tidak belajar dan hanya menebak secara acak sejak awal epoch. Penyebab utamanya adalah nilai learning rate yang terlalu besar (0.1) untuk ukuran optimizer adaptif seperti Adam. Hal ini memicu terjadinya overshooting, di mana pembaruan bobot terlalu ekstrem hingga melompati titik minimum dan merusak fungsi pemetaan grafiknya. Dari sisi efisiensi waktu, meskipun kapasitas model diperkecil, waktu training tetap membengkak hingga ~327 detik untuk 20 epochs. Ini membuktikan bahwa batch size yang sangat kecil (16) menciptakan terlalu banyak iterasi per epoch, sehingga meningkatkan overhead komputasi secara keseluruhan.

---

### Eksperimen #4

**Apa yang diubah dari baseline:**  
> Menggunakan `4 hidden layer`, activation function `sigmoid`, optimizer `adam`, serta dropout `0.3`.

**Hipotesis sebelum run:**  
> Penambahan hidden layer diharapkan dapat meningkatkan kemampuan model dalam mengenali pola yang lebih kompleks. Dropout digunakan untuk mengurangi kemungkinan overfitting selama training.

**Hasil:**  
- Test accuracy: ~85%  
- Train accuracy: ~87%  
- Validation accuracy: ~86%  
- Train time: ~53 detik  
- Apakah overfit/underfit?: tidak terdapat overfitting maupun underfitting karena performa train dan validation masih stabil.

**Observasi & Insight:**  
> Penambahan layer dan dropout memberikan hasil yang cukup stabil. Namun activation sigmoid membuat proses pembelajaran tidak secepat ReLU sehingga peningkatan akurasi tidak terlalu signifikan dibanding eksperimen sebelumnya.

---


### Eksperimen #5

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

## 🏆 Konfigurasi Terbaik

Setelah semua eksperimen, salin konfigurasi terbaik kalian ke sini:

```python
HIDDEN_LAYERS     = ?
NEURONS_PER_LAYER = ?
ACTIVATION        = ?
DROPOUT_RATE      = ?
OPTIMIZER         = ?
LEARNING_RATE     = ?
BATCH_SIZE        = ?
EPOCHS            = ?
```

**Test accuracy final: ___%**
