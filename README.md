# Histogram Equalization

> Eksperimen dan implementasi manual peningkatan kualitas citra menggunakan metode **Global Histogram Equalization (HE)**.

## Deskripsi

Proyek ini menerapkan Histogram Equalization pada citra grayscale untuk meningkatkan penyebaran intensitas dan kontras citra. Proses HE dibuat secara manual menggunakan NumPy, kemudian dibandingkan dengan hasil dari `cv2.equalizeHist()`.

Eksperimen menggunakan citra `cat.jpeg` dan dijalankan melalui Google Colab.

## Menjalankan Notebook di Google Colab

1. Buka notebook melalui tautan berikut:

   [Buka di Google Colab](https://colab.research.google.com/github/haqiqien/globalhe/blob/main/python/Belajar_Histogram_Equalization.ipynb)

2. Jalankan sel notebook dari atas ke bawah.
3. Pada sel pertama, klik **Choose Files** atau tombol upload yang muncul.
4. Pilih file `img/cat.jpeg` dari repository atau unggah citra lain.
5. Amati hasil citra, histogram, CDF, tabel pemetaan, perbandingan OpenCV, dan statistiknya.

Jika library belum tersedia, jalankan sel berikut di Colab:

```python
!pip install -q numpy matplotlib opencv-python
```

## Tahapan Eksperimen

Notebook melakukan tahapan berikut:

1. Membaca dan mengubah citra menjadi grayscale.
2. Menghitung histogram citra.
3. Menghitung Cumulative Distribution Function (CDF).
4. Menentukan `cdf_min`.
5. Menormalisasi CDF ke rentang 0--255.
6. Memetakan setiap nilai piksel ke nilai baru.
7. Membandingkan hasil manual dengan `cv2.equalizeHist()`.
8. Membandingkan mean, standar deviasi, entropy, dan rentang intensitas.

Rumus pemetaan yang digunakan adalah:

\[
T(i) = \operatorname{round}\left(
\frac{\operatorname{cdf}(i)-\operatorname{cdf}_{\min}}
{N-\operatorname{cdf}_{\min}}\times255
\right)
\]

## Struktur Repository

```text
globalhe/
├── img/
│   ├── cat.jpeg
│   ├── perbandingan-visual.png
│   ├── proses-he.png
│   ├── statistik.png
│   └── verifikasi-opencv.png
├── python/
│   └── Belajar_Histogram_Equalization.ipynb
├── laporan_he_template.tex
├── Poin_Laporan_HE.md
└── README.md
```

## Hasil Utama

Berdasarkan eksperimen pada `cat.jpeg`:

| Statistik | Sebelum HE | Sesudah HE |
|---|---:|---:|
| Rata-rata kecerahan | 43.87 | 129.21 |
| Standar deviasi | 36.74 | 72.55 |
| Entropy | 6.627 | 6.508 |
| Rentang intensitas | 0--255 | 0--255 |

Peningkatan standar deviasi menunjukkan penyebaran intensitas dan kontras meningkat. Entropy tidak selalu meningkat karena Histogram Equalization mengubah distribusi piksel, bukan menambahkan informasi baru.

## Laporan

Template laporan tersedia pada [laporan_he_template.tex](laporan_he_template.tex). Laporan memuat teori, implementasi manual, verifikasi OpenCV, visualisasi, statistik, dan contoh perhitungan numerik.

Repository:

<https://github.com/haqiqien/globalhe>

## Referensi

- [OpenCV Histogram Equalization](https://docs.opencv.org/4.x/d4/d1b/tutorial_histogram_equalization.html)
- [NumPy histogram](https://numpy.org/doc/stable/reference/generated/numpy.histogram.html)
- [Google Colab](https://colab.research.google.com/)
