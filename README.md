# Laporan Proyek Machine Learning -  Adinda Chandra Ayu Kusumawardhana

## Project Overview
![Film](https://github.com/user-attachments/assets/8d88be1f-b881-41c3-a158-3accf4041b41)

## Project Overview: Film Recommendation System

### Tujuan

Membangun sebuah **sistem rekomendasi film berbasis konten (content-based filtering)** yang dapat menyarankan film serupa berdasarkan data metadata seperti genre, skor, dan sinopsis. Sistem ini diimplementasikan menggunakan Python dan dieksekusi melalui Google Colab.

---

### Dataset

Dataset diambil dari Kaggle:
📦 **"Movies Updated Data"** oleh [Ashish Kumar Jayswal](https://www.kaggle.com/datasets/ashishkumarjayswal/movies-updated-data)
File utama: `movies_updated.csv`

Isi dataset:

* 25 kolom seperti: `Name`, `Genre`, `Score`, `Director`, `Votes`, `Budget`, `Gross`, `Runtime`, dll.
* Fokus utama hanya pada kolom: `Name`, `Score`, `Genre`, `Company`, `Star`.

---

### Langkah-Langkah Proyek

1. **Inisialisasi & Setup**

   * Menghubungkan Google Drive dan menyiapkan API Kaggle untuk mengunduh dataset.
   * Melakukan unzip dan membaca file `.csv` dengan Pandas.

2. **Data Understanding**

   * Menampilkan statistik dasar: jumlah data, informasi kolom, tipe data.
   * Mengecek missing values dan struktur konten data.

3. **Preprocessing**

   * Membersihkan teks dan menggabungkan beberapa fitur deskriptif untuk dijadikan input.
   * Menggabungkan kolom seperti `Genre`, `Star`, `Company`, dan `Director` menjadi satu string sebagai basis pencocokan konten.

4. **Ekstraksi Fitur**

   * Menggunakan **TF-IDF Vectorizer** untuk mengubah teks menjadi vektor numerik.
   * Menerapkan **Cosine Similarity** untuk mengukur kemiripan antar film.

5. **Sistem Rekomendasi**

   * Implementasi fungsi untuk merekomendasikan 10 film berdasarkan film input pengguna.

6. **Evaluasi (Opsional)**

   * Terdapat library untuk evaluasi clustering seperti:

     * `calinski_harabasz_score`
     * `davies_bouldin_score`
   * Namun, tidak terlihat adanya analisis evaluasi model secara eksplisit dalam output awal.

---

### Algoritma dan Teknologi

* **TF-IDF (Term Frequency-Inverse Document Frequency)**: Teknik representasi teks untuk mengukur pentingnya kata dalam dokumen.
* **Cosine Similarity**: Metode pengukuran kemiripan antar dua vektor dalam ruang multidimensi.
* **Nearest Neighbors** (sklearn): Siap digunakan untuk pendekatan KNN atau pengelompokan alternatif.
* **Matplotlib & Seaborn**: Visualisasi data.

---

### Referensi Jurnal dan Teori

1. **Content-Based Recommendation**

   * Lops, P., de Gemmis, M., & Semeraro, G. (2011). *Content-based recommender systems: State of the art and trends*. In Recommender Systems Handbook.
     [https://doi.org/10.1007/978-0-387-85820-3\_3](https://doi.org/10.1007/978-0-387-85820-3_3)

2. **TF-IDF and Text Similarity**

   * Ramos, J. (2003). *Using TF-IDF to determine word relevance in document queries*.
     Proceedings of the First Instructional Conference on Machine Learning.

3. **Recommender System Overview**

   * Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems: Introduction and Challenges*. In Recommender Systems Handbook.

---

### 📌 Catatan Tambahan

* Proyek ini cocok sebagai studi kasus awal dalam bidang **Rekomendasi Berbasis Konten**.
* Dapat dikembangkan ke sistem **Hybrid** dengan Collaborative Filtering di masa depan.
* Perluasan dengan evaluasi metrik seperti precision\@k dan recall\@k bisa menjadi langkah lanjutan.

---


## Business Understanding
Sistem rekomendasi film berpotensi memberikan berbagai manfaat signifikan, baik bagi penonton maupun penyedia layanan streaming. Bagi pengguna, sistem ini mempermudah dalam menemukan film yang sesuai dengan minat secara lebih praktis dan efektif. Sementara itu, bagi platform streaming, sistem ini dapat meningkatkan interaksi pengguna, memperkuat loyalitas penonton, serta membantu operasional platform menjadi lebih efisien dan responsif terhadap kebutuhan pengguna.[[5](http://repository.uin-malang.ac.id/18842/1/18842.pdf)]

## Problem Statements
- Bagaimana membangun sistem rekomendasi film yang menyarankan tontonan kepada pengguna dengan mengacu pada genre yang diminati?
- Bagaimana penyedia layanan streaming dapat menyarankan film yang belum pernah ditonton oleh pengguna dengan memanfaatkan data penilaian yang telah diberikan?
- Bagaimana membangun model rekomendasi menggunakan pendekatan Cosine Similarity dan algoritma K-Nearest Neighbor?
- Bagaimana mengevaluasi kinerja dari model sistem rekomendasi yang sudah dikembangkan?

## Goals
Untuk menangani permasalahan tersebut, dirancanglah sebuah sistem rekomendasi dengan tujuan sebagai berikut :
- Menyajikan daftar Top-N rekomendasi film kepada pengguna berdasarkan genre yang diminati.
- Memberikan sejumlah rekomendasi film yang relevan dengan minat pengguna dan belum pernah ditonton sebelumnya.
- Mengembangkan model sistem rekomendasi menggunakan pendekatan Cosine Similarity dan K-Nearest Neighbor berdasarkan fitur yang telah diekstraksi dari dataset.
- Mengevaluasi kinerja model sistem rekomendasi dengan menerapkan metrik pengukuran yang sesuai

Solution Approach
Data dianalisis melalui proses ***Exploratory Data Analysis (EDA)*** dan ***divisualisasikan*** untuk memahami pola serta karakteristik yang ada. Untuk memperoleh model prediksi yang optimal, dilakukan ***pembersihan data***, seperti menghapus ***nilai yang hilang*** (missing value), memeriksa keberadaan ***data duplikat***, menghapus karakter ***alfanumerik*** yang tidak relevan, serta menghilangkan ***tautan*** (URL). Selanjutnya, data ***kategorikal dikonversi menjadi format numerik*** menggunakan metode ***one-hot encoding***. Guna menilai performa model yang dibangun, digunakan metrik evaluasi seperti ***Precision***, ***Score Calinski-Harabasz***, dan ***Skor Davies-Bouldin***.

## Data Understanding
EDA - Penjelasan Setiap Variabel

| Jenis    | Keterangan                                                |
|----------|-----------------------------------------------------------|
| Title    | Movies Dataset Visualization                                        |
| Source   |[Kaggle](https://www.kaggle.com/datasets/ashishkumarjayswal/movies-updated-data)  |
| Maintainer | [ashishkumarjayswal](https://www.kaggle.com/ashishkumarjayswal)                           |
| License  | Database: Open Database, Contents: Database Contents      |
| Visibility | Publik                                                  |
| Tags     | Movies and TV Shows |
| Usability | 7.06                                                     | 

Dataset ini tersedia secara publik di Kaggle dengan nama [movies-updated-data](https://www.kaggle.com/datasets/ashishkumarjayswal/movies-updated-data), dan dapat diakses serta diunduh langsung melalui situs [Kaggle](https://www.kaggle.com/).

Informasi yang terdapat dataset : 
- Datasets berupa file csv (Comma-Seperated Values).
- Dataset berupa 1 buah file CSV yaitu :
  - movies_updated.csv
 
Pada model yang saya buat kali ini dataset yang dipakai memiliki spesifikasi seperti di bawah ini:
- Dataset ini terdiri dari 4000 entri dan mencakup 15 atribut.
- Dari total fitur tersebut, terdapat 10 fitur bertipe objek, 3 fitur bertipe int64, serta 2 fitur bertipe float64.
- Ditemukan missing value pada kolom gross sebanyak 169 data, pada kolom rating sebanyak 40 data, 10 data pada kolom company, 1 data pada kolom writer dan juga kolom star.
- Tidak ditemukan adanya data duplikat dalam dataset ini.

| Kolom        | Tipe Data        | Deskripsi                                                                                     | Cara Pakai di Model                                                                                      |
| ------------ | ---------------- | --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **name**     | `object`         | Judul film.                                                                                   | Sebagai label/ID unik; bisa juga digunakan untuk menampilkan hasil rekomendasi.                          |
| **rating**   | `float`/`object` | Rating MPAA (misal “PG-13”, “R”, “G”).                                                        | Fitur kategorikal: mengelompokkan konten sesuai batas usia.                                              |
| **genre**    | `object`         | Kategori/jenis film (misal “Action”, “Comedy”, “Drama”). Bisa berisi beberapa genre per film. | Fitur multi-label: bisa di-encode dengan one-hot atau embedding genre.                                   |
| **year**     | `int`            | Tahun produksi film.                                                                          | Fitur numerik: mengukur umur film, tren preferensi berdasarkan era.                                      |
| **released** | `object`         | Tanggal rilis (misal “July 16, 2010”).                                                        | Bisa di-parse jadi tanggal (`datetime`) untuk ekstrak bulan, kuartal, hari dalam seminggu, dll.          |
| **score**    | `float`          | Skor rata-rata pengguna (misal IMDb score).                                                   | Fitur numerik: merepresentasikan popularitas/penilaian umum film.                                        |
| **votes**    | `int`            | Jumlah suara atau ulasan pengguna.                                                            | Fitur numerik: proxy untuk seberapa banyak orang yang menilai—indikator popularitas.                     |
| **director** | `object`         | Nama sutradara.                                                                               | Fitur kategorikal: di-encode (label/one-hot/embedding). Sutradara populer bisa meningkatkan rekomendasi. |
| **writer**   | `object`         | Nama penulis skenario.                                                                        | Serupa `director`: fitur kategorikal untuk menangkap gaya penulisan.                                     |
| **star**     | `object`         | Nama aktor/aktris utama.                                                                      | Fitur kategorikal penting—aktor favorit pengguna dapat memengaruhi rekomendasi.                          |
| **country**  | `object`         | Negara produksi film.                                                                         | Fitur kategorikal: mengelompokkan selera berdasarkan wilayah.                                            |
| **budget**   | `float`/`int`    | Anggaran pembuatan film (dalam USD).                                                          | Fitur numerik: film ber-anggaran besar cenderung produksi lebih “berkelas” dan populer.                  |
| **gross**    | `float`/`int`    | Pendapatan box-office (dalam USD).                                                            | Fitur numerik: proxy keberhasilan komersial—sering dikaitkan dengan popularitas massal.                  |
| **company**  | `object`         | Rumah produksi atau studio (misal “Warner Bros.”).                                            | Fitur kategorikal: studio besar biasanya memproduksi film dengan kualitas/genre tertentu.                |

![gambar1](https://github.com/user-attachments/assets/87fe85b6-b4c3-4c7f-b0f4-1d0abbfb68fb)

Gambar 1.Rating/Skor

![gambar2](https://github.com/user-attachments/assets/8759ec24-6c23-4223-8334-3a97acd753dc)

Gambar 2. Distribusi Company (perusahaan)

Gambar di atas menunjukkan **diagram pie distribusi perusahaan produksi film** yang terdapat dalam dataset. Terlihat bahwa mayoritas film (sekitar **77,87%**) diproduksi oleh perusahaan yang termasuk dalam kategori **"Other"**, yaitu perusahaan-perusahaan yang masing-masing memiliki proporsi kecil dan tidak termasuk dalam lima besar. Adapun lima perusahaan produksi film terbesar dalam data ini adalah:

* **Universal Pictures** dan **Paramount Pictures** masing-masing menyumbang **5,01%** dari total film,
* **Columbia Pictures** sebanyak **4,58%**,
* **Warner Bros.** sebanyak **4,30%**, dan
* **Twentieth Century Fox** sebanyak **3,24%**.

Hal ini mengindikasikan bahwa industri film dalam dataset bersifat sangat **terdesentralisasi**, di mana sebagian besar film diproduksi oleh banyak perusahaan kecil yang tersebar, bukan hanya oleh studio-studio besar Hollywood. Analisis seperti ini penting untuk memahami dominasi dan keragaman dalam industri film.


![gambar3](https://github.com/user-attachments/assets/038926b0-f8f2-4e71-93fa-d98a73becaae)

Gambar 3. Top 15 Vote Terbanyak

![gambar4](https://github.com/user-attachments/assets/34845eba-f792-43ce-930b-c1c8079ad883)

Gambar 4. Top 15 Film dengan Skor Tertinggi 

Gambar di atas menampilkan visualisasi **15 film dengan skor tertinggi** berdasarkan data penilaian pengguna atau rating. Visualisasi ini menggunakan **diagram batang horizontal**, yang memudahkan pembaca untuk membandingkan skor masing-masing film secara langsung. Setiap batang mewakili satu judul film, dengan panjang batang menunjukkan seberapa tinggi skor yang diperoleh film tersebut. Judul-judul film ditampilkan di sumbu vertikal, sementara skor ditampilkan secara horizontal pada sumbu x.

Dari visualisasi ini, film **"The Shawshank Redemption"** terlihat menduduki posisi teratas dengan skor tertinggi di antara semua film dalam daftar. Film ini memang sering dianggap sebagai salah satu film terbaik sepanjang masa, yang menegaskan validitas data yang digunakan. Diikuti oleh film-film lain yang juga sangat populer dan diakui secara kritis, seperti *Schindler's List*, *Pulp Fiction*, *Forrest Gump*, dan *The Lord of the Rings: The Fellowship of the Ring*.

Menariknya, film-film yang muncul dalam daftar ini sebagian besar merupakan karya dari dekade 1990-an dan awal 2000-an, periode yang dianggap sebagai era keemasan perfilman modern. Beberapa film seperti *Spirited Away* juga menunjukkan bahwa animasi dari Jepang mampu bersaing di panggung internasional dengan skor tinggi. Film *Life Is Beautiful*, yang berasal dari Italia, juga menunjukkan bahwa karya non-Hollywood mampu mendapatkan pengakuan luas.

Secara keseluruhan, grafik ini menunjukkan kecenderungan preferensi penonton terhadap film-film dengan tema kuat, penceritaan mendalam, dan kualitas sinematik yang tinggi. Analisis seperti ini bisa sangat bermanfaat dalam pembuatan sistem rekomendasi film, karena memperlihatkan pola-pola yang disukai oleh audiens global.

## Data Preparation
Pada tahap Data Preparation, dilakukan text cleaning untuk membersihkan teks dari tanda baca dan tautan (URL). Untuk menangani missing value, digunakan metode dropping dengan fungsi drop(). Alasan penggunaan metode ini adalah karena data yang dihapus tidak memberikan pengaruh signifikan terhadap performa model. Awalnya, dataset berjumlah 4000 entri, dan setelah menghapus data yang memiliki missing value, jumlah data tersisa menjadi 3795 entri.

Dalam membangun sistem rekomendasi pada proyek ini, digunakan beberapa fitur utama, yaitu: ***name, score, genre, vote, company, dan star.***
- Untuk sistem rekomendasi berbasis genre, atribut yang digunakan adalah *name* dan *genre*.
- Untuk sistem rekomendasi menggunakan metode Collaborative Filtering, atribut yang digunakan meliputi *name, score*, dan *company*.
- Selain itu, dilakukan juga proses **one-hot encoding** pada fitur *star* dan *company* untuk mengubah variabel kategorikal menjadi format numerik yang dapat diproses oleh model pembelajaran mesin.
- Khusus pada sistem Content-Based Filtering, dilakukan **TF-IDF Vectorization** pada fitur *genre*. TF-IDF digunakan untuk mengubah teks genre menjadi vektor numerik berbasis frekuensi, yang kemudian digunakan untuk menghitung tingkat kemiripan antar film menggunakan Cosine Similarity.

## Modelling
Pada proyek ini, hanya digunakan dua model, yaitu Cosine Similarity dan K-Nearest Neighbor (KNN). Kedua algoritma ini digunakan untuk mengukur tingkat kesamaan antar data berdasarkan fitur-fitur yang tersedia. Model akan mempelajari kemiripan antar entri dalam dataset guna menghasilkan sistem rekomendasi yang relevan.

#### Cosine Similarity
Cosine Similarity adalah sebuah metode yang digunakan untuk mengukur tingkat kemiripan antara dua vektor dalam ruang multidimensi. Perhitungan ini didasarkan pada nilai kosinus dari sudut antara dua vektor, yang masing-masing direpresentasikan oleh dimensi dan magnitudonya. Nilai hasil pengukuran cosine similarity berkisar antara -1 hingga 1:
- Nilai 1 menunjukkan bahwa kedua vektor memiliki arah yang sama (sangat mirip),
- Nilai 0 menunjukkan bahwa kedua vektor tegak lurus (tidak memiliki hubungan),
- Nilai -1 menunjukkan arah yang sepenuhnya berlawanan (sangat tidak mirip).
Metode ini umum digunakan dalam bidang pemrosesan teks dan pengelompokan data untuk menentukan tingkat kemiripan antar dokumen atau antar fitur dalam suatu dataset [[6](https://medium.com/geekculture/cosine-similarity-and-cosine-distance-48eed889a5c4)]

Rumus Cosine Similarity dituliskan dalam : 

$$Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||)$$ 

dimana: 
- (A·B) menyatakan produk titik dari vektor A dan B.
- ||A|| mewakili norma Euclidean (magnitudo) dari vektor A.
- ||B|| mewakili norma Euclidean (magnitudo) dari vektor B.

Untuk melakukan pengujian model, digunakan potongan kode berikut.
```python
film_recommendations('The Green Mile')
```

| name                                             | genre                                                       |
|--------------------------------------------------|--------------------------------------------------------------|
| Kama Sutra A Tale of Love                 |Crime                        |
| Scarface	                                |Crime                        |
| The Cell                                  |Crime                      |
| Carlitos Way	|Crime                     |
| A Bronx Tale	         |Crime                  |

Table 1. Hasil Pengujian Model Content Based Filtering (dengan Filter genre).

Berdasarkan Tabel 1, hasil pengujian model Content-Based Filtering (berdasarkan Genre) menunjukkan bahwa sistem berhasil merekomendasikan 5% film teratas yang paling mirip dengan The Green Mile. Rekomendasi ini mencakup beberapa seri dan film yang masih berada dalam waralaba The Green Mile itu sendiri. Artinya, ketika seorang pengguna menyukai The Green Mile, sistem mampu menyarankan seri atau film lain yang masih memiliki keterkaitan erat.

Pendekatan ini bekerja dengan cara mengidentifikasi kemiripan dalam atribut genre antara The Green Mile dan film lainnya, sehingga pengguna dapat menerima rekomendasi konten yang relevan dengan preferensi mereka. Dengan demikian, sistem mampu membantu pengguna menemukan tontonan lain yang sejalan dengan ketertarikan mereka terhadap The Green Mile.

Kelebihan Cosine Similarity : 
  - Efisiensi Perhitungan: Memiliki kompleksitas yang rendah, sehingga sangat efisien digunakan dalam proses komputasi, terutama pada skala besar.
  - Tangguh terhadap Dimensi Tinggi: Cocok diterapkan pada dataset berdimensi tinggi karena metode ini fokus pada arah vektor, bukan pada jumlah dimensi data.

Kekurangan Cosine Similarity:
  - Mengabaikan Besarnya Nilai (Magnitudo): Hanya mempertimbangkan arah vektor dan tidak memperhitungkan besarannya. 
  - Rentan terhadap Nilai Ekstrem: Dua vektor dengan magnitudo yang sangat berbeda tetap dapat dianggap mirip jika memiliki arah yang sama, meskipun secara nilai sesungguhnya cukup jauh.

## K-Nearest Neighbor
K-Nearest Neighbor (KNN) merupakan salah satu algoritma paling sederhana dalam klasifikasi dan regresi. Metode ini bekerja dengan mengklasifikasikan suatu data berdasarkan kedekatannya terhadap sejumlah data tetangga terdekat dalam ruang fitur. Jumlah tetangga yang diperhitungkan ditentukan oleh parameter K. Semakin dekat jarak antara data baru dengan data dalam kelompok tertentu, maka semakin besar kemungkinan data baru tersebut termasuk ke dalam kelompok tersebut.

Sebagai contoh, jika K = 1, maka klasifikasi dilakukan berdasarkan satu tetangga terdekat saja—artinya data baru akan diberi label yang sama dengan data yang paling mirip atau paling dekat jaraknya.[[7](https://medium.com/bee-solution-partners/cara-kerja-algoritma-k-nearest-neighbor-k-nn-389297de543e)]

K-Nearest Neighbor dituliskan dalam rumus:

 $$Euclidean Distance (P, Q) = sqrt(∑(Pi - Qi)^2)$$

dimana:
- Pi merepresentasikan nilai fitur ke-i dari titik data P.
- Qi merepresentasikan nilai fitur ke-i dari titik data Q, yang merupakan bagian dari kumpulan data D.
- ∑ adalah simbol yang digunakan untuk menjumlahkan seluruh nilai fitur dari data yang dibandingkan.

Hasil Pengujian Model K-Nearest Neighbor (KNN) menggunakan Euclidean Distance:

Jika pengguna menyukai film Heavens Gate, maka sistem merekomendasikan beberapa film lain yang memiliki kemiripan berdasarkan kedekatan jarak fitur, antara lain:

Berikut ini adalah aplikasi yang juga mungkin akan disukai :
| Nama Film                                   | Similarity Score |
|----------------------------------------------|------------------|
| Heavens Gate	        | 100.0%           |
| Fright Night	| 98.55%           |
| A Passage to India	                                 | 98.53%           |
| Crossing Delancey	98.                 | 98.27%           |
| Stir Crazy	                           | 98.00%           |

Tabel 2. Hasil Pengujian Model K-Nearest Neighbor

Berdasarkan Tabel 2, model K-Nearest Neighbor (KNN) menghasilkan rekomendasi film yang memiliki kemiripan berdasarkan fitur-fitur seperti Name, Score, Type, dan Studios. Ketika pengguna menyukai film Heavens Gate, model berhasil memberikan rekomendasi film yang dinilai serupa berdasarkan pola data yang telah dipelajari.

Rekomendasi yang dihasilkan meliputi :
- Heavens Gate (100.00%)
- Fright Night (98.55%)
- A Passage To India (TV) (98.53%)
- Crossing Delancey 98. (98.27%)
- Stir Crazy (98.00%)
Persentase yang tercantum menunjukkan tingkat kemiripan relatif dari masing-masing film terhadap film acuan. Hasil ini menunjukkan bahwa model KNN dapat secara efektif mengidentifikasi dan merekomendasikan film-film dengan karakteristik yang serupa. Pendekatan ini sangat membantu pengguna dalam menemukan konten yang relevan dan sesuai dengan preferensi mereka berdasarkan film yang telah disukai sebelumnya.

Kelebihan K-Nearest Neighbor (KNN):
1. Waktu pelatihan yang sangat cepat
2. Algoritma yang sederhana dan mudah dipahami
3. Tahan terhadap data pelatihan yang mengandung noise
4. Efektif pada dataset berukuran besar

Kekurangan K-Nearest Neightbor (KNN) :
1. Penentuan nilai k menjadi bias dalam model.
2. Komputasi yang kompleks, terutama pada data besar atau dimensi fitur tinggi.
3. Keterbatasan memori karena harus menyimpan semua data pelatihan.
4. Rentan terhadap atribut yang tidak relevan yang dapat memengaruhi hasil klasifikasi.


## Evaluation
Metrik evaluasi digunakan untuk menilai seberapa baik performa suatu model dalam menjalankan tugasnya, baik dalam konteks klasifikasi maupun klastering. Dalam proyek ini, beberapa metrik evaluasi yang digunakan antara lain:

### 1. Precision
Precision digunakan dalam konteks klasifikasi untuk mengukur proporsi prediksi positif yang benar-benar relevan. Metrik ini penting untuk mengetahui seberapa akurat model dalam mengidentifikasi kelas positif dibandingkan dengan semua prediksi positif yang dibuat.
  
Precision merupakan salah satu metrik evaluasi yang penting dalam menilai kinerja model, khususnya dalam konteks klasifikasi atau pengelompokan berbasis label. Precision mengukur proporsi prediksi positif yang benar dari keseluruhan prediksi positif yang dibuat oleh model. Nilai precision yang tinggi menunjukkan bahwa model memiliki tingkat kesalahan rendah dalam mengklasifikasikan data sebagai positif, sehingga hasil prediksi positif dapat dianggap lebih akurat dan dapat dipercaya. Dengan demikian, precision sangat membantu dalam mengevaluasi ketepatan model dalam mengenali data yang relevan dari seluruh prediksi positif yang dihasilkan[[8](https://esairina.medium.com/memahami-confusion-matrix-accuracy-precision-recall-specificity-dan-f1-score-610d4f0db7cf)].

Rumus Presisi Ditulis seperti ini :

$$Presisi = \frac{TP}{TP + FP}$$

dimana: 
- True Positive (TP): Jumlah data yang diklasifikasikan sebagai positif oleh model, dan memang benar-benar termasuk dalam kelas positif.
- False Positive (FP): Jumlah data yang diklasifikasikan sebagai positif oleh model, namun sebenarnya termasuk dalam kelas negatif.

Interpretasi Hasil Presisi Berdasarkan Tabel 1:

Berdasarkan Tabel 1. Hasil Pengujian Model Content Based Filtering (dengan Filter genre), diketahui bahwa nilai presisi model untuk rekomendasi Top-5 adalah sempurna, yakni 5 dari 5 atau 100%. Artinya, semua rekomendasi yang diberikan oleh model merupakan film yang memiliki genre serupa dengan film The Green Mile, yakni Crime.

Presisi yang tinggi ini mengindikasikan bahwa model memiliki performa yang sangat baik dalam mengidentifikasi item yang relevan sesuai preferensi pengguna. Lima rekomendasi teratas yang dihasilkan model terbukti konsisten dalam menyajikan film dengan genre yang sama atau sangat mirip dengan The Green Mile. Dengan demikian, model Content Based Filtering ini efektif dalam membantu pengguna menemukan tontonan yang sesuai dengan minat mereka.

### 2. Skor Calinski-Harabasz
Metrik ini digunakan untuk mengevaluasi hasil dari algoritma klastering. Semakin tinggi nilai Calinski-Harabasz, semakin baik performa klastering, karena menunjukkan bahwa klaster yang terbentuk memiliki jarak antar klaster yang besar dan kepadatan internal klaster yang tinggi.

Calinski-Harabasz Score merupakan salah satu metrik evaluasi yang digunakan untuk menilai kualitas hasil pengelompokan (clustering). Metrik ini mengukur seberapa baik algoritma pengelompokan dalam memisahkan data ke dalam kelompok-kelompok yang padat (kompak) di dalam masing-masing cluster, sekaligus saling berjauhan (terpisah) antar cluster.

Skor ini dihitung sebagai rasio antara sebaran antar cluster (antara pusat cluster) terhadap sebaran dalam cluster (antar data di dalam cluster yang sama). Semakin tinggi nilai Calinski-Harabasz (CH), semakin baik hasil pengelompokan tersebut. Kelebihan utama dari metrik ini adalah tidak memerlukan label kebenaran dasar (ground truth), sehingga sangat cocok untuk digunakan dalam metode unsupervised learning seperti clustering.[[9](https://medium.com/@haataa/how-to-measure-clustering-performances-when-there-are-no-ground-truth-db027e9a871c)]

Rumus Skor Calinski-Harabasz adalah:

$$CH = \frac{B}{W} \times \frac{N - k}{k - 1}$$

Penjelasan :
- B = menyatakan variabilitas antar klaster (between-cluster variance).
- W = menunjukkan variabilitas di dalam masing-masing klaster (within-cluster variance).
- N = merepresentasikan total jumlah data yang dianalisis.
- k = menggambarkan jumlah klaster yang terbentuk dalam proses pengelompokan.

Untuk melakukan pengujian pada model, digunakan kode berikut.
```python
calinski_harabasz_score(data_baru, filmdata_name)
```
Dan didapatkan score dari pengujian model.
```
0.8370911010140509
```

Hasil evaluasi menunjukkan bahwa pemisahan antar kluster dalam model ini belum optimal, yang ditunjukkan oleh nilai skor Calinski-Harabasz (CH) yang relatif rendah, yaitu sebesar 0.837. Nilai CH yang rendah mengindikasikan bahwa data dalam masing-masing kluster belum cukup kompak dan antar kluster belum cukup terpisah.

Kondisi ini dapat menyebabkan sistem merekomendasikan aplikasi yang kurang relevan dengan preferensi pengguna, karena pengelompokan yang dilakukan belum mencerminkan struktur data yang jelas. Oleh karena itu, perlu dilakukan evaluasi ulang terhadap parameter model atau metode fitur yang digunakan agar pemisahan kluster dapat ditingkatkan dan kualitas rekomendasi menjadi lebih akurat.


### 3. Skor Davies-Bouldin
Davies-Bouldin Index mengukur rasio antara jarak dalam klaster dan jarak antar klaster. Nilai yang lebih rendah menunjukkan klaster yang lebih baik karena berarti klaster tersebut lebih terpisah dan lebih kompak.

Davies-Bouldin Score adalah metrik evaluasi untuk menilai kualitas hasil pengelompokan dalam algoritma clustering. Metrik ini mengukur rata-rata tingkat kemiripan antara setiap klaster dengan klaster paling mirip lainnya. Kemiripan ini dihitung berdasarkan rasio antara sebaran dalam klaster (intra-cluster distance) dan jarak antar klaster (inter-cluster distance).

Skor DB memiliki nilai minimum 0, di mana nilai yang lebih rendah menunjukkan performa pengelompokan yang lebih baik. Skor yang rendah mengindikasikan bahwa klaster-klaster yang terbentuk:

- Memiliki jarak yang jauh antar satu sama lain (baik pemisahan antar klaster),
- Dan memiliki penyebaran data yang kompak dalam masing-masing klaster.
Sama seperti Silhouette Score, Davies-Bouldin Score tidak memerlukan label kebenaran dasar (ground truth), sehingga cocok digunakan untuk mengevaluasi model unsupervised learning. Dengan formulasi yang lebih sederhana, metrik ini memberikan cara yang efisien untuk menilai kinerja model pengelompokan secara objektif.[[10](https://ieeexplore.ieee.org/document/4766909)]

Rumus dari Skor Davies-Bouldin adalah:


$$ DB = \frac{1}{k} \sum_{i=1}^{k} \max_{j \neq i} \left( \frac{R_i + R_j}{d(c_i, c_j)} \right) $$


Di mana:
- k: Jumlah total klaster yang terbentuk.
- R_i Ukuran penyebaran (radius) dari klaster ke-i, biasanya dihitung sebagai rata-rata jarak antara tiap titik dalam klaster ke pusatnya.
- d(c_i, c_j) Jarak antara pusat klaster i dan pusat klaster j.

Davies-Bouldin Score (DB) didefinisikan sebagai rata-rata dari nilai-nilai R untuk semua klaster dalam hasil pengelompokan. Nilai R ini merepresentasikan rasio antara sebaran dalam klaster (intra-cluster dispersion) dan jarak antar pusat klaster (inter-cluster distance).

Untuk melakukan pengujian model, digunakan potongan kode berikut.
```python
davies_bouldin_score(data_baru, filmdata_name)
```
Dan didapatkan skor dari pengujian model.
```python
1.0766974943290932
```

Skor Davies-Bouldin (DB) sebesar 1.08 menunjukkan bahwa hasil klasterisasi yang dilakukan cukup baik, dengan klaster yang relatif terpisah dan kompak meskipun masih ada ruang untuk perbaikan. Skor ini berada pada kisaran yang umumnya dianggap layak untuk digunakan dalam analisis lebih lanjut, seperti segmentasi data atau sistem rekomendasi. Semakin rendah skor DB, semakin baik kualitas klasterisasi, karena menunjukkan bahwa klaster-klaster saling berjauhan dan masing-masing memiliki penyebaran data yang kecil. Oleh karena itu, skor ini mengindikasikan bahwa struktur klaster sudah terbentuk dengan cukup baik, namun tetap bisa dioptimalkan misalnya dengan menyesuaikan jumlah klaster atau melakukan praproses data tambahan.



# Referensi

1. https://doi.org/10.1007/978-0-387-85820-3\_3](https://doi.org/10.1007/978-0-387-85820-3_3

2. https://id.wikipedia.org/wiki/film#:~:text=4.2%20Bacaan%20terkait-,Definisi%20dan%20penggunaan,animasi%20yang%20dibuat%20di%20Jepang%22.

3. https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/20612/19925

4. https://journal.mediapublikasi.id/index.php/logic/article/view/4299

5. https://www.researchgate.net/publication/274712918_Rekomendasi_Anime_dengan_Latent_Semantic_Indexing_Berbasis_Sinopsis_Genre

6. http://repository.uin-malang.ac.id/18842/1/18842.pdf

7. https://medium.com/geekculture/cosine-similarity-and-cosine-distance-48eed889a5c4

8. https://medium.com/bee-solution-partners/cara-kerja-algoritma-k-nearest-neighbor-k-nn-389297de543e

9. https://esairina.medium.com/memahami-confusion-matrix-accuracy-precision-recall-specificity-dan-f1-score-610d4f0db7cf

10. https://medium.com/@haataa/how-to-measure-clustering-performances-when-there-are-no-ground-truth-db027e9a871c

11. https://ieeexplore.ieee.org/document/4766909
