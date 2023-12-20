![Flow Project](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/twit_cov19.jpg) <br>

# **Latar Belakang Penelitian**

Dalam pesatnya perkembangan era digital dan sosial media, informasi menyebar sangat cepat, terutama terkait dengan isu-isu kesehatan seperti pandemi COVID-19 yang telah kita lalui. Masyarakat seringkali membagikan opini, berita, atau informasi terkait COVID-19 melalui media sosial seperti twitter. Maka dengan memahami dan mengklasifikasikan tweet yang ditulis masyarakat harapannya dapat memberikan wawasan yang berharga terkait sentimen dan pandangan masyarakat terhadap pandemi.

Penting untuk memahami bagaimana masyarakat merespons COVID-19, apakah dengan kekhawatiran, harapan, atau bahkan disertai dengan informasi yang mengada ada (hoax). Klasifikasi tweet tentang COVID-19 dapat membantu mendeteksi pola-pola tertentu dan mengidentifikasi tren dalam percakapan online.

Dalam penelitian yang dilakukan oleh sejumlah ahli komunikasi, analisis sentimen terhadap isu-isu kesehatan masyarakat dapat memberikan gambaran tentang dampak sosial dan psikologis dari pandemi. Melalui proyek klasifikasi tweet tentang COVID-19 yang saya coba bangun ini, diharapkan dapat diperoleh pemahaman yang lebih dalam terkait respons dan pandangan masyarakat melalui media sosial selama pandemi. Hal ini dapat memberikan manfaat bagi pihak-pihak terkait, seperti peneliti, lembaga kesehatan, dan pemerintah, dalam merespon dan mengelola isu-isu kesehatan masyarakat dengan lebih efektif.

## **Alur Pengerjaan Proyek**
![Flow Project](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/flow-tweet-baru.png) <br>

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
So, Long Short-Term Memory (LSTM) adalah salah satu jenis RNN. RNN sendiri adalah jenis arsitektur dari neural network yang dirancang untuk menangani case data berbasis sekuensial(urutan). Data sekuensial ini sederhananya dimana terdapat suatu data yang mana urutan pada data sebelumnya memberi dampak informasi pada data selanjutnya. Dalam konteks tweet classification ini tentunya tweet dapat dianggap sebagai data sekuensial yang mana frasa yang muncul sebelumnya dapat memengaruhi konteks makna secara kesuluruhan.
##### Gambaran Umum Arsitektur
LSTM pertama kali dicetuskan oleh Hochreiter & Schmidhuber (1997) dan hingga kini masih banyak digunakan dan dikembangkan oleh banyak researcher. LSTM sendiri merupakan modifikasi dari RNN dengan memiliki gerbang(gate) yang lebih beragam. Dimana LSTM memiliki 3 gate utama yaitu: forget gate, input gate, dan output gate. Penjelasan singkat:
- Forget Gate <br>
![Architecture LSTM](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/forget.png) <br>

    - Jadi input akan menerima berupa konteks(time step) sebelumnya  \$`C_{t-1}`$ di input saat ini \$`x_t`$ 
    - Berikutnya dengan menghitung nilai sigmoid pada setiap elemen dalam \$`C_{t-1}`$ dengan menggunakan formula $f_t=\sigma\left(W_f \cdot\left[h_{t-1}, x_t\right]+b_f\right)$ , dimana \$`W_f`$ adalah bobot, adalah fungsi \$`\sigma`$ sigmoidnya, \$`\cdot`$ adalah operasi dot product antara weight dan hidden state serta langkah waktu pada t saat ini , serta  \$`b_f`$ adalah nilai dari  biasnya
    - Dari sini tentunya kita bisa menentukan elemen mana yang akan dibuang atau dipertahankan, dengan \$`f_t`$ mendekati 1 informasi akan tetap dipertahankan dan sebaliknya.
- Input Gate <br>
![Architecture LSTM](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/input.png) <br>

    - Setelah menerima input berupa konteks sebelumnya di \$`C_{t-1}`$
    - Kita akan menghitung nilai sigmoid(\$`i_t`$) dan kandidat vektor baru (\$`\tilde{C}_t`$) menggunakan formula $i_t=\sigma\left(W_i \cdot\left[h_{t-1}, x_t\right]+b_i\right)$ dan
      $`\tilde{C}_t=\sigma\left(W_i \cdot\left[h_{t-1}, x_t\right]+b_c\right)`$
    - Dari output \$i_t$ kita dapat menentukan seberapa banyak nilai yang akan diperbarui
