# Poin-Poin Laporan Tugas Enhancement Citra — Fokus Histogram Equalization (HE)

Konteks tugas: eksperimen/implementasi satu atau lebih metode peningkatan kualitas citra, tanpa batasan domain aplikasi. Kompleksitas metode dan kedalaman pembahasan menjadi pertimbangan utama penilaian.

Karena metode yang dicoba hanya HE, fokusnya diarahkan ke **kedalaman pembahasan satu metode**, bukan perbandingan banyak metode.

Laporan ini juga menyertakan hasil praktik langsung dari Google Colab dalam bentuk screenshot — cara menyisipkannya dijelaskan di bagian paling bawah.

---

## 1. Pendahuluan
- Latar belakang: kenapa citra kontras rendah butuh ditingkatkan kualitasnya
- Tujuan: eksperimen dan analisis Histogram Equalization
- Citra yang dipakai: sumber, jenis, dan alasan pemilihannya — jelaskan ciri kontras rendahnya (histogram menumpuk di area mana)

## 2. Dasar Teori
- Konsep histogram citra
- Penjelasan HE: `h(i)` → `cdf(i)` → normalisasi → pemetaan, sertakan rumus:

  ```
  baru(i) = round( (cdf(i) - cdf_min) / (N - cdf_min) × 255 )
  ```

- Jelaskan dengan bahasa sendiri kenapa proses ini menaikkan kontras — nilai yang sering muncul di histogram "direnggangkan" lebih jauh oleh pemetaan ini, karena cdf-nya melompat lebih curam di sekitar nilai tersebut

## 3. Metodologi / Implementasi
- Alur kerja: citra asli → grayscale → hitung histogram → hitung CDF → normalisasi → pemetaan piksel
- Tampilkan kode manual (bukan hanya `cv2.equalizeHist()`) — pembeda utama dari laporan yang sekadar memanggil satu fungsi bawaan
- Sertakan bukti verifikasi: hasil manual vs `cv2.equalizeHist()` identik atau nyaris identik (menunjukkan pemahaman proses, bukan sekadar pemakaian fungsi)

**Sisipkan di sini:**
- Screenshot sel kode implementasi manual di Colab
  `![Kode implementasi HE manual](screenshots/kode-he-manual.png)`
- Screenshot output verifikasi (angka selisih manual vs OpenCV)
  `![Verifikasi terhadap cv2.equalizeHist](screenshots/verifikasi-opencv.png)`

## 4. Hasil & Pembahasan (bagian terpenting)
- **Perbandingan visual**: citra asli vs hasil HE berdampingan
  `![Perbandingan citra asli dan hasil HE](screenshots/perbandingan-visual.png)`
- **Perbandingan histogram**: overlay sebelum/sesudah, jelaskan perubahan bentuknya
  `![Histogram sebelum dan sesudah HE](screenshots/histogram-overlay.png)`
- **Kurva CDF sebelum/sesudah** — menunjukkan pemahaman terhadap mekanisme, bukan hanya hasil akhir. Jelaskan hubungan antara kecuraman kurva CDF dan seberapa jauh nilai piksel direnggangkan
  `![Kurva CDF sebelum dan sesudah HE](screenshots/kurva-cdf.png)`
- **Statistik kuantitatif**: tabel mean, standar deviasi (kontras), dan entropy sebelum vs sesudah — lalu interpretasikan angkanya, bukan hanya ditampilkan
  `![Output statistik mean std entropy](screenshots/statistik.png)`
- **Uji tambahan** (wajib coba minimal satu, ini yang menambah kedalaman pembahasan):
  - HE pada citra yang kontrasnya sudah bagus dari awal → tunjukkan hasilnya tidak banyak berubah atau malah muncul artefak, jelaskan lewat kurva CDF-nya
    `![Uji HE pada citra kontras tinggi](screenshots/uji-kontras-tinggi.png)`
  - HE pada citra berwarna via channel V (HSV) dibandingkan bila diterapkan langsung ke R, G, B secara terpisah → tunjukkan dan jelaskan bedanya
    `![Uji HE pada citra berwarna via HSV](screenshots/uji-warna-hsv.png)`

## 5. Kesimpulan
- Ringkas kapan HE efektif dan kapan tidak, berdasarkan hasil eksperimen sendiri
- Sebutkan keterbatasan HE: bekerja secara global, tidak menyesuaikan diri terhadap area lokal citra

## 6. Referensi & Lampiran
- Sumber teori yang dirujuk
- Kode lengkap (notebook)

---

## Catatan Prioritas

Bagian yang paling berkontribusi pada nilai "kedalaman pembahasan" untuk laporan yang fokus HE saja:

1. Implementasi manual (bukan hanya fungsi bawaan)
2. Verifikasi terhadap `cv2.equalizeHist()`
3. Visualisasi kurva CDF, bukan hanya histogram
4. Minimal satu uji tambahan/eksperimen di luar kasus dasar

Keempat poin ini bersama-sama menunjukkan pemahaman terhadap mekanisme di balik HE, bukan sekadar pemakaian fungsi — itulah yang membuat pembahasan terasa dalam walau metode yang dicoba hanya satu.

---

## Cara Menyisipkan Screenshot dari Colab

1. **Ambil screenshot tiap output penting** di Colab — cukup screenshot area output-nya saja (gambar/grafik/teks hasil print), tidak perlu seluruh layar.
2. **Simpan semua screenshot dalam satu folder** bernama `screenshots/` yang sejajar dengan file markdown ini, lalu beri nama file yang jelas, misalnya:
   - `kode-he-manual.png`
   - `verifikasi-opencv.png`
   - `perbandingan-visual.png`
   - `histogram-overlay.png`
   - `kurva-cdf.png`
   - `statistik.png`
3. **Sintaks markdown untuk gambar**: `![Teks alternatif](screenshots/nama-file.png)` — placeholder di setiap bagian di atas sudah memakai format ini, tinggal pastikan nama filenya cocok dengan screenshot yang kamu simpan.
4. Kalau laporan akan diserahkan dalam bentuk Word atau PDF, gambar markdown ini akan otomatis ikut ter-render asalkan foldernya tetap berada di lokasi yang sama saat dikonversi — atau bisa juga screenshot ditempel manual satu-satu kalau menulis laporan langsung di Word.
5. Tambahkan **keterangan singkat di bawah tiap gambar** (mis. *"Gambar 1. Histogram citra sebelum dan sesudah Histogram Equalization"*) supaya pembaca laporan langsung tahu itu gambar apa tanpa perlu menebak dari konteks.
