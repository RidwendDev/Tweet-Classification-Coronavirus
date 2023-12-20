# **Latar Belakang Penelitian**

Dalam pesatnya perkembangan era digital dan sosial media, informasi menyebar sangat cepat, terutama terkait dengan isu-isu kesehatan seperti pandemi COVID-19 yang telah kita lalui. Masyarakat seringkali membagikan opini, berita, atau informasi terkait COVID-19 melalui media sosial seperti twitter. Maka dengan memahami dan mengklasifikasikan tweet yang ditulis masyarakat harapannya dapat memberikan wawasan yang berharga terkait sentimen dan pandangan masyarakat terhadap pandemi.

Penting untuk memahami bagaimana masyarakat merespons COVID-19, apakah dengan kekhawatiran, harapan, atau bahkan disertai dengan informasi yang mengada ada (hoax). Klasifikasi tweet tentang COVID-19 dapat membantu mendeteksi pola-pola tertentu dan mengidentifikasi tren dalam percakapan online.

Dalam penelitian yang dilakukan oleh sejumlah ahli komunikasi, analisis sentimen terhadap isu-isu kesehatan masyarakat dapat memberikan gambaran tentang dampak sosial dan psikologis dari pandemi. Melalui proyek klasifikasi tweet tentang COVID-19 yang saya coba bangun ini, diharapkan dapat diperoleh pemahaman yang lebih dalam terkait respons dan pandangan masyarakat melalui media sosial selama pandemi. Hal ini dapat memberikan manfaat bagi pihak-pihak terkait, seperti peneliti, lembaga kesehatan, dan pemerintah, dalam merespon dan mengelola isu-isu kesehatan masyarakat dengan lebih efektif.

## **Alur Pengerjaan Proyek**
![Flow Project](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/flow-tweet.png) <br>

### 1. Data Exploration

Pertama, disini saya melakukan eksplorasi data untuk memahami karakteristik dataset tweet COVID-19. Adapun part yang dilakukan sebagai berikut.
- Analisis statistik deskriptif dataset.
- Identifikasi distribusi target pada data.
- Visualisasi tren dan pola waktu memposting tweet terkait COVID-19.
- Visualisasi wordcloud untuk setiap target pada data.

### 2. Data Cleaning

Berikutnya melakukan pembersihan data untuk memastikan kualitas data yang baik. 

- Melakukan penghapusan URL
- Melakukan penghapusan mentions
- Melakukan penghapusan hastags
- Melakukan penghapusan digit
- Melakukan penghapusan tag html
- Melakukan penghapusan emoji
- Melakukan penghapusan punctuation
- Melakukan penghapusan special characters
- Melakukan penghapusan stopwords


### 3. Data Splitting

Disini saya membagi dataset menjadi subset pelatihan (train) dan pengujian (test) untuk melatih dan menguji model. Dengan porsi dari train adalah 80% dan test 20%.

### 4. Modeling

#### 4.1 LSTM Approach



#### 4.2 GRU Approach


  
#### 4.3 DistilBERT Approach



### 5. Performance Evaluation