- Context Update <br>
![Architecture LSTM](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/context.png) <br>

    - Dengan menggunakan nilai dari forget gate(\$f_t$) kita akan memutuskan elemen mana dari konteks sebelumnya \$`C_{t-1}`$ yang akan dibuang
    - Dengan menggunakan nilai dari input gate(\$i_t$) kita akan memutuskan seberapa kandidat vektor baru($`\tilde{C}_t`$) yang akan disertakan  
    - Pembaruan konteks dapat dilakukan dengan formula seperti ini $C_t=f_t \cdot C_{t-1}+i_t \cdot \tilde{C}_t$
- Output Gate <br>
![Architecture LSTM](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/output.png) <br>

    - Akhirnya kita sampai ke gate terakhir, di gate ini serupa dengan gate gate sebelumnya input akan menerima konteks sebelumnya  di \$`C_{t-1}`$
    - lalu menghitung nilai sigmoid (\$`o`$) untuk menentukan bagian mana dari konteks yang akan dihasilkan dengan formula $o_t=\sigma\left(W_i \cdot\left[h_{t-1}, x_t\right]+b_o\right)$
    - Terakhir output $`h_t`$ akan digenerate dengan mengalikan nilai tanh dari konteks saat ini dengan formula \$`h_t = o_t*tanh(C_t)`$

<br>Terlihat memusingkan wkwk? 😖 <br>
Baik disini saya akan coba menjelaskan tanpa menggunakan formula, intinya secaara sederhana `LSTM layaknya seorang penjaga perpustakaan`. dimana forget gate diibaratkan penjaga tsb melihat beberapa buku yang sudah tidak relevan dimana buku tersebut akan dibuang dan mempertahankan buku buku yang lebih populer saat ini. Berikutnya untuk input gate, ini layaknya penjaga tsb kedatangan buku baru yang mana dia mendecide apakah buku tersebut akan ditambahkan ke perpustakaannya atau tidak? jika dianggap relevan maka dia akan menambahkannya. Berikutnya Cell State ini seperti catatan terorganisir dari penjaga perpus tsb mencakup detail buku yang telah ditambahkan atau dihapus. Dan yang terakhir untuk Output Gate, ketika ada seseorang yang ingin meminjam buku, penjaga perpus tsb memberikan informasi yang dia simpan tadi untuk merekomendasikan ke peminjam tsb.  
#### 4.2 GRU Approach
##### Gambaran Umum Arsitektur
GRU pertama kali diperkenalkan pada paper yang diangkat oleh Cho dkk (2014) dan Chung dkk (2014). Perbedaan arsitektur ini dibannding LSTM adalah lebih simpel dan efisiend dimana GRU memiliki satu cell memori saja, disini GRU mengintegrasikan forget gate dan input gate menjadi satu gate saja yang disebut reset gate. Sehingga pendekatan ini dapat mengurangi kompleksitas dan jumlah parameter yang perlu dikalkulasi. Dari alasan alasan tsb tentunya kita dapat memilih GRU sebagai pilihan saat hanya memiliki sumber daya komputasi yang terbatas.Penjelasan singkat:

![Architecture LSTM](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/resetGRU.png) <br>
- Reset Gate <br>
    - Disini kita menentukan sejauh mana kita akan "melupakan" konteks sebelumnya (\$`C _{t−1}`$).
    - Dengan menggunakan fungsi sigmoid untuk menghasilkan $r_t=\sigma\left(W_r \cdot\left[C_{t-1}, x_t\right]+b_r\right)$  dimana \$`W_r`$ adalah bobot, adalah fungsi \$`\sigma`$ sigmoidnya, \$`\cdot`$ adalah operasi dot product antara weight dan cell state serta langkah waktu pada t saat ini , serta  \$`b_r`$ adalah nilai dari  biasnya
- Update Gate <br>
    - Kita akan enentukan sejauh mana konteks sebelumnya \$`C_{t-1}`$ akan diupdate dengan konteks yang baru $`\tilde{C}_t`$
    - Berikutnya menggunakan fungsi sigmoid untuk mengenerate $u_t=\sigma\left(W_u \cdot\left[C_{t-1}, x_t\right]+b_u\right)$

<br>Yang sekiranya masih kesulitan untuk memahami, hampir serupa dengan LSTM untuk analoginya, jadi ada penjaga perpustakaan tetapi disini penjaga perpus hanya melakukan penghapusan catatan buku buku yang dianalogikan dengan reset gate, serta melakukan penambahan catatan baru yang menciptakan cell state yang dianalogikan sebagai update gate.
  
