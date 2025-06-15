# Tugas_W15_probstat
## Kelompok 4 Probabilitas dan Statistik B
- Ahmad Fadhilah Mappisara (5025221195)
- Almira Fidela Soehartanto Putri (5025221222)
- Muhammad Detri Abdul Fikar (5025221236)
- Garda Sudarmanto (5025221268)
## Analisis ANOVA
ANOVA adalah metode statistik yang digunakan untuk menentukan apakah terdapat perbedaan signifikan antara rata-rata dari tiga kelompok atau lebih. Metode ini membantu memahami bagaimana satu variabel independen memengaruhi variabel dependen secara signifikan. Ada tiga jenis ANOVA:
- _One-Way ANOVA_.
- _Two-Way ANOVA_.
- _Repeated Measures ANOVA_ untuk data longitudinal atau berulang.
## Studi Kasus 1
# **studi kasus one way**

Masalah: Seorang guru ingin mengetahui apakah ada perbedaan rata-rata nilai 
ujian dari tiga kelas berbeda (Kelas A, Kelas B, dan Kelas C). Nilai ujian dari 
tiap kelas dicatat dan diuji dengan ANOVA.


import numpy as np
import pandas as pd
import scipy.stats as stats
import matplotlib.pyplot as plt
import seaborn as sns

# Nilai ujian dari tiga kelas
kelas_A = [78, 85, 82, 90, 76]
kelas_B = [88, 79, 92, 85, 87]
kelas_C = [84, 83, 85, 86, 82]
df = pd.DataFrame({
    'Nilai': kelas_A + kelas_B + kelas_C,
    'Kelas': ['A']*len(kelas_A) + ['B']*len(kelas_B) + ['C']*len(kelas_C)
})


plt.figure(figsize=(8, 6))
sns.boxplot(x='Kelas', y='Nilai', data=df)
plt.title('Bdistribusi nilai')
plt.xlabel('Kelas')
plt.ylabel('Nilai')
plt.show()


# Statistik deskriptif per kelompok
df.groupby('Kelas').describe()

# **Uji ANOVA**

Menggunakan fungsi f_oneway dari scipy.stats, kita menghitung:

F-value: Statistik uji ANOVA

P-value: Probabilitas bahwa perbedaan rata-rata antar kelompok terjadi secara kebetulan

Interpretasi:

Jika p-value < 0.05, maka terdapat perbedaan signifikan secara statistik di antara kelompok.

# Lakukan uji ANOVA satu arah
f_value, p_value = stats.f_oneway(kelas_A, kelas_B, kelas_C)

print(f"F-Value (Statistik ANOVA): {f_value:.4f}")
print(f"P-Value: {p_value:.4f}")

**interpertensi hasil**
- **F-value** adalah statistik uji dari ANOVA.
- **P-value** menunjukkan apakah perbedaan antar rata-rata kelompok signifikan secara statistik.
- Jika **p-value < 0.05**, maka kita menyimpulkan bahwa **setidaknya ada satu kelompok yang berbeda secara signifikan** dari yang lain.


# Uji T untuk membandingkan pasangan kelompok
ttest_AB = stats.ttest_ind(kelas_A, kelas_B)
ttest_AC = stats.ttest_ind(kelas_A, kelas_C)
ttest_BC = stats.ttest_ind(kelas_B, kelas_C)

print(f"T-test A vs B: t = {ttest_AB.statistic:.4f}, p = {ttest_AB.pvalue:.4f}")
print(f"T-test A vs C: t = {ttest_AC.statistic:.4f}, p = {ttest_AC.pvalue:.4f}")
print(f"T-test B vs C: t = {ttest_BC.statistic:.4f}, p = {ttest_BC.pvalue:.4f}")

## Studi Kasus 2
### **studi kasus two-way anova**

**Masalah:**  
Sebuah perusahaan ingin mengetahui apakah skor tes karyawan dipengaruhi oleh dua faktor:
- **Jenis pelatihan** (A atau B)
- **Tingkat pendidikan** (SMA, S1, S2)

Selain itu, ingin diketahui juga apakah ada **interaksi antara pelatihan dan pendidikan** yang memengaruhi hasil tes.

## Kesimpulan
