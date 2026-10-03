Klasterisasi Game Steam: K-Means vs K-Medoids

Segmentasi game di platform Steam berdasarkan popularitas, harga, dan waktu bermain, sekaligus membandingkan algoritma K-Means dengan K-Medoids (FasterPAM). Proyek ini adalah skripsi S1 Informatika, Universitas Muhammadiyah Sidoarjo (UMSIDA).

Preprint: A Comparative Analysis of K-Means and K-Medoids Algorithms for Steam Game Clustering Based on Popularity, Price, and Playtime 🔗 DOI: 10.21070/ups.11841

Latar Belakang

Katalog Steam sangat besar dan beragam. Genre saja tidak cukup untuk menggambarkannya, karena dua game dengan genre sama bisa sangat berbeda dalam jangkauan pasar, harga, dan keterlibatan pemain. Proyek ini mengelompokkan game dengan tiga fitur numerik, lalu menguji algoritma mana yang memberi representasi segmen terbaik.

Dataset
Sumber: Steam Games Dataset (Kaggle: fronkongames/steam-games-dataset)
Data mentah: 136.080 entri
Setelah penyaringan 4 tingkat: 22.659 game yang memenuhi syarat
Fitur klasterisasi:
estimated_owners_numeric (popularitas)
price (harga)
average_playtime_forever (waktu bermain)

Alur Metodologi
Akuisisi data: unduh dataset dan kunci snapshot mentah.
Penyaringan bertingkat (Level 1-4): 136.080 → 22.659 data.
EDA: distribusi dan kemencengan (skewness) tiap fitur.
Pra-pemrosesan: transformasi Yeo-Johnson (PowerTransformer) dilanjutkan StandardScaler.
Penentuan K optimal: evaluasi K = 2 sampai 10 dengan Silhouette Score dan Davies-Bouldin Index. K = 3 dipilih karena Silhouette tertinggi.
Pemodelan: K-Means vs K-Medoids (FasterPAM).
Profiling dan pelabelan klaster, divalidasi dengan uji Kruskal-Wallis.
Visualisasi: PCA 2D, diagram silhouette, boxplot per klaster, radar chart, dan scatter 3D.

Setiap tahap disimpan sebagai checkpoint CSV beserta log dan manifest, sehingga alur kerjanya dapat ditelusuri dan direproduksi.

Hasil Utama
Perbandingan algoritma (K = 3)
Model	Silhouette	Davies-Bouldin	Distribusi klaster (0 / 1 / 2)
K-Means	0,2913	1,1234	6.864 / 7.112 / 8.683
K-Medoids (FasterPAM)	0,2922	1,1493	7.179 / 7.672 / 7.808

K-Medoids sedikit unggul pada Silhouette dan menghasilkan distribusi klaster yang lebih seimbang, sehingga dipilih sebagai model utama. Nilai Davies-Bouldin-nya memang sedikit lebih tinggi daripada K-Means.

Tiga segmen game
Klaster	Label	Rata-rata pemilik	Rata-rata harga	Rata-rata playtime	Proporsi
0	Popular-Premium-High Engagement	760.647	9,92	2.238,40	31,68%
1	Budget / F2P	288.355	1,17	369,05	33,86%
2	Niche-Low Engagement	13.734	6,15	230,01	34,46%

Uji Kruskal-Wallis menunjukkan perbedaan yang signifikan antar klaster pada ketiga fitur.

Cara Menjalankan
Buka notebook di Google Colab. Gunakan tombol Open in Colab di bagian atas notebook.
Jalankan sel dari atas ke bawah. Sel pertama memasang pustaka tambahan (kmedoids, tabulate, kaggle).
Izinkan akses Google Drive saat diminta. Checkpoint dan output disimpan di Drive pada folder skripsi_steam/.
