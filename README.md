# PA-01_202231003_Farrel-Alfared-C_A
<br>
<br>
Nama : Farrel Alfared Carasiola<br>
NIM : 202231003<br>
Kelas : Pengolahan Citra Digital - A<br>
Ketentuan Projek : Deteksi Tepi Pola Objek<br>

---

## Pendahuluan
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pengolahan citra digital adalah proses di mana gambar digital dianalisis dan dimodifikasi menggunakan algoritma komputer. Tujuan dari pengolahan citra adalah untuk meningkatkan kualitas gambar, mengekstrak informasi, atau melakukan tugas-tugas tertentu seperti deteksi tepi, segmentasi objek, dan identifikasi pola. <br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Deteksi tepi adalah teknik dalam pengolahan citra yang digunakan untuk menemukan batas atau tepi objek dalam gambar. Salah satu algoritma deteksi tepi yang paling populer adalah Canny Edge Detection, yang dikembangkan oleh John F. Canny pada tahun 1986.<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Deteksi Kontur (Contours Detection)
Kontur adalah kurva yang menghubungkan semua titik kontinu yang memiliki warna atau intensitas yang sama. Deteksi kontur adalah teknik penting dalam pengenalan objek dan analisis bentuk. Dalam OpenCV, fungsi findContours digunakan untuk mendeteksi kontur dalam gambar biner, yang seringkali merupakan hasil dari deteksi tepi.<br>
## Tahapan dalam Menyelesaikan Deteksi Tepi Pola Objek
- Memuat citra dengan library OpenCV<br>
- Mengambil gambar/citra<br>
- Mendeteksi citra tepi dengan Canny Edge Detection<br>
- Mendeteksi kontur<br>
- Menggabungkan hasil citra dalam satu gambar<br>

---
Berikut adalah tahapan cara menyelesaikan projek secara rinci:
### - Memuat citra dengan library OpenCV
```
import cv2
import numpy as np
from matplotlib import pyplot as plt
```
> Penjelasan:
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kode di atas mengimpor tiga pustaka penting yang sering digunakan dalam pemrosesan citra dan visualisasi data. Pertama, `import cv2` mengimpor library OpenCV, adalah sebuah pustaka open-source untuk pemrosesan gambar dan video. Kedua, `import numpy as np` mengimpor pustaka NumPy, yang menyediakan dukungan untuk array multidimensi.<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NumPy sangat berguna saat pemrosesan citra karena gambar dapat direpresentasikan sebagai array multidimensi. Terakhir, `from matplotlib import pyplot as plt` adalah mengimpor modul pyplot dari pustaka Matplotlib, yang digunakan untuk membuat visualisasi data dalam bentuk grafik dan plot.

### - Mengambil gambar/citra
```
image = cv2.imread('mypic.jpg')
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
> Penjelasan:
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kode di atas pertama-tama membaca gambar yang disimpan dalam berkas bernama 'mypic.jpg' menggunakan fungsi `cv2.imread` dari pustaka OpenCV. Fungsi ini mengembalikan gambar dalam format BGR (Blue-Green-Red), yang merupakan format warna default yang digunakan oleh OpenCV.<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Setelah gambar berhasil dibaca, kode tersebut mengonversi gambar dari format BGR ke format RGB (Red-Green-Blue) menggunakan fungsi `cv2.cvtColor` dengan parameter `cv2.COLOR_BGR2RGB`. Hasil dari konversi ini adalah gambar yang sama dalam format warna RGB, yang disimpan dalam variabel `image_rgb`.

### - Mendeteksi citra tepi dengan Canny <br>
```
edges = cv2.Canny(image, 100, 200)
```
> Penjelasan:
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fungsi `cv2.Canny` digunakan untuk mendeteksi tepi (edges) dalam citra kita. Variabel `edges` menyimpan hasil dari operasi deteksi tepi pada citra yang diberikan, dengan menggunakan metode Canny. Metode ini butuh tiga parameter utama, yaitu citra input (`image`), nilai ambang batas bawah (100), dan nilai ambang batas atas (200). <br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nilai ambang batas ini digunakan untuk mengidentifikasi intensitas gradien yang menunjukkan adanya tepi. Titik-titik dengan intensitas gradien di bawah 100 akan diabaikan, sementara titik-titik dengan intensitas gradien di atas 200 akan dianggap sebagai tepi. Hasilnya adalah citra biner yang menunjukkan lokasi-lokasi tepi pada citra asli.

### - Mendeteksi kontur
```
contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
image_contours = image_rgb.copy()
cv2.drawContours(image_contours, contours, -1, (0, 255, 0), 2)
```
> Penjelasan:
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kode di atas digunakan untuk mendeteksi dan menggambar kontur pada gambar. Pertama, fungsi `cv2.findContours` dari pustaka OpenCV digunakan untuk menemukan kontur pada gambar tepi yang sudah diekstraksi sebelumnya yaitu (`edges`). Fungsi ini mengembalikan dua nilai, yaitu kontur yang ditemukan dan informasi hierarki.<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Metode `cv2.RETR_TREE` digunakan untuk mengambil semua kontur dan membentuk pohon hierarki penuh, sedangkan `cv2.CHAIN_APPROX_SIMPLE` digunakan untuk menghemat memori dengan menghapus semua titik redundansi dan hanya menyimpan titik-titik penting untuk menggambar kontur. Selanjutnya, salinan dari gambar asli dalam format RGB (`image_rgb`) dibuat dengan nama `image_contours`.<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Terakhir, fungsi `cv2.drawContours` digunakan untuk menggambar semua kontur yang ditemukan pada salinan gambar tersebut dengan warna hijau (dinyatakan sebagai `(0, 255, 0)` dalam format BGR) dan dengan ketebalan garis sebesar 2 piksel. Lalu, hasil akhirnya adalah gambar dengan semua kontur yang ditemukan ditampilkan dengan jelas.

**Hasil dari gabungan kode di bawah ini akan menghasilkan array multidimensi<br>**
```
image = cv2.imread('mypic.jpg')
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

