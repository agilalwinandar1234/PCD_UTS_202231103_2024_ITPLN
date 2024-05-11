  # PCD_UTS_202231103_2024_ITPLN
  # import library
```  
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
*cv2 (OpenCV) adalah pustaka utama untuk pengolahan citra dan penglihatan komputer. 
*matplotlib.pyplot (matplotlib) adalah modul dalam matplotlib yang digunakan untuk membuat plot grafik 2D. 
*numpy (np) adalah pustaka Python yang sangat populer untuk komputasi numerik. Numpy  sangat berguna ketika bekerja dengan data citra karena citra sering direpresentasikan sebagai array numerik. dengan menggunakan numpy, kita dapat dengan mudah melakukan operasi seperti pengolahan piksel, perhitungan statistik, dan transformasi matematika lainnya pada citra.
```
img = cv2.imread("agilalwinandar.jpg")
```
* cv2.imread() untuk membaca gambar dengan nama file "agilalwinandar.jpg" dan menyimpannya dalam variabel img. fungsi ini akan membaca gambar dari file dan mengembalikan array NumPy yang mewakili citra.
```
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
* cv2.cvtColor() perintah untuk mengubah ruang warna citra dari BGR  ke RGB. hal ini sering dilakukan karena format warna standar dalam Python adalah RGB, sedangkan OpenCV secara default menggunakan BGR.
```
plt.imshow(rgb)
```
* plt.imshow() untuk menampilkan citra yang telah kita baca dan ubah warnanya ke format RGB menggunakan OpenCV. ini adalah cara yang tepat untuk menampilkan citra dalam Matplotlib.
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
* cv2.cvtColor() lagi, tapi untuk mengubah citra asli menjadi citra skala keabuan 
grayscale dengan menggunakan flag cv2.COLOR_BGR2GRAY. Citra skala keabuan hanya memiliki satu saluran warna, sehingga lebih efisien secara komputasi dibandingkan dengan citra berwarna.
```
alpha = 1.5 # kontras
beta = 30   # kecerahan
adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta)
```
* cv2.convertScaleAbs() untuk menyesuaikan kontras dan kecerahan citra. Dalam fungsi ini kita dapat mengatur faktor kontras dengan parameter alpha dan nilai kecerahan dengan parameter beta. Hasilnya akan disimpan dalam variabel adjusted.
  
```
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.title('Original Image')
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.subplot(1, 2, 2)
plt.title('Brightened Image')
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.show()
```
*plt.figure(figsize=(10, 5)) membuat sebuah gambar baru (figure) dengan ukuran 10x5 inci. kita memberikan ukuran ini menggunakan parameter figsize yang menerima nilai lebar dan tinggi dalam inci.
*plt.subplot(1, 2, 1) mendefinisikan subplot pertama di dalam gambar yang kita buat. Subplot ini memiliki 1 baris, 2 kolom, dan merupakan subplot pertama. Dengan kata lain, kita memiliki dua subplot sejajar, dan yang pertama adalah yang sedang kita definisikan.
*plt.title('Original Image') menambahkan judul "Original Image" pada subplot pertama.
*plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)) menampilkan citra asli dalam subplot pertama. Fungsi cv2.cvtColor() digunakan untuk mengonversi citra dari format BGR (yang digunakan oleh OpenCV) menjadi RGB (yang diharapkan oleh Matplotlib).
*plt.axis('off') mematikan sumbu x dan y pada subplot pertama, sehingga tidak ada garis sumbu yang ditampilkan.
*plt.subplot(1, 2, 2) mendefinisikan subplot kedua di dalam gambar yang kita buat. Subplot ini memiliki 1 baris, 2 kolom, dan merupakan subplot kedua.
*plt.title('Brightened Image') menambahkan judul "Brightened Image" pada subplot kedua.
*plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)) menampilkan citra yang telah disesuaikan (dalam hal ini, citra yang ditingkatkan kecerahan dan kontras) di subplot kedua. Seperti sebelumnya, kita menggunakan cv2.cvtColor() untuk mengonversi citra ke format RGB.
*plt.axis('off') mematikan sumbu x dan y pada subplot kedua, sehingga tidak ada garis sumbu yang ditampilkan.
*plt.show() menampilkan keseluruhan gambar (figure) yang telah kita definisikan dengan dua subplot di layar.

