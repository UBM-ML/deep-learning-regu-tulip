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
| 4 |    4    |    64     |       sigmoid     |    adam       |   0.01     |    0.01   |     32   |     10    |    ~85%      |       ~53s     |
| 5 |        |         |            |           |        |       |        |         |          |            |

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

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #3

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #4

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

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
