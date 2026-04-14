# Jobsheet 3 Pengolahan Citra

## Identitas Mahasiswa
- Nama Mahasiswa: Alif Rahman Maulana
- NIM: 3.34.23.2.01
- Praktikum: Jobsheet 3 Pengolahan Citra

## Ringkasan Praktikum
Notebook `Jobsheet_3_Pengolahan_Citra.ipynb` berisi 7 topik utama pengolahan citra:
1. Transformasi negatif citra (grayscale dan berwarna)
2. Histogram dan ekualisasi histogram (grayscale dan berwarna)
3. Filter rata-rata (mean filter) pada citra grayscale dan berwarna
4. Filter median untuk reduksi noise salt-and-pepper pada citra grayscale dan berwarna
5. Transformasi gamma untuk pengaturan kecerahan/gelap citra
6. Perbandingan contrast stretching dan histogram equalization
7. Perbandingan performa mean filter vs median filter pada noise impuls

## Praktikum 1: Transformasi Negatif Citra
### Tujuan
Melakukan inversi intensitas citra dengan persamaan:
\[
I_{negatif} = 1 - I_{asal}
\]

### Hasil Praktikum
- Pada citra grayscale (`camera`), area terang menjadi gelap dan area gelap menjadi terang.
- Pada citra berwarna (`astronaut`), inversi terjadi pada setiap kanal RGB sehingga warna berubah menjadi komplemen warna aslinya.

### Output
- Visualisasi 2x2:
  - Grayscale original
  - Grayscale negative
  - Color original
  - Color negative

### Kesimpulan
Transformasi negatif efektif untuk menonjolkan detail tertentu yang kurang terlihat pada citra asli, terutama saat kontras objek-latar belakang pada citra asal kurang jelas.

## Praktikum 2: Histogram dan Ekualisasi Histogram
### Tujuan
Menganalisis sebaran intensitas piksel melalui histogram dan meningkatkan kontras citra dengan histogram equalization.

### Hasil Praktikum
- **Grayscale**:
  - Histogram awal menunjukkan distribusi intensitas yang tidak merata.
  - Setelah ekualisasi, distribusi intensitas lebih menyebar sehingga kontras global meningkat.
- **Citra berwarna**:
  - Histogram ditampilkan untuk kanal R, G, B.
  - Ekualisasi dilakukan per kanal, menghasilkan peningkatan kontras tetapi dapat mengubah keseimbangan warna.

### Output
- Figure grayscale (2x2):
  - Grayscale original
  - Histogram original
  - Grayscale equalized
  - Histogram equalized
- Figure color (2x2):
  - Color original
  - Histogram original RGB
  - Color equalized (per channel)
  - Histogram equalized RGB

### Kesimpulan
Ekualisasi histogram mampu meningkatkan kontras citra. Pada citra berwarna, ekualisasi per kanal RGB dapat meningkatkan detail, tetapi berpotensi menimbulkan pergeseran warna.

## Praktikum 3: Filter Rata-Rata (Mean Filter)
### Tujuan
Menghaluskan citra dengan merata-ratakan intensitas piksel dalam jendela kernel 5x5.

### Hasil Praktikum
- Pada citra grayscale, hasil filtering terlihat lebih halus namun detail tepi menjadi berkurang.
- Pada citra berwarna, filtering dilakukan per kanal RGB dan hasilnya serupa: noise halus berkurang, tetapi ketajaman berkurang.

### Output
- Grayscale:
  - Original
  - Filtered (5x5 Average)
- Color:
  - Original
  - Filtered (5x5 Average)

### Kesimpulan
Mean filter efektif untuk smoothing umum, tetapi menyebabkan blur pada tepi dan detail halus. Cocok untuk pra-pemrosesan sebelum tahap lanjutan yang tidak sensitif terhadap ketajaman tinggi.

## Praktikum 4: Filter Median dengan Noise Salt-and-Pepper
### Tujuan
Mengurangi noise impuls (salt-and-pepper) menggunakan median filter dengan structuring element disk radius 3.

### Hasil Praktikum
- Noise salt-and-pepper ditambahkan sebesar 5% pada citra grayscale dan berwarna.
- Median filter berhasil mengurangi bintik-bintik noise secara signifikan.
- Pada citra berwarna, filtering diterapkan per kanal RGB dan hasil denoising tetap menjaga struktur objek lebih baik dibandingkan mean filter.

