# Sistem rekomendasi 

![steffen-b-28joUilHigc-unsplash](https://user-images.githubusercontent.com/88027268/204917765-94b162b6-d8f8-4023-a30c-2a54cc659cc2.jpg)
Gambar 1. Candi Borobudur yogyakarta

## Proyek overview

Pulau Jawa merupakan pulau dengan tempat wisata yang cukup populer dikunjungi oleh wisatawan lokal maupun internasional. sistem rekomendasi ini memberikan rekomendasi tempat wisata berdasarkan preference pengguna lain yang mungkin memiliki selera seperti pengguna tersebut sehingga dengan sistem ini diharapkan pengguna dapat termudahkan untuk berkunjung ke tempat wisata di pulau jawa.

Rekomendasi sistem ini dapat memudahkan user dalam memilih tempat wisata dari beberapa pilihan yang mungkin relevan dengan pengguna. Dengan termudahkannya pengguna dalam memilih tempat wisata dapat meningkatkan daya wisata ke orang banyak yang ingin mengunjungi pulau jawa. [(Ni Made Ernawati, N M Sudarmini and N M R Sukmawati, 2018)](https://www.researchgate.net/publication/322945292_Impacts_of_Tourism_in_Ubud_Bali_Indonesia_a_community-based_tourism_perspective)
 
## Business Understanding

Bagian ini akan menjelaskan proses klarifikasi masalah.

### Problem Statements

- Berdasarkan data mengenai daftar tempat wisata, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik *content-based filtering*?
- Apakah sistem rekomendasi ini dapat memudahkan pengguna dalam memilih tempat wisata yang paling relevan berdasarkan preference pengguna dengan teknik *collaborative filtering*?

### Goals

- Menghasilkan beberapa rekomendasi tempat wisata yang dipersonalisasi untuk pengguna dengan teknik *content-based filtering*.
- Menghasilkan rekomendasi tempat wisata yang relevan dengan pengguna berdasarkan *preference* pengguna lain pada data histori yang pernah dikunjungi oleh pengguna.

    ### Solution statements
    - Menggunakan dua teknik sistem rekomendasi yaitu *content based filtering* dan *collaborative filtering*

## Data Understanding
Link download dataset: https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination  

### Variabel-variabel pada dataset adalah sebagai berikut:

Dataset wisata pulau jawa pada dataset *tourism_rating.csv*:
- User_Id: *id* pengguna tersebut.
- Place_Id: *id* tempat wisata tersebut.	
- Place_Ratings: Rata-rata rating yang diberikan oleh pengguna ke tempat wisata tersebut.

Dataset wisata pulau jawa pada dataset *tourism_with_id.csv*:
- Place_Id: *id* tempat wisata tersebut.
- Place_Name: Nama tempat wisata tersebut.	
- Description: Deskripsi singkat tentang wisata tersebut.	
- Category: Kategori tempat wisata tersebut.	
- City: Kota dari tempat wisata tersebut. 	
- Price: Biaya yang harus dikeluarkan untuk mengunjungi tempat wisata tersebut.	
- Rating: Rata-rata rating yang diberikan oleh pengguna ke tempat wisata tersebut.
- Time_Minutes: Total waktu berdasarkan menit yang harus ditempuh pengguna untuk berkunjung ke tempat wisata tersebut dari tengah kota.	
- Coordinate: koordinat dari tempat wisata tersebut.	
- Lat: Latitude tempat wisata tersebut.	
- Long: Longitude tempat wisata tersebut.

#### tourism_rating.csv

Langkah pertama import *library* yang dibutuhkan untuk kasus kali ini:

*Library* yang akan diimport adalah *library* yang berhubungan untuk memanipulasi data, perhitungan matriks, teknik fitur ekstraksi, teknik untuk mencari hubungan antara fitur, menampilkan seluruh angka yang berada dibelakang koma, data visualisasi, *preprocessing*, model *machine learning* dan mematikan warning yang didapat setelah menjalankan code. 

### Exploratory Data Analysis:

Selanjutnya membaca dataset dan menampilkan 3 data random:

|      	| User_Id 	| Place_Id 	| Place_Ratings 	|
|-----:	|--------:	|---------:	|--------------:	|
| 2296 	|      71 	|      320 	|             1 	|
| 5277 	|     160 	|      292 	|             2 	|
|  62  	|       3 	|      310 	|             3 	|

> Dataset ini terdiri dari 10000 data dan 3 kolom.


| # 	| Column        	| Non-Null Count 	| Dtype 	|
|---	|---------------	|----------------	|-------	|
| 0 	| User_Id       	| 10000 non-null 	| int64 	|
| 1 	| Place_Id      	| 10000 non-null 	| int64 	|
| 2 	| Place_Ratings 	| 10000 non-null 	| int64 	|

Seluruh fitur pada dataset ini adalah integer atau numerik.

Dataset ini memiiliki total 300 pengguna berbeda dan total 437 tempat wisata berbeda


|       	|      User_Id 	|     Place_Id 	| Place_Ratings 	|
|------:	|-------------:	|-------------:	|--------------:	|
| count 	| 10000.000000 	| 10000.000000 	|  10000.000000 	|
|  mean 	|   151.292700 	|   219.416400 	|      3.066500 	|
|  std  	|    86.137374 	|   126.228335 	|      1.379952 	|
|  min  	|     1.000000 	|     1.000000 	|      1.000000 	|
|  25%  	|    77.000000 	|   108.750000 	|      2.000000 	|
|  50%  	|   151.000000 	|   220.000000 	|      3.000000 	|
|  75%  	|   226.000000 	|   329.000000 	|      4.000000 	|
|  max  	|   300.000000 	|   437.000000 	|      5.000000 	|

- Dapat dilihat bahwa rata-rata rating untuk tempat wisata sekitar 3.
- Dapat dilihat juga bahwa rating terendah untuk tempat wisata yaitu 1 dan rating tertinggi yaitu 5.

#### tourism_with_id.csv

Membaca dataset dan menampilkan 3 data random:

|     	| Place_Id 	|                        Place_Name 	|                                       Description 	|      Category 	|     City 	| Price 	| Rating 	| Time_Minutes 	|                                      Coordinate 	|      Lat 	|       Long 	| Unnamed: 11 	| Unnamed: 12 	|
|----:	|---------:	|----------------------------------:	|--------------------------------------------------:	|--------------:	|---------:	|------:	|-------:	|-------------:	|------------------------------------------------:	|---------:	|-----------:	|------------:	|------------:	|
|  48 	|       49 	|             Galeri Indonesia Kaya 	| Galeri Indonesia Kaya (disingkat GIK) adalah r... 	|        Budaya 	|  Jakarta 	|     0 	|    4.8 	|         90.0 	|         {'lat': -6.1948499, 'lng': 106.8200607} 	| -6.19485 	| 106.820061 	|         NaN 	|          49 	|
| 279 	|      280 	| Gereja Tiberias Indonesia Bandung 	| Gereja Tiberias Indonesia (GTI), atau Tiberias... 	| Tempat Ibadah 	|  Bandung 	|     0 	|    4.9 	|          NaN 	|         {'lat': -6.9347698, 'lng': 107.6253513} 	| -6.93477 	| 107.625351 	|         NaN 	|         280 	|
| 435 	|      436 	|      Taman Flora Bratang Surabaya 	| Taman Flora adalah salah satu taman kota di Su... 	| Taman Hiburan 	| Surabaya 	|     0 	|    4.6 	|          NaN 	| {'lat': -7.294330299999999, 'lng': 112.7617534} 	| -7.29433 	| 112.761753 	|         NaN 	|         436 	|

> Dataset ini terdiri dari 437 data dan 13 kolom.

| #  	| Column       	| Non-Null Count 	| Dtype   	|
|----	|--------------	|----------------	|---------	|
| 0  	| Place_Id     	| 437 non-null   	| int64   	|
| 1  	| Place_Name   	| 437 non-null   	| object  	|
| 2  	| Description  	| 437 non-null   	| object  	|
| 3  	| Category     	| 437 non-null   	| object  	|
| 4  	| City         	| 437 non-null   	| object  	|
| 5  	| Price        	| 437 non-null   	| int64   	|
| 6  	| Rating       	| 437 non-null   	| float64 	|
| 7  	| Time_Minutes 	| 205 non-null   	| float64 	|
| 8  	| Coordinate   	| 437 non-null   	| object  	|
| 9  	| Lat          	| 437 non-null   	| float64 	|
| 10 	| Long         	| 437 non-null   	| float64 	|
| 11 	| Unnamed: 11  	| 0 non-null     	| float64 	|
| 12 	| Unnamed: 12  	| 437 non-null   	| int64   	|

Fitur pada dataset ini terdiri dari 8 tipe numeric dan 5 tipe object.

Dataset ini memiiliki total 437 lokasi berbeda dan tempat wisata tersebut tersebar kedalam beberapa kota, sebagai berikut:

| Nama kota  	| Total 	|
|------------	|-------	|
| Yogyakarta 	| 126   	|
| Bandung    	| 124   	|
| Jakarta    	| 84    	|
| Semarang   	| 57    	|
| Surabaya   	| 46    	|

Dalam bentuk visualisasi data:

![2](https://user-images.githubusercontent.com/88027268/204716628-0d46241b-702a-41bf-a029-82e04745cc48.png)

Gambar 2. Distribusi lima kota dengan tempat wisatanya

Yogyakarta dan bandung menjadi kota dengan tempat wisata terbanyak pada dataset sekitar 124-126 tempat wisata lalu disusul kota Jakarta, semarang dan surabaya.

Berikut adalah kategori tempat wisata bersarkan kota asalnya:

![3](https://user-images.githubusercontent.com/88027268/204716844-b27280f7-3250-44a1-ac6b-b944b3d840bf.png)

Gambar 3. Distribusi enam kategori tempat wisata berdasarkan kotanya

- Dari visualisasi diatas Bandung adalah kota yang memiliki tempat wisata dengan kateogri cagar alam dan taman hiburan terbanyak dikota tersebut.
- Kota Jakarta memiliki tempat wisata dengan kateogri budaya dan taman hiburan terbanyak dikota tersebut.
- Kota Semarang memiliki sedikit atau bahkan tidak memiliki tempat wisata perbelanjaan dan cenderung memiliki banyak kategori tempat wisata dikota tersebut adalah Cagar alam, Budaya dan taman hiburan.
- Kota Surabaya memiliki tempat wisata dengan kategori taman hiburan dan budaya terbanyak dikota tersebut.
- Kota Yogyakarta memiliki data yang cukup signifikan pada kategori tempat wisata bahari dibanding kota lainnya.

|       	|   Place_Id 	|         Price 	|     Rating 	| Time_Minutes 	|        Lat 	|       Long 	| Unnamed: 11 	| Unnamed: 12 	|
|------:	|-----------:	|--------------:	|-----------:	|-------------:	|-----------:	|-----------:	|------------:	|------------:	|
| count 	| 437.000000 	|    437.000000 	| 437.000000 	|   205.000000 	| 437.000000 	| 437.000000 	|         0.0 	|  437.000000 	|
|  mean 	| 219.000000 	|  24652.173913 	|   4.442792 	|    82.609756 	|  -7.095438 	| 109.160142 	|         NaN 	|  219.000000 	|
|  std  	| 126.295289 	|  66446.374709 	|   0.208587 	|    52.872339 	|   0.727241 	|   1.962848 	|         NaN 	|  126.295289 	|
|  min  	|   1.000000 	|      0.000000 	|   3.400000 	|    10.000000 	|  -8.197894 	| 103.931398 	|         NaN 	|    1.000000 	|
|  25%  	| 110.000000 	|      0.000000 	|   4.300000 	|    45.000000 	|  -7.749590 	| 107.578369 	|         NaN 	|  110.000000 	|
|  50%  	| 219.000000 	|   5000.000000 	|   4.500000 	|    60.000000 	|  -7.020524 	| 110.237468 	|         NaN 	|  219.000000 	|
|  75%  	| 328.000000 	|  20000.000000 	|   4.600000 	|   120.000000 	|  -6.829411 	| 110.431869 	|         NaN 	|  328.000000 	|
|  max  	| 437.000000 	| 900000.000000 	|   5.000000 	|   360.000000 	|   1.078880 	| 112.821662 	|         NaN 	|  437.000000 	|

- Dapat dilihat bahwa rata-rata rating yang diberikan oleh pengguna ke tempat wisata tersebut yaitu 4.4 dan memberikan rating terendah yaitu 3.4 dan tertinggi yaitu 5.0.
- Dapat dilihat juga bahwa biaya masuk tempat wisata tersebut memiliki range harga sekitar 0 - 900k.
- Untuk kolom Unnamed: 11 dan Unnamed: 12 adalah kolom noise yang akan dibuang saat fase *data cleasing* 

### Data Preparation

## Content-based filtering

Melihat *missing value* pada dataset:

|        Kolom 	| Total 	| Percentage of Missing Values 	|
|-------------:	|------:	|-----------------------------:	|
|  Unnamed: 11 	|   437 	|                   100.000000 	|
| Time_Minutes 	|   232 	|                    53.089245 	|
|   Place_Id   	|     0 	|                     0.000000 	|
|  Place_Name  	|     0 	|                     0.000000 	|
|  Description 	|     0 	|                     0.000000 	|
|   Category   	|     0 	|                     0.000000 	|
|     City     	|     0 	|                     0.000000 	|
|     Price    	|     0 	|                     0.000000 	|
|    Rating    	|     0 	|                     0.000000 	|
|  Coordinate  	|     0 	|                     0.000000 	|
|      Lat     	|     0 	|                     0.000000 	|
|     Long     	|     0 	|                     0.000000 	|
|  Unnamed: 12 	|     0 	|                     0.000000 	|

> *Missing value* yang terjadi pada dataset dapat dihapus dengan menghapus kolomnya langsung pada feature selection.

#### Feature Selection
*Feature selection* adalah proses mengurangi jumlah fitur atau variabel input dengan memilih fitur-fitur yang dianggap paling relevan terhadap model agar mempermudah kinerja dari model tersebut.

- menghapus kolom Coordinate, Lat, Long, Unnamed: 11, Unnamed: 12, Time_Minutes, Rating dan Description karena tidak berguna dan dapat mengganggu pada saat dilakukan training.

## Collaborative filtering

#### tourism_rating.csv

Melihat *missing value* pada dataset:

|         Kolom 	| Total 	| Percentage of Missing Values 	|
|--------------:	|------:	|-----------------------------:	|
|    User_Id    	|     0 	|                          0.0 	|
|    Place_Id   	|     0 	|                          0.0 	|
| Place_Ratings 	|     0 	|                          0.0 	|

> Tidak ada nilai yang kosong pada dataset ini.

> Tidak ada data duplikat pada datatet

#### tourism_with_id.csv

|        Kolom 	| Total 	| Percentage of Missing Values 	|
|-------------:	|------:	|-----------------------------:	|
|  Unnamed: 11 	|   437 	|                   100.000000 	|
| Time_Minutes 	|   232 	|                    53.089245 	|
|   Place_Id   	|     0 	|                     0.000000 	|
|  Place_Name  	|     0 	|                     0.000000 	|
|  Description 	|     0 	|                     0.000000 	|
|   Category   	|     0 	|                     0.000000 	|
|     City     	|     0 	|                     0.000000 	|
|     Price    	|     0 	|                     0.000000 	|
|    Rating    	|     0 	|                     0.000000 	|
|  Coordinate  	|     0 	|                     0.000000 	|
|      Lat     	|     0 	|                     0.000000 	|
|     Long     	|     0 	|                     0.000000 	|
|  Unnamed: 12 	|     0 	|                     0.000000 	|

> *Missing value* yang terjadi pada dataset dapat dihapus dengan menghapus kolomnya langsung pada feature selection.

#### Feature Selection
*Feature selection* adalah proses mengurangi jumlah fitur atau variabel input dengan memilih fitur-fitur yang dianggap paling relevan terhadap model agar mempermudah kinerja dari model tersebut.

- menghapus kolom Coordinate, Lat, Long, Unnamed: 11, Unnamed: 12, Time_Minutes, Rating dan Description karena tidak berguna dan dapat mengganggu pada saat dilakukan training.

Setelah semua data telah dilakukan pembersihan maka dapat digabung menjadi satu dataframe dan hasilnya akan seperti ini:

| index 	| User_Id 	| Place_Id 	| Place_Ratings 	|      Place_Name 	| Category 	|       City 	| Price 	|
|------:	|--------:	|---------:	|--------------:	|----------------:	|---------:	|-----------:	|------:	|
|   0   	|       1 	|      179 	|           3.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|
|   1   	|      22 	|      179 	|           4.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|
|   2   	|      40 	|      179 	|           3.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|
|   3   	|      49 	|      179 	|           5.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|
|   4   	|      74 	|      179 	|           3.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|

Melakukan *Encode* valua pada kolom *User_Id* dan *Place_Id* kedalam angka integer dan hasilnya akan seperti ini:

| index 	| User_Id 	| Place_Id 	| Place_Ratings 	|      Place_Name 	| Category 	|       City 	| Price 	| user 	| place 	|
|------:	|--------:	|---------:	|--------------:	|----------------:	|---------:	|-----------:	|------:	|-----:	|------:	|
|   0   	|       1 	|      179 	|           3.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|    0 	|     0 	|
|   1   	|      22 	|      179 	|           4.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|    1 	|     0 	|
|   2   	|      40 	|      179 	|           3.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|    2 	|     0 	|
|   3   	|      49 	|      179 	|           5.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|    3 	|     0 	|
|   4   	|      74 	|      179 	|           3.0 	| Candi Ratu Boko 	|   Budaya 	| Yogyakarta 	| 75000 	|    4 	|     0 	|

Setelah berhasil melakukan *encode* pada fitur *User_Id* dan *Place_Id* maka langkah terakhir pada fase preprocessing yaitu pembagian untuk data training dan data testing.

Kolom yang akan digunakan sebagai independen variabel adalah fitur *User_Id* dan *Place_Id* lalu untuk fitur dependen yaitu *Place_Ratings*.

> Data untuk training sebesar 80% dan data untuk testing sebesar 20%.

## Modeling dan results

### Content-based filtering

*Content-based filtering* adalah sistem rekomendasi yang merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Jenis sistem rekomendasi ini menggunakan informasi tentang item untuk mempelajari preferensi pelanggan. Misal, jika pengguna A menyukai film *Koala Kumal*, maka sistem dapat merekomendasikan film dengan genre yang sama atau aktor yang sama. Contoh lain, saat berbelanja di e-commerce, sistem akan merekomendasikan item yang sama dengan yang telah pengguna lihat atau beli.

Kelebihan *content-based filtering*:
- Tidak memerlukan data apa pun dari pengguna lain dan hal itu dapat memudahkan pembuat sistem rekomendasi berbasis konten
- Model dapat mengetahui minat khusus dari pengguna sehingga model dapat merekomendasikan item yang sangat sedikit diminati pengguna lain
- Rekomendasi yang diberikan kepada pengguna adalah item yang paling relevan dengan pengguna tersebut.

Kekurangan *content-based filtering*:
- Model hanya dapat sebatas merekomendasikan item yang pengguna minat saja sehingga model tidak dapat memperluas minat berdasarkan pengguna lain.
- *Scalability*. Ketika terdapat item baru yang masuk kedalam daftar item maka harus diberi fitur yang digunakan sebagai acuan content based filtering agar model dapat merekomendasikan secara tepat
- *New user*. ketika data disuatu *profil* tidak banyak dan lengkap maka rekomendasi yang akan dihasilkan akan tidak akurat atau relevan.

Melakukan pemberian bobot pada fitur lokasi didataset menggunakan TF-IDF Vectorizer pada *library* sklearn. 

Selanjutnya setelah dilakukan perhitungan idf dapat dilanjutkan ke proses transformasi ke dalam bentuk matriks

> Matriks ini memiliki total 437 data dan 5 kota

Hasil matriks jika dalam bentuk dataframe:

|              City   	| jakarta 	| surabaya 	| bandung 	| semarang 	| yogyakarta 	|
|--------------------:	|--------:	|---------:	|--------:	|---------:	|-----------:	|
|          Place_Name 	|         	|          	|         	|          	|            	|
|       Goa Rong      	|     0.0 	|      0.0 	|     0.0 	|      1.0 	|        0.0 	|
| Hutan Pinus Pengger 	|     0.0 	|      0.0 	|     0.0 	|      0.0 	|        1.0 	|
|    Taman Begonia    	|     0.0 	|      0.0 	|     1.0 	|      0.0 	|        0.0 	|
|      Pulau Pari     	|     1.0 	|      0.0 	|     0.0 	|      0.0 	|        0.0 	|
|    Caringin Tilu    	|     0.0 	|      0.0 	|     1.0 	|      0.0 	|        0.0 	|
|  The Lodge Maribaya 	|     0.0 	|      0.0 	|     1.0 	|      0.0 	|        0.0 	|
| Wisata Kraton Jogja 	|     0.0 	|      0.0 	|     0.0 	|      0.0 	|        1.0 	|
|    Curug Bugbrug    	|     0.0 	|      0.0 	|     1.0 	|      0.0 	|        0.0 	|
|     Pantai Baron    	|     0.0 	|      0.0 	|     0.0 	|      0.0 	|        1.0 	|
|   Pantai Nguluran   	|     0.0 	|      0.0 	|     0.0 	|      0.0 	|        1.0 	|

Hasil diatas menunjukkan tempat wisata dengan lokasi yang benar akan diberi nilai 1 dan tempat wisata yang tidak sesuai dengan lokasi akan diberi nilai 0. sehingga data tempat wisata *Pulau Pari* Penida berlokasi di kota *Jakarta* diberi nilai 1, Karena hotel tersebut memang berlokasi di kota *Jakarta*.

Setelah melakukan pemberian bobot pada tiap fitur maka akan dilanjut ke tahap mengidentifikasi korelasi antara tempat wisata dan kotanya. untuk melakukan hal tersebut dapat menghitung derajat kesamaan atau similarity degree antar lokasi menggunakan teknik cosine similarity. Berikut adalah hasil perhitungan korelasinya:

|                   Place_Name 	| Curug Cilengkrang 	| Rumah Sipitung 	| Bandros City Tour 	| Pelabuhan Marina 	| Bukit Wisata Pulepayung 	|
|-----------------------------:	|------------------:	|---------------:	|------------------:	|-----------------:	|------------------------:	|
|                   Place_Name 	|                   	|                	|                   	|                  	|                         	|
|       Kawasan Malioboro      	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|
|         Pantai Timang        	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|
| Kauman Pakualaman Yogyakarta 	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|
|      Surabaya North Quay     	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     0.0 	|
|         Heha Sky View        	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|
|        Museum Perangko       	|               0.0 	|            1.0 	|               0.0 	|              1.0 	|                     0.0 	|
|       Pantai Ngrenehan       	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|
|          Bukit Jamur         	|               1.0 	|            0.0 	|               1.0 	|              0.0 	|                     0.0 	|
|        Pantai Ngandong       	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|
|   Taman Pelangi Yogyakarta   	|               0.0 	|            0.0 	|               0.0 	|              0.0 	|                     1.0 	|

Hasil dari perhitungan derajat kesamaan akan menghasilkan dimensi (437, 437) merupakan ukuran matriks similarity dari dataset dengan kata lain mesin berhasil mengidentifikasi 437 tempat wisata yang sama (masing-masing dalam sumbu X dan y). Sebagai contoh *Bukit Jamur* dengan *Curug Cilengkrang* memiliki nilai 1 yang berarti terdapat kemiripan lokasi kota. Untuk memastikan bahwa kedua tempat wisata tersebut memiliki kesamaaan, sebagai berikut:

|     	| Place_Id 	|        Place_Name 	|   Category 	|    City 	| Price 	|
|----:	|---------:	|------------------:	|-----------:	|--------:	|------:	|
| 321 	|      322 	|       Bukit Jamur 	| Cagar Alam 	| Bandung 	|     0 	|
| 281 	|      282 	| Curug Cilengkrang 	| Cagar Alam 	| Bandung 	|  7500 	|

Setelah semua tahap telah terselesaikan maka akan tiba saatnya membuat sebuah fungsi yang dimana pada fungsi tersebut akan mengembalikan 5 data tempat wisata teratas berdasarkan lokasi dari data histori pengguna. Berikut adalah rekomendasi misalnya pengguna sebelumnya mengunjungi *Surabaya North Quay*:

| index 	|                                Place_Name 	|     City 	|
|------:	|------------------------------------------:	|---------:	|
|     0 	| Gereja Perawan Maria Tak Berdosa Surabaya 	| Surabaya 	|
|     1 	|           Taman Ekspresi Dan Perpustakaan 	| Surabaya 	|
|     2 	|                             Kenjeran Park 	| Surabaya 	|
|     3 	|                      Kebun Bibit Wonorejo 	| Surabaya 	|
|     4 	|             Museum TNI AL Loka Jala Crana 	| Surabaya 	|

Data *Surabaya North Quay*:

| index 	| Place_Id 	|          Place_Name 	|      Category 	|     City 	| Price 	|
|------:	|---------:	|--------------------:	|--------------:	|---------:	|------:	|
|  404  	|      405 	| Surabaya North Quay 	| Taman Hiburan 	| Surabaya 	| 50000 	|

## Evaluation

Berdasarkan rekomendasi pada tahap *modeling dan results* dapat dilihat bahwa seluruh rekomendasi yang diberikan oleh model adalah yang berlokasi di kota *Surabaya* dan lokasi tersebut sesuai dengan data lokasi tempat wisata *Surabaya North Quay* yang diasumsikan sebagai data tempat wisata yang dikunjungi sebelumnya oleh pengguna.

Disini akan menggunakan metric precision sebagai acuan karena harapannya sistem rekomendasi dapat memberikan beberapa rekomendasi yang benar-benar relevan dengan data tempat wisata yang sebelumnya telah dikunjungi oleh pengguna

```math
Recall = \frac{Total-rekomendasi-yang-relevan}{Total-rekomendasi-yang-diberikan}
```

Penjelasan dari formula diatas:
- Total-rekomendasi-yang-relevan berarti sistem rekomendasi berhasil memberikan rekomendasi yang relevan dengan data tempat wisata yang sebelumnya dikunjungi oleh pengguna.
- Total-rekomendasi-yang-diberikan berarti jumlah rekomendasi yang telah diberikan oleh sistem kepada pengguna tanpa memikirkan apakah rekomendasi itu relevan atau tidak. 

```math
Recall = \frac{5}{5} = 1.00
```

Dari hasil perhitungan diatas sistem rekomendasi yang telah dibuat mencapai score 1.00 atau sempurna berhasil memberikan rekomendasi yang relevan kepada pengguna.

### Collaborative filtering

*Collaborative filtering* bekerja mengidentifikasi pola serupa dalam perilaku pelanggan dan merekomendasikan item yang telah berinteraksi dengan pelanggan serupa lainnya. jenis rekomendasi ini dibagi menjadi kedalam dua bagian yaitu: *model based* (metode berbasis model machine learning) dan *memory based* (metode berbasis memori).

Kelebihan *Collaborative filtering*:
- Tidak membutuhkan *domain knowledge* karena sistem yang akan mencari pola dari pengguna satu dengan pengguna lainnya berdasarkan kemiripan antar pengguna tersebut.
- Sistem dapat menemukan minat atau kesukaan baru dari pengguna karena sistem dapat merekomendasikan item dari pengguna lain yang mungkin tidak pernah dilihat dan setelah dilihat pengguna tersebut menyukainya.

Kekurangan *Collaborative filtering*:
- Tidak dapat memberikan rekomendasi item baru jika belum dilakukan pelatihan ulang dengan menambahkan item baru tersebut kedalam fase pelatihan.
- *Dataset* yang dibutuhkan cukup besar karena menggunakan *machine learning* atau bahkan *deep learning*

Setelah melakukan data preprocessing maka akan dilanjut ketahap modeling menggunakan tensorflow. Ditahap ini model akan menghitung kecocokan antara pengguna dan tempat wisata dengan teknik embedding. Proses pertama yang akan dilakukan adalah melakukan embedding terhadap data user dan tempat wisata. lalu melakukan proses operasi perkalian dot product antara embedding user dan tempat wisata. Disetiap perhitungan embedding akan ditambahkan juga bias untuk data user dan tempat wisata. Hasil akhir dari model ini adalah 0 dan 1 dikarenakan menggunakan fungsi aktivasi sigmoid yang mana fungsi aktivasi tersebut akan menghasilkan dua nilai saja yaitu 0 dan 1.

Selanjutnya membuat proses compile terhadap model dengan kriteria menggunakan loss fungsi yaitu *MeanSquaredError*, optimizer yaitu *Adagrad* dengan *learning_rate* 0.01 dan metrik evaluasi yaitu *RMSE*.

Formula *MeanSquaredeError*:

```math
\frac{1}{n}\sum_{i=1}^{n}(\hat{y} - y)^2 
```

penjelasan:
- Σ adalah total dari perhitungan nilai yang ada didalam kurung
- y hat adalah nilai yang diprediksi oleh model
- y adalah nilai yang sebenarnya
- n adalah *sample size*

Penjelasan *Adagrad*: Algoritme ini secara adaptif menskalakan *learning_rate* untuk setiap dimensi.

Formula *MeanSquaredeError*:

```math
\sqrt{\sum_{i=1}^{n} \frac{(\hat{y} - y)^2}{n}}
```

penjelasan:
- √ adalah akar dari nilai yang ada didalam akar tersebut
- Σ adalah total dari perhitungan nilai yang ada didalam kurung
- y hat adalah nilai yang diprediksi oleh model
- y adalah nilai yang sebenarnya
- n adalah *sample size*

Langkah terakhir fase ini adalah melakukan training pada data train dan data test dengan epochs yaitu 10 dan batch_size = 24.

Setelah semua tahap telah terselesaikan maka akan tiba saatnya membuat *testing* rekomendasi untuk salah satu pengguna. misalkan untuk pengguna dengan *User_Id* 201. Berikut adalah rekomendasi yang akan diberikan:

| Showing recommendations for users: 201     	|
|--------------------------------------------	|
| ===========================                	|
| Place with high ratings from user          	|
| --------------------------------           	|
| Hutan Pinus Kayon : Semarang               	|
| Curug Aseupan : Bandung                    	|
| Kebun Binatang Bandung : Bandung           	|
| Monumen Serangan Umum 1 Maret : Yogyakarta 	|
| Glamping Lakeside Rancabali : Bandung      	|
| --------------------------------           	|
| Top 10 place recommendation                	|
| --------------------------------           	|
| Panama Park 825 : Bandung                  	|
| Bumi Perkemahan Batu Kuda : Bandung        	|
| Museum Barli : Bandung                     	|
| Sudut Pandang Bandung : Bandung            	|
| Situ Patenggang : Bandung                  	|
| Teras Cikapundung BBWS : Bandung           	|
| Taman Vanda : Bandung                      	|
| Bukit Bintang : Bandung                    	|
| Museum Gedung Sate : Bandung               	|
| Monumen Bandung Lautan Api : Bandung       	|

## Evaluation

Setelah melakukan modeling dapat melakukan visualisasi score dari metrik yang telah dihitung pada fase training.

> Model berhasil mendapatkan *RMSE* pada data training yaitu 0.3446 dan pada validasi yaitu 0.3434. Hasil tersebut cukup bagus untuk sistem rekomendasi.

Kesimpulan: Pulau jawa merupakan pulau yang sering untuk dikunjungi turis dan untuk memudahkan turis dalam memilih tempat wisata apa saja yang mungkin relevan dengan pengguna tersebut berdasarkan kota yang pernah dikunjungi menggunakan teknik *content-based filtering* atau berdasarkan *preference* pengguna lain yang menyukai tempat wisata tersebut menggunakan teknik *collaborative filtering*. Proyek ini berhasil memberikan rekomendasi kepada pengguna yang mungkin relevan dengannya dan akurasi yang didapat pada teknik *content-based filtering* yaitu 1.00 atau sangat akurat lalu pada teknik *collaborative filtering* yaitu 0.34 yang mana akurasi tersebut sudah cukup baik.

Reference: [(Charilaos Zisopoulos, Savvas Karagiannidis, Georgios Demirtsoglou and Stefanos Antaris, 2008)](https://www.researchgate.net/publication/236895069_Content-Based_Recommendation_Systems) dan [(Hael Al-bashiri, Mansoor Abdullateef Abdulgabber, Awanis Romli and Fadhl Hujainah, 2017)](https://www.researchgate.net/publication/320761149_Collaborative_Filtering_Recommender_System_Overview_and_Challenges#:~:text=This%20paper%20is%20to%20present%20an%20overview%20of,help%20users%20to%20overcome%20the%20information%20overload%20issue.), 

**---END---**
