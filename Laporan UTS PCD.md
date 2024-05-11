UTS PCD

import cv2 //Merupakan sebuah pustaka yang digunakan untuk memanipulasi gambar//

import matplotlib.pyplot as plt // sebuah pustaka yang digunakan untuk menampilkan gambar//

import numpy as np //pustaka yang digunakan untuk komputasi numerik//

img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)//cara untuk membaca gambar dari file yang bersifat jpg ataupun jpeg menggunakan pustaka opencv agar gambarnya bisa dibaca//

biru = img[:, :, 0] //merupakan saluran khusus untuk warna biru//
hijau = img[:, :, 1] //merupakan saluran khusus untuk warna hijau//
merah = img[:, :, 2] //merupakan saluran khusus untuk warna merah//
//Coingan diatas sebagai pemisah gambar menjadi saluran warna dan  membantu dalam memahami dan menganalisis komposisi warna dalam gambar.//

plt.figure(figsize=(15, 5))

# Menampilkan gambar asli
plt.subplot(2, 2, 1)
plt.imshow(img)
plt.title('Citra Asli')
plt.axis('off')

#Menampilkan citra biru
plt.subplot(2, 2, 2)
plt.imshow(biru, cmap='gray')
plt.title('Blue Image')
plt.axis('off')

#Menampilkan citra hijau
plt.subplot(2, 2, 3)
plt.imshow(hijau, cmap='gray')
plt.title('Green color')
plt.axis('off')

#Menampilkan citra merah
plt.subplot(2, 2, 4)
plt.imshow(merah, cmap='gray')
plt.title('Red color')
plt.axis('off')

plt.tight_layout()
plt.show()
//Kode di atas bertujuan untuk menampilkan beberapa visualisasi gambar, termasuk gambar asli dan saluran warna utama (biru, hijau, merah) dari gambar tersebut. Menampilkan gambar asli bersama dengan saluran warna individual memungkinkan kita untuk memeriksa perbedaan intensitas dan distribusi warna di antara saluran tersebut.
Menggunakan skala abu-abu (grayscale) untuk menampilkan saluran warna individual memungkinkan kita untuk fokus pada informasi intensitas (kecerahan) dalam gambar, yang berguna dalam berbagai jenis analisis dan pemrosesan citra.//

fig, axs = plt.subplots(2,2, figsize=(20,5))
axs[0, 0].hist(img.ravel(),256,[0,256])
axs[0, 0].set_title('Histogram Citra Asli')

axs[0, 1].hist(biru.ravel(), 256, [0, 256], color='blue')
axs[0, 1].set_title('Histogram Warna Biru')

axs[1, 0].hist(hijau.ravel(), 256, [0, 256], color='green')
axs[1, 0].set_title('Histogram Warna Hijau')

axs[1, 1].hist(merah.ravel(), 256, [0, 256], color='red')
axs[1, 1].set_title('Histogram Warna Merah')
plt.show() //Kode di atas bertujuan untuk menampilkan histogram dari gambar asli dan histogram dari setiap saluran warna utama (biru, hijau, merah) dari gambar tersebut. Histogram adalah representasi grafis dari distribusi intensitas piksel di dalam gambar.
Histogram merupakan alat yang sangat berguna dalam analisis gambar karena memberikan informasi tentang distribusi intensitas piksel di dalam gambar.
Dengan menampilkan histogram dari gambar asli dan setiap saluran warna, kita dapat memahami lebih baik tentang komposisi dan distribusi warna dalam gambar.//

img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)//Mengonversi skema warna gambar dari BGR (Blue-Green-Red) ke RGB (Red-Green-Blue).//
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)//mengonversi skema warna gambar dari BGR ke HSV (Hue-Saturation-Value). Representasi warna HSV memungkinkan kita untuk dengan mudah menentukan rentang warna tertentu.//


# Definisikan rentang warna untuk biru, merah, dan hijau
biru_bawah = np.array([100, 43, 46])//nilai minimal rentang warna biru dalam ruang warna HSV. Angka-angka ini menunjukkan nilai Hue, Saturation, dan Value.//
biru_atas = np.array([130, 255, 255])//nilai maksimal rentang warna biru dalam ruang warna HSV. Angka-angka ini juga mewakili Hue, Saturation, dan Value.//

merah_bawah = np.array([100, 43, 46])
merah_atas = np.array([100, 255, 255])

hijau_bawah = np.array([36, 43, 46])
hijau_atas = np.array([75, 255, 255])


biru_mask = cv2.inRange(hsv, biru_bawah, biru_atas)
merah_mask = cv2.inRange(hsv, merah_bawah, merah_atas)
hijau_mask = cv2.inRange(hsv, hijau_bawah, hijau_atas)

# Temukan piksel yang cocok dengan setiap warna
biru_piksel = cv2.bitwise_and(img, img, mask=biru_mask)
merah_piksel = cv2.bitwise_and(img, img, mask=merah_mask)
hijau_piksel = cv2.bitwise_and(img, img, mask=hijau_mask)

plt.figure(figsize=(10, 5)) // membuat sebuah figur dengan ukuran 10x5 inci

# Gambar Asli
plt.subplot(2, 2, 1) // Membuat sebuah subplot dalam grid 2x2, di mana i adalah nomor subplot. 
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)) //Digunakan untuk menampilkan gambar
plt.title('Gambar Asli') //Memberikan judul
plt.axis('off') // Menghilangkan sumbu pada subplot

# Gambar Biru
plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(biru_piksel, cv2.COLOR_BGR2RGB))
plt.title('Biru')
plt.axis('off')

# Gambar Merah
plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(merah_piksel, cv2.COLOR_BGR2RGB))
plt.title('Merah')
plt.axis('off')

# Gambar Hijau
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(hijau_piksel, cv2.COLOR_BGR2RGB))
plt.title('Hijau')
plt.axis('off')

plt.tight_layout() // menyusun subplot dengan tata letak yang lebih baik secara otomatis, sehingga tidak ada tumpang tindih antara subplot.//
plt.show()
## Documentation

[Documentation](https://linktodocumentation)


## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [How to write a Good readme](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)

