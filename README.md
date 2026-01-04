# Sistem Pengenalan Motif Batik 🇮🇩
**PProjek Ujian Akhir Semester (UAS) Mata Kuliah: Pengolahan Citra Digital**

Projek ini merupakan sistem pengenalan motif batik secara real-time yang dibangun menggunakan pendekatan Computer Vision dan Machine Learning. Sistem dikembangkan sebagai bagian dari tugas Ujian Akhir Semester dan dikerjakan oleh satu kelompok yang terdiri dari lima mahasiswa.

---

## Anggota Kelompok
1. 231011403404  -  Aditya Alfianto
2. 231011400524  -  Nabil Radina
3. 231011403045  -  Raihan Fathir M.
4. 231011403152  -  Revaldi Ridwan
5. 231011400511  -  Sadam Sofyan

---

## Gambaran Umum Projek
Tujuan utama dari projek ini adalah mengidentifikasi dan mengklasifikasikan jenis motif batik, seperti Parang, Kawung, dan motif lainnya, berdasarkan citra kain batik. Sistem bekerja dengan mempelajari pola warna dan tekstur dari kumpulan data latih (dataset), kemudian mengubah karakteristik tersebut menjadi fitur numerik. Model yang telah dilatih selanjutnya digunakan untuk melakukan prediksi motif batik secara langsung melalui kamera (webcam).

### Metode Pengolahan Citra
Untuk memperoleh representasi fitur yang optimal, sistem mengombinasikan tiga teknik ekstraksi fitur utama, yaitu:

1. **Ekstraksi Fitur Warna**:
Metode ini bertujuan menangkap karakteristik warna khas pada motif batik, dengan cara:  

   - Mengekstraksi nilai **Mean** dan **Standard Deviation** pada ruang warna **BGR** dan **HSV**.
   - Menggunakan **Color Histogram** dengan 8 bin untuk menangkap distribusi intensitas warna pada setiap saluran.

2. **Ekstraksi Fitur Tekstur GLCM**:
   - Menganalisis hubungan spasial antar piksel pada aras keabuan (grayscale).
   - Parameter yang diambil meliputi: *Contrast, Dissimilarity, Homogeneity, Energy, Correlation,* dan *ASM*.

3. **Ekstraksi Fitur Tekstur LBP**:
Local Binary Pattern (LBP) digunakan untuk mendeskripsikan tekstur lokal yang relatif tahan terhadap perubahan pencahayaan. Metode ini sangat efektif dalam membedakan detail motif batik yang memiliki pola berulang dan kompleks.

### Metode Klasifikasi
Seluruh fitur hasil ekstraksi kemudian diproses menggunakan **Random Forest Classifier**. Algoritma ini dipilih karena mampu menangani data numerik hasil ekstraksi fitur dengan baik serta memberikan performa klasifikasi yang stabil dan akurat.

---

## Struktur Program
Projek ini terdiri dari dua modul utama yang saling terintegrasi:

* **`fiturbatik.py` (Ekstraksi Fitur)**: 
   Script ini digunakan untuk memproses seluruh gambar pada dataset *training* dan *testing*. Semua fitur warna dan tekstur (Color, GLCM, dan LBP) diekstraksi dan disimpan dalam bentuk file `.CSV` sebagai basis data untuk pelatihan model.


* **`runbatik.py` (Recognition & Training)**: 
    Script utama yang melatih model Random Forest menggunakan data CSV. Script ini mengaktifkan webcam dan menggunakan **Region of Interest (ROI)** berbentuk kotak di tengah layar untuk mendeteksi kain batik secara real-time.

---

## Alur Kerja Sistem
1. **Preprocessing**:
   - Citra dikonversi ke grayscale untuk analisis tekstur
   - Citra diubah ke ruang warna HSV untuk analisis warna

2. **Ekstraksi Fitur**: 
   - Sistem menghitung fitur matematis dari warna dan tekstur batik

3. **Training Model**: 
   - Model mempelajari pola motif batik berdasarkan data fitur dalam file CSV

4. **Real-time Detection**: 
   - Kamera menangkap citra batik
   - Fitur diekstraksi secara instan
   - Sistem menampilkan label motif batik dan tingkat kepercayaan prediksi pada layar