### Output
- Grayscale (1x3):
  - Original
  - Noisy (Salt & Pepper)
  - Median Filtered
- Color (1x3):
  - Original
  - Noisy (Salt & Pepper)
  - Median Filtered

### Kesimpulan
Median filter sangat efektif untuk noise salt-and-pepper karena mampu menghilangkan noise impuls tanpa mengaburkan tepi sekuat mean filter.

## Praktikum 5: Eksperimen Transformasi Intensitas (Gamma)
### Tujuan
Menganalisis pengaruh nilai gamma terhadap intensitas citra grayscale menggunakan transformasi gamma:
\[
I_{out} = I_{in}^{\gamma}
\]

### Hasil Praktikum
- Untuk `gamma = 2.0` pada citra `camera`, citra menjadi lebih gelap karena intensitas menengah-rendah ditekan.
- Untuk `gamma = 0.5` pada citra `astronaut` (yang sudah diubah ke grayscale), citra menjadi lebih terang karena intensitas rendah dinaikkan.
- Perubahan intensitas terjadi non-linear sehingga detail tertentu bisa lebih menonjol tergantung nilai gamma.

### Output
- Visualisasi 2x2:
  - Camera asli
  - Camera hasil gamma 2.0 (lebih gelap)
  - Astronaut grayscale asli
  - Astronaut hasil gamma 0.5 (lebih terang)

### Kesimpulan
Transformasi gamma efektif untuk kontrol kecerahan non-linear: `gamma > 1` cenderung menggelapkan citra, sedangkan `gamma < 1` cenderung mencerahkan citra.

## Praktikum 6: Perbandingan Metode Peningkatan Kontras
### Tujuan
Membandingkan dua metode peningkatan kontras pada citra low contrast, yaitu contrast stretching dan histogram equalization.

### Hasil Praktikum
- **Contrast stretching** dengan rentang persentil 2-98 memperluas distribusi intensitas tanpa terlalu dipengaruhi outlier.
- **Histogram equalization** meratakan histogram lebih agresif sehingga kontras global meningkat lebih kuat.
- Kedua metode sama-sama meningkatkan keterbacaan detail, dengan karakter hasil visual yang berbeda.

### Output
- Visualisasi 3x2:
  - Citra low contrast asli + histogram asli
  - Hasil contrast stretching + histogram stretching
  - Hasil histogram equalization + histogram equalization

### Kesimpulan
Contrast stretching cocok untuk peningkatan kontras yang lebih terkontrol, sementara histogram equalization cocok untuk peningkatan kontras global yang lebih kuat.

## Praktikum 7: Perbandingan Filter Median vs Mean
### Tujuan
Mengevaluasi kinerja mean filter dan median filter pada citra yang diberi noise salt-and-pepper.

### Hasil Praktikum
- Mean filter (kernel 3x3) mampu mengurangi noise, tetapi menghasilkan blur dan masih menyisakan artefak noise impuls.
- Median filter (disk radius 3) lebih efektif menghapus bintik salt-and-pepper sambil menjaga ketajaman tepi.
- Secara visual, median filter memberikan kompromi terbaik antara denoising dan preservasi struktur.

### Output
- Visualisasi 1x4:
  - Citra asli
  - Citra noisy (salt-and-pepper)
  - Hasil mean filter
  - Hasil median filter

### Kesimpulan
Untuk noise salt-and-pepper, median filter lebih unggul daripada mean filter karena mampu mereduksi noise impuls tanpa mengaburkan tepi secara berlebihan.

## Kesimpulan Umum Jobsheet 3
- Transformasi negatif mengubah representasi visual dengan inversi intensitas.
- Histogram membantu analisis distribusi intensitas, sedangkan ekualisasi histogram meningkatkan kontras.
- Mean filter cocok untuk smoothing sederhana namun mengurangi ketajaman.
- Median filter lebih unggul untuk menangani noise salt-and-pepper dengan mempertahankan tepi lebih baik.
- Transformasi gamma memberi kontrol pencahayaan non-linear yang fleksibel.
- Contrast stretching dan histogram equalization sama-sama meningkatkan kontras, tetapi dengan karakter hasil yang berbeda.
- Pada denoising noise impuls, median filter konsisten memberikan hasil paling baik secara visual.

Dengan demikian, pemilihan metode pengolahan citra harus disesuaikan dengan tujuan: peningkatan kontras, smoothing, atau denoising berbasis jenis noise.
