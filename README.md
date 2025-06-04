# Laporan Proyek Machine Learning -  Muhammad Nurul Fatwa Al Fajar

## Project Overview
![Film](https://github.com/user-attachments/assets/8d88be1f-b881-41c3-a158-3accf4041b41)

Film merupakan media hiburan favorit di berbagai kalangan dan kini dapat diakses melalui banyak platform streaming. Meski begitu, banyaknya judul yang tersedia terkadang menyulitkan pengguna aplikasi dalam memilih film yang sesuai dengan preferensi mereka masing masing. Untuk mengatasi permasalahan ini, pada penelitian ini mengajukan pengembangan sistem rekomendasi[[2](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/20612/19925)]. Sistem ini dirancang untuk Menemukan Nama film Yang Dicari serta genre yang sama dengan film Tersebut. Berdasarkan data tersebut, sistem dapat menyarankan film yang paling sesuai dengan selera individu[[3](https://journal.mediapublikasi.id/index.php/logic/article/view/4299)].

Bagi pengguna, sistem ini memungkinkan mereka menemukan film baru yang sesuai minat, menjelajahi genre yang belum pernah ditonton, dan mendapatkan rekomendasi sesuai dengan suasana hati mereka. Sementara bagi perusahaan, sistem ini berpotensi meningkatkan jumlah penonton, menyajikan konten yang lebih bervariasi, meningkatkan kepuasan pengguna, serta memahami pola preferensi penonton terhadap film.

Secara keseluruhan, sistem rekomendasi ini dapat menjadi solusi yang efektif dalam membantu pengguna dalam menemukan judul film yang cocok dengan minat mereka, sekaligus meningkatkan kualitas pengalaman menonton secara menyeluruh[[4](https://www.researchgate.net/publication/274712918_Rekomendasi_film_dengan_Latent_Semantic_Indexing_Berbasis_Sinopsis_Genre)].


## Business Understanding
Sistem rekomendasi film berpotensi memberikan berbagai manfaat signifikan, baik bagi penonton maupun penyedia layanan streaming. Bagi pengguna, sistem ini mempermudah dalam menemukan film yang sesuai dengan minat secara lebih praktis dan efektif. Sementara itu, bagi platform streaming, sistem ini dapat meningkatkan interaksi pengguna, memperkuat loyalitas penonton, serta membantu operasional platform menjadi lebih efisien dan responsif terhadap kebutuhan pengguna. [[5](http://repository.uin-malang.ac.id/18842/1/18842.pdf)]

## Problem Statements
- Bagaimana membangun sistem rekomendasi film yang menyarankan tontonan kepada pengguna dengan mengacu pada genre yang diminati?
- Bagaimana penyedia layanan streaming dapat menyarankan film dengan genre yang sama dengan judul yang sebelumnya ditonton?
- Bagaimana membangun model rekomendasi menggunakan pendekatan Cosine Similarity?

## Goals
Untuk menangani permasalahan tersebut, dirancanglah sebuah sistem rekomendasi dengan tujuan sebagai berikut :
- Menyajikan daftar Top-N rekomendasi film kepada pengguna berdasarkan genre yang diminati.
- Memberikan sejumlah rekomendasi film yang relevan dengan minat pengguna dan Judul film lain yang memiliki genre yang sama.
- Mengembangkan model sistem rekomendasi menggunakan pendekatan Cosine Similarity berdasarkan fitur yang telah diekstraksi dari dataset.

Solution Approach
Data dianalisis melalui proses ***Exploratory Data Analysis (EDA)*** dan ***divisualisasikan*** untuk memahami pola serta karakteristik yang ada. Untuk memperoleh model prediksi yang optimal, dilakukan ***pembersihan data***, seperti menghapus ***nilai yang hilang*** (missing value), memeriksa keberadaan ***data duplikat***, menghapus karakter ***alfanumerik*** yang tidak relevan, serta menghilangkan ***tautan*** (URL). Selanjutnya, data ***kategorikal dikonversi menjadi format numerik*** menggunakan metode ***one-hot encoding***. Guna menilai performa model yang dibangun, digunakan metrik evaluasi seperti ***Precision***.

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

# Penjelasan Kolom dalam Dataframe Anime

Dataset anime ini memuat berbagai informasi penting pada setiap kolom, yang dijelaskan sebagai berikut :

1. ***film***: Sebagai label/ID unik; bisa juga digunakan untuk menampilkan hasil rekomendasi.

2. ***rating***: Fitur kategorikal: mengelompokkan konten sesuai batas usia.

3. ***genre***: Fitur multi-label: bisa di-encode dengan one-hot atau embedding genre.

4. ***year***: Fitur numerik: mengukur umur film, tren preferensi berdasarkan era.

5. ***released***: Bisa di-parse jadi tanggal (`datetime`) untuk ekstrak bulan, kuartal, hari dalam seminggu, dll.

6. ***score***: Fitur numerik: merepresentasikan popularitas/penilaian umum film.

7. ***votes***: Fitur numerik: proxy untuk seberapa banyak orang yang menilai—indikator popularitas.

8. ***director***: Fitur kategorikal: di-encode (label/one-hot/embedding). Sutradara populer bisa meningkatkan rekomendasi.

9. ***writer***: Serupa `director`: fitur kategorikal untuk menangkap gaya penulisan.

10. ***star***: Fitur kategorikal penting—aktor favorit pengguna dapat memengaruhi rekomendasi.

11. ***country***: Fitur kategorikal: mengelompokkan selera berdasarkan wilayah.

12. ***budget***: Fitur numerik: film ber-anggaran besar cenderung produksi lebih “berkelas” dan populer.

13. ***gross***: Fitur numerik: proxy keberhasilan komersial—sering dikaitkan dengan popularitas massal.

14. ***company***: Fitur kategorikal: studio besar biasanya memproduksi film dengan kualitas/genre tertentu.

15. ***runtime***: Durasi film berjalan.


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
- Untuk bagian set_indexing kolom yang digunakan kolom *name*.
- Untuk sistem rekomendasi berbasis genre, atribut yang digunakan adalah *name* dan *genre*.
- Untuk sistem rekomendasi menggunakan metode Collaborative Filtering, atribut yang digunakan meliputi *name, score*, dan *company*.
- Khusus pada sistem Content-Based Filtering, dilakukan **TF-IDF Vectorization** pada fitur *genre*. TF-IDF digunakan untuk mengubah teks genre menjadi vektor numerik berbasis frekuensi, yang kemudian digunakan untuk menghitung tingkat kemiripan antar film menggunakan Cosine Similarity.
- Selain itu, dilakukan juga proses **one-hot encoding** pada fitur *star* dan *company* untuk mengubah variabel kategorikal menjadi format numerik yang dapat diproses oleh model pembelajaran mesin.

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

## Evaluation
Metrik evaluasi digunakan untuk menilai seberapa baik performa suatu model dalam menjalankan tugasnya. Dalam proyek ini, ada 1 metrik evaluasi yang digunakan yaitu:

### 1. Precision
Precision digunakan dalam konteks klasifikasi untuk mengukur proporsi prediksi positif yang benar-benar relevan. Metrik ini penting untuk mengetahui seberapa akurat model dalam mengidentifikasi kelas positif dibandingkan dengan semua prediksi positif yang dibuat.
  
Precision merupakan salah satu metrik evaluasi yang penting dalam menilai kinerja model, khususnya dalam konteks klasifikasi atau pengelompokan berbasis label. Precision mengukur proporsi prediksi positif yang benar dari keseluruhan prediksi positif yang dibuat oleh model. Nilai precision yang tinggi menunjukkan bahwa model memiliki tingkat kesalahan rendah dalam mengklasifikasikan data sebagai positif, sehingga hasil prediksi positif dapat dianggap lebih akurat dan dapat dipercaya. Dengan demikian, precision sangat membantu dalam mengevaluasi ketepatan model dalam mengenali data yang relevan dari seluruh prediksi positif yang dihasilkan[[7](https://esairina.medium.com/memahami-confusion-matrix-accuracy-precision-recall-specificity-dan-f1-score-610d4f0db7cf)].

Rumus Presisi Ditulis seperti ini :

$$Presisi = \frac{TP}{TP + FP}$$

dimana: 
- True Positive (TP): Jumlah data yang diklasifikasikan sebagai positif oleh model, dan memang benar-benar termasuk dalam kelas positif.
- False Positive (FP): Jumlah data yang diklasifikasikan sebagai positif oleh model, namun sebenarnya termasuk dalam kelas negatif.

Interpretasi Hasil Presisi Berdasarkan Tabel 1:

Berdasarkan Tabel 1. Hasil Pengujian Model Content Based Filtering (dengan Filter genre), diketahui bahwa nilai presisi model untuk rekomendasi Top-5 adalah sempurna, yakni 5 dari 5 atau 100%. Artinya, semua rekomendasi yang diberikan oleh model merupakan film yang memiliki genre serupa dengan film The Green Mile, yakni Crime.

Presisi yang tinggi ini mengindikasikan bahwa model memiliki performa yang sangat baik dalam mengidentifikasi item yang relevan sesuai preferensi pengguna. Lima rekomendasi teratas yang dihasilkan model terbukti konsisten dalam menyajikan film dengan genre yang sama atau sangat mirip dengan The Green Mile. Dengan demikian, model Content Based Filtering ini efektif dalam membantu pengguna menemukan tontonan yang sesuai dengan minat mereka.


# Referensi

1. https://id.wikipedia.org/wiki/film#:~:text=4.2%20Bacaan%20terkait-,Definisi%20dan%20penggunaan,animasi%20yang%20dibuat%20di%20Jepang%22.

2. https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/20612/19925

3. https://journal.mediapublikasi.id/index.php/logic/article/view/4299

4. https://www.researchgate.net/publication/274712918_Rekomendasi_film_dengan_Latent_Semantic_Indexing_Berbasis_Sinopsis_Genre

5. http://repository.uin-malang.ac.id/18842/1/18842.pdf

6. https://medium.com/geekculture/cosine-similarity-and-cosine-distance-48eed889a5c4

7. https://esairina.medium.com/memahami-confusion-matrix-accuracy-precision-recall-specificity-dan-f1-score-610d4f0db7cf