```
plt.subplot(2, 1, 1)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.title('Original Image')

# Display the red channel
plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray")
plt.title('Red')

# Display the green channel
plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1], cmap="gray")
plt.title('Green')

# Display the blue channel
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2], cmap="gray")
plt.title('Blue')

plt.show()
```
*Kodingan di atas kita membuat subplot yang menampilkan citra asli di bagian atas kiri dan kemudian menampilkan saluran warna (merah, hijau, dan biru) sebagai subplot tambahan di bawahnya. Setiap subplot menampilkan satu saluran warna dari citra yang disesuaikan. kita menggunakan indeksing pada array citra untuk mengambil saluran warna tertentu dan menampilkannya menggunakan plt.imshow(). kita juga menambahkan judul untuk masing-masing subplot.
```
merah=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0] #merah
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([merah],[0],None,[256],[0,256])
axs[0].imshow(merah, cmap='gray')
axs[1].plot(hist)
plt.show()
```
* cv2.calcHist() untuk menghitung histogram dari saluran warna merah ([0] menunjukkan saluran ke-0). fungsi ini menghasilkan histogram, yang kemudian kita plot menggunakan plt.plot(). kita juga menampilkan citra saluran warna merah itu sendiri di subplot pertama.
```
hijau=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1] #hijau
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([hijau],[0],None,[256],[0,256])
axs[0].imshow(hijau, cmap='gray')
axs[1].plot(hist)
plt.show()
```
* cv2.calcHist() untuk menghitung histogram dari saluran warna hijau ([1] menunjukkan saluran ke-1). Kemudian kita menampilkan citra saluran warna hijau di subplot pertama dan histogram di subplot kedua. ini cara yang baik untuk memahami distribusi intensitas piksel dalam saluran warna hijau dari citra kita.
```
biru=cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2] #biru
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([biru],[0],None,[256],[0,256])
axs[0].imshow(biru, cmap='gray')
axs[1].plot(hist)
plt.show()
```
* cv2.calcHist() untuk menghitung histogram dari saluran warna biru ([2] menunjukkan saluran ke-2). Setelah itu kita menampilkan citra saluran warna biru di subplot pertama dan histogram di subplot kedua.

# 2
```
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
*cv2 (OpenCV) adalah pustaka utama untuk pengolahan citra dan penglihatan komputer. 
*matplotlib.pyplot (matplotlib) adalah modul dalam matplotlib yang digunakan untuk membuat plot grafik 2D. 
*numpy (np) adalah pustaka Python yang sangat populer untuk komputasi numerik. Numpy  sangat berguna ketika bekerja dengan data citra karena citra sering direpresentasikan sebagai array numerik. dengan menggunakan numpy, kita dapat dengan mudah melakukan operasi seperti pengolahan piksel, perhitungan statistik, dan transformasi matematika lainnya pada citra.
```
img = cv2.imread('agilalwinandar.jpg')
```
* cv2.imread() untuk membaca gambar dengan nama file "agilalwinandar.jpg" dan menyimpannya dalam variabel img. 
```
# Convert citra ke grayscale
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

# Inisialisasi subplot
fig, axs = plt.subplots(2, 2, figsize=(10,10))

# Ambang batas untuk mendapatkan citra biner (none)
(thresh, binary1) = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

# Convert citra ke HSV
image_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Definisikan range warna biru dalam HSV
blue_lower = np.array([100, 50, 50])
blue_upper = np.array([140, 255, 255])

# Membuat mask untuk warna biru
mask_blue = cv2.inRange(image_hsv, blue_lower, blue_upper)
axs[0,1].imshow(mask_blue, cmap='gray')
axs[0,1].set_title('BLUE')

# Ambang batas untuk mendapatkan citra biner (red-blue)
(thresh, binary3) = cv2.threshold(gray, 43, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')

# Ambang batas untuk mendapatkan citra biner (red-green-blue)
(thresh, binary4) = cv2.threshold(gray, 80, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')

plt.show()
```
*Convert citra ke grayscale saya menggunakan cv2.cvtColor() untuk mengonversi citra dari warna BGR menjadi skala keabuan grayscale dengan menggunakan cv2.COLOR_RGB2GRAY. hasilnya disimpan dalam variabel gray.
*Inisialisasi subplot saya menggunakan plt.subplots() untuk membuat gambar subplot dengan ukuran 2x2 (4 subplot) dengan ukuran total 10x10 inci. inimembuat grid 2x2 dari subplot.
*Ambang batas untuk mendapatkan citra biner (none) saya menggunakan cv2.threshold() untuk menerapkan ambang batas ke citra grayscale. dalam kasus ini, kita menggunakan nilai ambang 0, yang berarti semua piksel dengan intensitas di atas 0 akan diubah menjadi 255 (putih), dan yang di bawahnya akan menjadi 0 (hitam). Hasilnya disimpan dalam variabel binary1.
*Convert citra ke HSV saya menggunakan cv2.cvtColor() lagi untuk mengonversi citra asli dari format BGR ke ruang warna HSV.
*Definisikan range warna biru dalam HSV saya menentukan rentang nilai HSV yang sesuai dengan warna biru.
*Membuat mask untuk warna biru saya menggunakan cv2.inRange() untuk membuat mask dari citra HSV, yang akan menghasilkan citra biner dengan nilai 255 (putih) di mana warna dalam rentang biru dan 0 (hitam) di luar rentang.
*Ambang batas untuk mendapatkan citra biner (red-blue) saya menggunakan cv2.threshold() lagi untuk menerapkan ambang batas ke citra grayscale. Kali ini saya menggunakan nilai ambang 43. ini mungkin sesuai dengan nilai ambang tertentu yang menghasilkan citra biner yang memisahkan warna merah dan biru.
*Ambang batas untuk mendapatkan citra biner (red-green-blue) saya menggunakan cv2.threshold() sekali lagi untuk menerapkan ambang batas ke citra grayscale. Kali ini saya menggunakan nilai ambang 80. ini mungkin sesuai dengan nilai ambang tertentu yang menghasilkan citra biner yang memisahkan warna merah, hijau, dan biru.
*Menampilkan plot saya menggunakan plt.show() untuk menampilkan keseluruhan gambar subplot. 
