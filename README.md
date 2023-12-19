# **Latar Belakang Penelitian**

Dalam pesatnya perkembangan era digital dan sosial media, informasi menyebar sangat cepat, terutama terkait dengan isu-isu kesehatan seperti pandemi COVID-19 yang telah kita lalui. Masyarakat seringkali membagikan opini, berita, atau informasi terkait COVID-19 melalui media sosial seperti twitter. Maka dengan memahami dan mengklasifikasikan tweet yang ditulis masyarakat harapannya dapat memberikan wawasan yang berharga terkait sentimen dan pandangan masyarakat terhadap pandemi.

Penting untuk memahami bagaimana masyarakat merespons COVID-19, apakah dengan kekhawatiran, harapan, atau bahkan disertai dengan informasi yang mengada ada (hoax). Klasifikasi tweet tentang COVID-19 dapat membantu mendeteksi pola-pola tertentu dan mengidentifikasi tren dalam percakapan online.

Dalam penelitian yang dilakukan oleh sejumlah ahli komunikasi, analisis sentimen terhadap isu-isu kesehatan masyarakat dapat memberikan gambaran tentang dampak sosial dan psikologis dari pandemi. Melalui proyek klasifikasi tweet tentang COVID-19 yang saya coba bangun ini, diharapkan dapat diperoleh pemahaman yang lebih dalam terkait respons dan pandangan masyarakat melalui media sosial selama pandemi. Hal ini dapat memberikan manfaat bagi pihak-pihak terkait, seperti peneliti, lembaga kesehatan, dan pemerintah, dalam merespon dan mengelola isu-isu kesehatan masyarakat dengan lebih efektif.

## **Alur Pengerjaan Proyek**
![Flow Project](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/flow-tweet.png) <br>

### 1. Data Exploration

Pertama, disini saya melakukan eksplorasi data untuk memahami karakteristik dataset tweet COVID-19. Lakukan langkah-langkah berikut:
- Analisis statistik deskriptif dataset.
- Identifikasi distribusi target pada data.
- Visualisasi tren dan pola waktu memposting tweet terkait COVID-19.
- Visualisasi wordcloud untuk setiap target pada data.

### 2. Data Cleaning

Lakukan pembersihan data untuk memastikan kualitas data yang baik. Lakukan langkah-langkah berikut:

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

Bagi dataset menjadi subset pelatihan (train) dan pengujian (test) untuk melatih dan menguji model. Dengan porsi dari train adalah 80% dan test 20%.

### 4. Modeling

#### 4.1 DistilBERT Approach

- Lakukan tokenisasi menggunakan DistilBERT tokenizer.
- Bangun dan latih model klasifikasi menggunakan DistilBERT.
- Tentukan arsitektur model, hyperparameter, dan langkah-langkah pelatihan.

#### 4.2 LSTM Approach

- Lakukan tokenisasi dan padding menggunakan LSTM.
- Bangun dan latih model klasifikasi menggunakan arsitektur LSTM.
- Tentukan arsitektur model, hyperparameter, dan langkah-langkah pelatihan.

#### 4.3 GRU Approach

- Lakukan tokenisasi dan padding menggunakan GRU.
- Bangun dan latih model klasifikasi menggunakan arsitektur GRU.
- Tentukan arsitektur model, hyperparameter, dan langkah-langkah pelatihan.

### 5. Performance Evaluation

Evaluasikan kinerja masing-masing model menggunakan metrik yang sesuai seperti akurasi, presisi, recall, dan F1-score. Lakukan langkah-langkah berikut:

- Evaluasi masing-masing model pada subset pengujian.
- Bandingkan hasil evaluasi untuk menentukan model terbaik.