#### 4.3 DistilBERT Approach
Kita masuk ke approach terakhir dari penelitian ini yakni menggunakan DistilBERT, sebelum menyelam lebih jauh ke arsitekur ini ada baiknya kita menyinggung terlebih dahulu konsep dari Transformers. Transformers sendiri adalah salah saty arsitektur neural network yang dikembangkan oleh Google Brain pada tahun 2017. Berbeda dengan pendekatan sebelumnya disini transformers memperkenalkan mekanisme attention (perhatian 💕) untuk memproses input sekuensial. Transformers telah menjadi banyak pondasi model SOTA yang berkembang di sekitar kita seperti LLaMA, Falcon, dan GPT. Arsitektur ini menjawab keterbatasan yang dimiliki model sekuensial sebelumnya seperti LSTM dan GRU. 
##### Gambaran Umum Arsitektur
![Flow Project](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/BERT.png) <br>

- Encoder adalah komponen dari transformers yang bertanggung jawab untuk memproses input dan menghasilkan representasi dari internal dari input, representasi inilah yang nantinya akan digunakan oleh decoder menghasilkan output. Encoder sendiri terdiri dari beberapa lapisan seperti:
  - Embedding layer, lapisan ini akan mengubah suatu input menjadi representasi vektor yang mempunyai panjang yang sama untuk setiap input
  - Multi head attention layer, lapisan ini memungkinkan encoder untuk "memperhatikan" semua input secara bersamaan
  - Feed forward layer, lapisan ini menerapkan fungsi aktivasi pada output dari multi head attention layer
  
- Decoder adalah komponen dari transformer yang bertanggung jawab untuk menghasilkan output dari representasi internal yang dihasilkan oleh encoder. Decoder serupa dengan encoder yang memiliki 3 lapisan penting seperti yang sudah dijelaskan sebelumnya. Berikutnya ada teknik seperti Positional Encoding dan Masked Head Attemtion. Untuk postional encoding, teknik ini digunakan untuk memberikan informasi tentang posisi input ke encoder dan decoder. Informasi ini penting untuk tugas-tugas yang membutuhkan pemahaman tentang urutan sekuensial. Lalu Masked self attention adalah teknik yang digunakan untuk mencegah decoder memperhatikan outputnya sendiri. Teknik ini penting yang mana dapat mencegah decoder dari menghasilkan output yang tidak konsisten.

![Flow Project](https://github.com/RidwendDev/Tweet-Classification-Coronavirus/raw/main/asset/distilBERT.png) <br>

Nah setelah memahami konsep dari Transformers, disini kita akan menyelam ke DistilBERT. `DistilBERT ini merupakan konsep dari Distillation yang mana konteks ini mengacu pada proses transfer knowladge dari teacher model(model besar) yaitu BERT ke student model(model kecil) yaitu DistilBERT.` Tujuan utamanya adalah mengajarkan model yang lebih kecil untuk meniru distribusi output dari model yang lebih besar. Pada proses distilaasi tersebut student model ditrain menggunakan distribusi probabilitas(soft targets) yang dihasilkan oleh teacher model. Hal ini menjadikan student model memahami distribusi probabilitas dan knowladge yang lebih kaya. Untuk hasil komparasi evaluasi dari BERT dan DistilBERT ditunjukkan pada tabel berikut. 
| **Aspek**                                       | **BERT**                                              | **DistilBERT**                                        |
|------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------|
| **Pemahaman Bahasa dan Kemampuan Generalisasi** | Unggul dalam menangkap konteks dua arah.              | Tetap memiliki performa tinggi dengan ukuran 40% lebih kecil.   |
| **Performa pada Tugas-Tugas Turunan**             | Meraih akurasi tinggi pada berbagai uji benchmark.    | Sedikit kalah dari BERT pada beberapa tugas, misalnya IMDb, dengan ukuran lebih kecil.|
| **Kompromi Kecepatan/Ukuran**                    | Mahal secara komputasional, memiliki banyak parameter. | 40% lebih sedikit parameter dan sekitar 60% lebih cepat dalam inferensi.  |
| **Komputasi On-device**                          | Tantangan karena ukuran model besar dan kebutuhan sumber daya. | Lebih efisien di perangkat, 71% lebih cepat pada aplikasi seluler (iPhone 7 plus). Dengan ukuran model hanya: 207 MB.  |



### 5. Performance Evaluation