edges = cv2.Canny(image, 100, 200)

contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
image_contours = image_rgb.copy()
cv2.drawContours(image_contours, contours, -1, (0, 255, 0), 2)
```
```
Hasil:
array([[[150, 151, 120],
        [148, 149, 118],
        [145, 146, 115],
        ...,
        [149, 151, 130],
        [149, 151, 130],
        [149, 151, 130]],
       [[152, 153, 122],
        [150, 151, 120],
        [147, 148, 117],
        ...,
        [149, 151, 130],
        [149, 151, 130],
        [149, 151, 130]],
       [[155, 155, 127],
        [153, 153, 125],
        [151, 151, 123],
        ...,
        [149, 151, 130],
        [149, 151, 130],
        [149, 151, 130]],
       ...,
       [[212, 214, 201],
        [213, 215, 202],
        [214, 216, 203],
        ...,
        [141, 150, 133],
        [141, 150, 133],
        [141, 150, 133]],
       [[215, 217, 204],
        [216, 218, 205],
        [217, 219, 206],
        ...,
        [141, 150, 133],
        [141, 150, 133],
        [141, 150, 133]],
       [[218, 220, 207],
        [219, 221, 208],
        [219, 221, 208],
        ...,
        [141, 150, 133],
        [141, 150, 133],
        [141, 150, 133]]], dtype=uint8)
```
- Hasil akhirnya adalah gambar dengan kontur-kontur yang terdeteksi digambarkan di atas gambar asli yang telah dikonversi ke format RGB. Hasil gambar ini disimpan dalam array dengan tipe data uint8, yang merepresentasikan nilai-nilai piksel dalam format RGB. 
        
### - Menggabungkan hasil citra dalam satu gambar (Output 1)
```
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(image_rgb)
plt.title('Original Image')
plt.axis('on')

plt.subplot(1, 2, 2)
plt.imshow(edges, cmap='gray')
plt.title('Canny Edge Detection')
plt.axis('on')

plt.show()
```
> Penjelasan:
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kode di atas menggunakan matplotlib untuk membuat gambar subplot dengan total 1 baris dan 2 kolom. Subplot pertama (subplot 1, 2, 1), gambar asli (image_rgb) ditampilkan menggunakan plt.imshow() dengan nama "Original Image" (plt.title('Original Image')). Di subplot kedua (subplot 1, 2, 2), hasil deteksi tepi menggunakan Canny (edges) ditampilkan dalam skala abu-abu (cmap='gray') dengan judul "Canny Edge Detection" (plt.title('Canny Edge Detection')).<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hasil output dari kode ini adalah jendela gambar (plt.show()) yang menampilkan kedua subplot secara bersamaan. Subplot pertama menampilkan gambar asli dalam warna, sementara subplot kedua menampilkan gambar yang telah diproses dengan deteksi tepi Canny dalam skala abu-abu. Ini memungkinkan perbandingan visual antara gambar asli dan hasil deteksi tepi, membantu dalam analisis visual dan pemrosesan gambar. Kedua gambar berikut juga akan menampilkan sumbu koordinat dari x dan y menggunakan plt.axis('on').<br>

**Output 1:**
![alt text](https://github.com/farrelac/PA-01_202231003_Farrel-Alfared-C_A/blob/main/hasil_output/original-canny_edge_detection.png?raw=true)

### - Menggabungkan hasil citra dalam satu gambar (Output 2)
```
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(image_rgb)
plt.title('Original Image')
plt.axis('on')

plt.subplot(1, 3, 2)
plt.imshow(edges, cmap='gray')
plt.title('Canny Edge Detection')
plt.axis('on')

plt.subplot(1, 3, 3)
plt.imshow(image_contours)
plt.title('Contours Detection')
plt.axis('on')

plt.show()
```
> Penjelasan:
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sama halnya dengan sebelumnya, kode di atas menggunakan `matplotlib` untuk membuat sebuah gambar yang terdiri dari tiga subplot berdampingan secara horizontal di satu baris. Gambar pertama menampilkan citra asli dalam mode warna RGB dengan nama "Original Image". Gambar kedua menampilkan hasil deteksi tepi menggunakan metode Canny dalam skala abu-abu (grayscale) dengan nama "Canny Edge Detection". Gambar ketiga menampilkan citra hasil deteksi kontur objek dalam citra dengan judul "Contours Detection".<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Setiap subplot ditampilkan dengan sumbu (axis) yang aktif dan keseluruhan gambar ditampilkan dengan ukuran figur yang lebarnya (15 inch lebar x 5 inch tinggi). Hasil outputnya adalah tiga gambar berdampingan untuk mempermudah analisis visual terhadap perubahan yang terjadi pada citra setelah pemrosesan.<br>

**Output 2:**
![alt text](https://github.com/farrelac/PA-01_202231003_Farrel-Alfared-C_A/blob/main/hasil_output/original-canny_edge_detection-contours_detection.png?raw=true)

---

## Teori yang Mendukung :


