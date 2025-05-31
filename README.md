# Laporan Proyek Machine Learning -  Muhammad Nurul Fatwa Al Fajar

## Project Overview
![55e257ed-234a-441b-a94c-efd19ad2aedf](https://github.com/user-attachments/assets/b05a4903-136a-4196-8ab5-09bbd195071e)

Bagi kalian yang belum mengetahui, Anime adalah animasi khas Jepang, Berasal dari serapan kata "Animation"[[1](https://id.wikipedia.org/wiki/Anime#:~:text=4.2%20Bacaan%20terkait-,Definisi%20dan%20penggunaan,animasi%20yang%20dibuat%20di%20Jepang%22.)]( telah menjadi tontonan favorit di berbagai kalangan dan kini dapat diakses melalui banyak platform streaming. Meski begitu, banyaknya judul yang tersedia terkadang menyulitkan pengguna aplikasi dalam memilih anime yang sesuai dengan preferensi mereka masing masing. Untuk mengatasi permasalahan ini, pada penelitian ini mengajukan pengembangan sistem rekomendasi[[2](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/20612/19925)]. Sistem ini dirancang untuk menganalisis riwayat tontonan pengguna, genre yang disukai, serta penilaian yang pernah diberikan. Berdasarkan data tersebut, sistem dapat menyarankan anime yang paling sesuai dengan selera individu[[3](https://journal.mediapublikasi.id/index.php/logic/article/view/4299)].

Tak hanya itu, elemen tambahan seperti tingkat popularitas, ulasan dari pengguna lain, dan rekomendasi dari komunitas juga akan menjadi pertimbangan dalam sistem ini. Pendekatan ini diharapkan memberikan manfaat besar, baik bagi pengguna maupun penyedia layanan streaming. Bagi pengguna, sistem ini memungkinkan mereka menemukan anime baru yang sesuai minat, menjelajahi genre yang belum pernah ditonton, dan mendapatkan rekomendasi sesuai dengan suasana hati mereka. Sementara bagi perusahaan, sistem ini berpotensi meningkatkan jumlah penonton, menyajikan konten yang lebih bervariasi, meningkatkan kepuasan pengguna, serta memahami pola preferensi penonton terhadap anime.

Secara keseluruhan, sistem rekomendasi ini dapat menjadi solusi yang efektif dalam membantu pengguna dalam menemukan judul anime yang cocok dengan minat mereka, sekaligus meningkatkan kualitas pengalaman menonton secara menyeluruh[[4](https://www.researchgate.net/publication/274712918_Rekomendasi_Anime_dengan_Latent_Semantic_Indexing_Berbasis_Sinopsis_Genre)].


## Business Understanding
Sistem rekomendasi anime berpotensi memberikan berbagai manfaat signifikan, baik bagi penonton maupun penyedia layanan streaming. Bagi pengguna, sistem ini mempermudah dalam menemukan anime yang sesuai dengan minat secara lebih praktis dan efektif. Sementara itu, bagi platform streaming, sistem ini dapat meningkatkan interaksi pengguna, memperkuat loyalitas penonton, serta membantu operasional platform menjadi lebih efisien dan responsif terhadap kebutuhan pengguna.[[5](http://repository.uin-malang.ac.id/18842/1/18842.pdf)]

## Problem Statements
- Bagaimana membangun sistem rekomendasi anime yang menyarankan tontonan kepada pengguna dengan mengacu pada genre yang diminati?
- Bagaimana penyedia layanan streaming dapat menyarankan anime yang belum pernah ditonton oleh pengguna dengan memanfaatkan data penilaian yang telah diberikan?
- Bagaimana membangun model rekomendasi menggunakan pendekatan Cosine Similarity dan algoritma K-Nearest Neighbor?
- Bagaimana mengevaluasi kinerja dari model sistem rekomendasi yang sudah dikembangkan?

## Goals
Untuk menangani permasalahan tersebut, dirancanglah sebuah sistem rekomendasi dengan tujuan sebagai berikut :
- Menyajikan daftar Top-N rekomendasi anime kepada pengguna berdasarkan genre yang diminati.
- Memberikan sejumlah rekomendasi anime yang relevan dengan minat pengguna dan belum pernah ditonton sebelumnya.
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
| Maintainer | [ashishkumarjayswal](kaggle.com/ashishkumarjayswal)                           |
| License  | Database: Open Database, Contents: Database Contents      |
| Visibility | Publik                                                  |
| Tags     | Movies and TV Shows |
| Usability | 7.06                                                     |

Dataset yang digunakan dalam proyek ini berasal dari [MyAnimeList](https://myanimelist.net/), sebuah platform komunitas daring yang terkenal di kalangan penggemar anime dan manga. MyAnimeList menyediakan berbagai informasi penting seperti daftar anime, ulasan pengguna, serta skor atau penilaian dari pengguna terhadap berbagai judul anime. 

Dataset ini tersedia secara publik di Kaggle dengan nama [movies-updated-data](https://www.kaggle.com/datasets/ashishkumarjayswal/movies-updated-data), dan dapat diakses serta diunduh langsung melalui situs [Kaggle](https://www.kaggle.com/).

Informasi yang terdapat dataset : 
- Datasets berupa file csv (Comma-Seperated Values).
- Dataset berupa 6 buah file CSV yaitu :
  - anime-dataset-2023.csv
  - anime-filtered.csv
  - final_animedataset.csv
  - user-filtered.csv
  - users-details-2023.csv
  - users-score-2023.csv
 
Pada model yang saya buat kali ini dataset yang dipakai dari sekian banyak data adalah file ***anime-filtered.csv***
- Dataset ini terdiri dari 14.952 entri dan mencakup 25 atribut.
- Dari total fitur tersebut, terdapat 15 fitur bertipe objek, 8 fitur bertipe int64, serta 2 fitur bertipe float64.
- Ditemukan missing value pada kolom synopsis sebanyak 1.350 data dan pada kolom ranked sebanyak 1.721 data.
- Tidak ditemukan adanya data duplikat dalam dataset ini.

### Variabel pada dataset
1. anime_id: Merupakan identitas unik berupa angka atau kode untuk setiap judul anime.
2. Name: Nama asli dari anime, biasanya dalam bahasa Jepang.
3. Score: Nilai atau penilaian yang diberikan untuk anime tersebut.
4. Genres: Kategori genre dari anime yang ditampilkan, dipisahkan dengan tanda koma (contoh: Aksi, Komedi, Fantasi).
5. English name: Judul anime dalam versi bahasa Inggris (jika tersedia).
6. Japanese name: Judul anime dalam penulisan bahasa Jepang.
7. Synopsis: Ringkasan cerita atau deskripsi singkat mengenai alur cerita anime.
8. Type: Format atau bentuk dari anime, seperti Serial TV, Film, OVA, dan lainnya.
9. Episodes: Total jumlah episode yang dimiliki oleh anime.
10. Aired: Informasi mengenai tanggal atau periode penayangan anime.
11. Premiered: Musim dan tahun pertama kali anime ditayangkan.
12. Producers: Nama perusahaan atau pihak yang bertanggung jawab dalam produksi anime.
13. Licensors: Perusahaan atau platform yang memiliki hak lisensi untuk menayangkan anime.
14. Studios: Studio animasi yang mengerjakan produksi anime.
15. Source: Asal cerita dari anime, seperti manga, novel ringan, atau karya orisinal.
16. Duration: Lama waktu tayang untuk satu episode anime.
17. Rating: Kategori batas usia penonton yang disarankan.
18. Ranked: Peringkat anime berdasarkan skor, ulasan, atau kriteria tertentu.
19. Popularity: Peringkat popularitas berdasarkan jumlah interaksi pengguna.
20. Members: Jumlah pengguna yang memasukkan anime ke dalam daftar mereka.
21. Favorites: Jumlah pengguna yang menandai anime sebagai favorit.
22. Watching: Jumlah pengguna yang sedang menonton anime tersebut.
23. Completed: Jumlah pengguna yang telah menyelesaikan anime.
24. On Hold: Jumlah pengguna yang menghentikan sementara tontonan anime.
25. Dropped: Jumlah pengguna yang memutuskan untuk tidak melanjutkan menonton anime.


![Distribusi Skor Rata-rata Anime](https://github.com/user-attachments/assets/1babe9de-41e4-45a1-a5db-515a362a1633)

Gambar 1.Rating/Skor

![Distribusi Kategori](https://github.com/user-attachments/assets/5dc28b07-21b0-4fcf-9c6b-f66a6f24769b)

Gambar 2. Distribusi Kategori

Berdasarkan Gambar 1, diketahui bahwa nilai rata-rata rating anime adalah 6.5, dengan rating terendah sebesar 1.8 dan rating tertinggi mencapai 9.1. Sementara pada Gambar 2, distribusi kategori jenis anime menunjukkan bahwa dataset terdiri dari 6 tipe utama, yaitu: TV, OVA, Movie, Special, ONA, dan Music.TV (Television Series) adalah serial anime yang ditayangkan melalui saluran televisi dengan jumlah episode yang bervariasi. OVA (Original Video Animation) merupakan anime yang dirilis langsung untuk media rumahan seperti DVD atau Blu-ray. Movie adalah anime yang ditayangkan di bioskop dan umumnya memiliki durasi yang lebih panjang. Special merujuk pada episode tambahan atau bonus yang biasanya terhubung dengan serial TV atau film utama. ONA (Original Net Animation) adalah anime yang dirilis secara eksklusif melalui platform daring atau internet. Music merupakan jenis anime yang dibuat untuk mendukung promosi rilisan musik seperti album atau single.

![Anime Komunitas](https://github.com/user-attachments/assets/68504918-8bb8-4867-b1cd-c5067cc406c6)

Gambar 3. Top 15 Anime Community

![Skor Anime](https://github.com/user-attachments/assets/80009361-08cc-449b-9176-ae2ef3ba6eab)

Gambar 4. Top 15 Anime Rating Tertinggi 

Berdasarkan Gambar 3, yang menampilkan Top 15 Komunitas Anime, dapat dilihat bahwa anime Death Note menempati posisi pertama sebagai anime dengan komunitas terbanyak, diikuti oleh Shingeki no Kyojin di posisi kedua, Fullmetal Alchemist: Brotherhood ketiga, Sword Art Online keempat, dan One Punch Man kelima. Selanjutnya, Boku no Hero Academia berada di urutan keenam, Tokyo Ghoul ketujuh, Naruto kedelapan, Steins;Gate kesembilan, dan No Game No Life menempati posisi kesepuluh, kimi no na wa kesebelas, hunter x hunter ke dua belas, Boku no Hero Academia 2nd Season ke tiga belas, Angle Beats! ke empat belas, dan Shingeki no Kyojin Season 2 ke lima belas.

Informasi ini dapat dimanfaatkan oleh pengembang sistem untuk merekomendasikan anime yang populer berdasarkan jumlah anggota komunitasnya. Semakin besar komunitas, semakin besar pula indikasi bahwa anime tersebut digemari dan mendapat perhatian dari banyak pengguna.

Sedangkan pada Gambar 4, yang menampilkan Top 10 Anime dengan Rating Tertinggi, anime dengan peringkat tertinggi pertama adalah Fullmetal Alchemist: Brotherhood, diikuti oleh Shingeki no Kyojin: Final Season di posisi kedua, Steins;Gate ketiga, Shingeki no Kyojin Season 3 Part 2 keempat, dan Hunter x Hunter (2011) kelima. Di posisi keenam terdapat Gintama°, ketujuh Gintama', kedelapan Ginga Eiyuu Densetsu, kesembilan Gintama': Enchousen, dan kesepuluh adalah 3-gatsu no Lion 2nd Season. kesebelas ada Koe no Katachi, dua belas ada Gintama., ke tiga belas ada Gintama lagi, ke empat belas ada Clannad: After Story, dan Terakhir ke lima belas ada Kimi no Na Wa.

Data ini juga dapat dijadikan acuan dalam sistem rekomendasi, karena anime dengan rating tinggi umumnya mencerminkan kualitas cerita dan penerimaan yang baik oleh pengguna. Makin banyak pengguna yang memberikan rating, makin besar kemungkinan bahwa anime tersebut populer dan layak ditonton.

## Data Preparation
Pada tahap Data Preparation, dilakukan text cleaning untuk membersihkan teks dari tanda baca dan tautan (URL). Untuk menangani missing value, digunakan metode dropping dengan fungsi drop(). Alasan penggunaan metode ini adalah karena data yang dihapus tidak memberikan pengaruh signifikan terhadap performa model. Awalnya, dataset berjumlah 14.952 entri, dan setelah menghapus data yang memiliki missing value, jumlah data tersisa menjadi 13.229 entri.

Dalam membangun sistem rekomendasi pada proyek ini, digunakan beberapa fitur utama, yaitu: ***Name, Score, Genres, Type, dan Studios.***
- Untuk sistem rekomendasi berbasis genre, atribut yang digunakan adalah *Name* dan *Genres*.
- Untuk sistem rekomendasi menggunakan metode Collaborative Filtering, atribut yang digunakan meliputi *Name, Score*, dan *Type*.
- Selain itu, dilakukan juga proses **one-hot encoding** pada fitur *Type* dan *Studios* untuk mengubah variabel kategorikal menjadi format numerik yang dapat diproses oleh model pembelajaran mesin.
- Khusus pada sistem Content-Based Filtering, dilakukan **TF-IDF Vectorization** pada fitur *Genres*. TF-IDF digunakan untuk mengubah teks genre menjadi vektor numerik berbasis frekuensi, yang kemudian digunakan untuk menghitung tingkat kemiripan antar anime menggunakan Cosine Similarity.

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
anime_recommendations('Naruto')
```

| Name                                             | Genres                                                       |
|--------------------------------------------------|--------------------------------------------------------------|
| Boruto Jump Festa 2016 Special                   |Action, Adventure, Comedy, Super Power                        |
| Naruto Shippuuden                                |Action, Adventure, Comedy, Super Power                        |
| Rekka no Honoo                                   |Action, Adventure, Martial Arts, Shounen                      |
| Naruto Honoo no Chuunin Shiken Naruto vs Konoh...|Action, Adventure, Martial Arts, Shounen,                     |
| Naruto Shippuuden Movie 6 Road to Ninja	         |Action, Adventure, Super Power, Martial Arts                  |

Table 1. Hasil Pengujian Model Content Based Filtering (dengan Filter Genres).

Berdasarkan Tabel 1, hasil pengujian model Content-Based Filtering (berdasarkan Genre) menunjukkan bahwa sistem berhasil merekomendasikan 5% anime teratas yang paling mirip dengan Naruto. Rekomendasi ini mencakup beberapa seri dan film yang masih berada dalam waralaba Naruto itu sendiri. Artinya, ketika seorang pengguna menyukai Naruto, sistem mampu menyarankan seri atau film lain yang masih memiliki keterkaitan erat.

Pendekatan ini bekerja dengan cara mengidentifikasi kemiripan dalam atribut genre antara Naruto dan anime lainnya, sehingga pengguna dapat menerima rekomendasi konten yang relevan dengan preferensi mereka. Dengan demikian, sistem mampu membantu pengguna menemukan tontonan lain yang sejalan dengan ketertarikan mereka terhadap Naruto.

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

Jika pengguna menyukai anime Neon Genesis Evangelion: Death & Rebirth, maka sistem merekomendasikan beberapa anime lain yang memiliki kemiripan berdasarkan kedekatan jarak fitur, antara lain:

Berikut ini adalah aplikasi yang juga mungkin akan disukai :
| Anime Name                                   | Similarity Score |
|----------------------------------------------|------------------|
| Neon Genesis Evangelion Death Rebirth        | 100.0%           |
| Neon Genesis Evangelion The End of Evangelion| 98.94%           |
| Kekkaishi TV                                 | 98.59%           |
| Doraemon Doraemon Comes Back                 | 98.59%           |
| Dr Slump Aralechan                           | 98.59%           |

Tabel 2. Hasil Pengujian Model K-Nearest Neighbor

Berdasarkan Tabel 2, model K-Nearest Neighbor (KNN) menghasilkan rekomendasi anime yang memiliki kemiripan berdasarkan fitur-fitur seperti Name, Score, Type, dan Studios. Ketika pengguna menyukai anime Neon Genesis Evangelion: Death & Rebirth, model berhasil memberikan rekomendasi anime yang dinilai serupa berdasarkan pola data yang telah dipelajari.

Rekomendasi yang dihasilkan meliputi :
- Neon Genesis Evangelion: Death & Rebirth (100.00%)
- Neon Genesis Evangelion: The End of Evangelion (98.94%)
- Kekkaishi (TV) (98.59%)
- Doraemon: Doraemon Comes Back (98.59%)
- Dr. Slump: Arale-chan (98.59%)
Persentase yang tercantum menunjukkan tingkat kemiripan relatif dari masing-masing anime terhadap anime acuan. Hasil ini menunjukkan bahwa model KNN dapat secara efektif mengidentifikasi dan merekomendasikan anime-anime dengan karakteristik yang serupa. Pendekatan ini sangat membantu pengguna dalam menemukan konten yang relevan dan sesuai dengan preferensi mereka berdasarkan anime yang telah disukai sebelumnya.

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

Berdasarkan Tabel 1. Hasil Pengujian Model Content Based Filtering (dengan Filter Genres), diketahui bahwa nilai presisi model untuk rekomendasi Top-5 adalah sempurna, yakni 5 dari 5 atau 100%. Artinya, semua rekomendasi yang diberikan oleh model merupakan anime yang memiliki genre serupa dengan anime Naruto, seperti Action, Adventure, Comedy, Drama, Fantasy, Shounen, dan Super Power.

Presisi yang tinggi ini mengindikasikan bahwa model memiliki performa yang sangat baik dalam mengidentifikasi item yang relevan sesuai preferensi pengguna. Lima rekomendasi teratas yang dihasilkan model terbukti konsisten dalam menyajikan anime dengan genre yang sama atau sangat mirip dengan Naruto. Dengan demikian, model Content Based Filtering ini efektif dalam membantu pengguna menemukan tontonan yang sesuai dengan minat mereka.

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
calinski_harabasz_score(data_baru, animedata_name)
```
Dan didapatkan score dari pengujian model.
```
3.1613291729405617
```

Hasil evaluasi menunjukkan bahwa pemisahan antar kluster dalam model ini belum optimal, yang ditunjukkan oleh nilai skor Calinski-Harabasz (CH) yang relatif rendah, yaitu sebesar 3.161. Nilai CH yang rendah mengindikasikan bahwa data dalam masing-masing kluster belum cukup kompak dan antar kluster belum cukup terpisah.

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
davies_bouldin_score(data_baru, animedata_name)
```
Dan didapatkan skor dari pengujian model.
```python
0.7864266764751376
```

Evaluasi menggunakan metrik Davies-Bouldin (DB) menghasilkan skor sebesar 0.7864266764751376, yang tergolong cukup rendah. Nilai ini menunjukkan bahwa model telah berhasil membentuk klaster dengan tingkat pemisahan yang cukup baik antar kelompok data. Dengan demikian, dapat disimpulkan bahwa kualitas pengelompokan yang dihasilkan model cukup efektif dalam memisahkan data berdasarkan kemiripan fitur.

Kondisi ini berkontribusi positif terhadap akurasi sistem rekomendasi, yang mampu menghasilkan daftar anime yang relevan dengan preferensi pengguna. Artinya, model mampu mengelompokkan data dengan baik dan mendasari hasil rekomendasi yang sesuai dengan karakteristik anime yang disukai pengguna.

Metrik-metrik ini memberikan gambaran menyeluruh terhadap kinerja model dari sisi akurasi prediksi dan kualitas pemisahan data dalam tugas klastering.



# Referensi

1. https://id.wikipedia.org/wiki/Anime#:~:text=4.2%20Bacaan%20terkait-,Definisi%20dan%20penggunaan,animasi%20yang%20dibuat%20di%20Jepang%22.

2. https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/20612/19925

3. https://journal.mediapublikasi.id/index.php/logic/article/view/4299

4. https://www.researchgate.net/publication/274712918_Rekomendasi_Anime_dengan_Latent_Semantic_Indexing_Berbasis_Sinopsis_Genre

5. http://repository.uin-malang.ac.id/18842/1/18842.pdf

6. https://medium.com/geekculture/cosine-similarity-and-cosine-distance-48eed889a5c4

7. https://medium.com/bee-solution-partners/cara-kerja-algoritma-k-nearest-neighbor-k-nn-389297de543e

8. https://esairina.medium.com/memahami-confusion-matrix-accuracy-precision-recall-specificity-dan-f1-score-610d4f0db7cf

9. https://medium.com/@haataa/how-to-measure-clustering-performances-when-there-are-no-ground-truth-db027e9a871c

10. https://ieeexplore.ieee.org/document/4766909
