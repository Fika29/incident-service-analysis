<!-- Header Image -->
<!-- Header Image -->
<p align="center">
  <img src="https://i2.wp.com/theonlinecorner.com/wp-content/uploads/2020/02/image-3.png?fit=1024%2C294&ssl=1" width="800"/>
</p>

# Service Reliability & Incident Performance Analysis
Analysis of service incidents, SLA performance, and operational risk.

---

## Background and Overview

Keandalan layanan IT tidak hanya ditentukan oleh seberapa cepat insiden ditutup, tetapi oleh **pola gangguan yang berulang, konsistensi pemenuhan SLA, dan kesiapan tim dalam menghadapi lonjakan masalah**. Project ini menggunakan data incident management dari platform **ServiceNow™** untuk melihat **stabilitas layanan secara menyeluruh**, bukan dari satu kasus ke kasus lain.

Analisis ini dibuat untuk menjawab pertanyaan utama stakeholder:

> Apakah layanan berjalan stabil, di bagian mana masalah paling sering muncul, dan area mana yang paling berisiko jika tidak segera diperbaiki?

### Northstar Metrics
- **Service Stability Trends** — Melihat tren stabilitas layanan dan mengidentifikasi periode dengan risiko lonjakan insiden.
- **Incident Concentration by Category** — Mengidentifikasi kategori layanan yang paling sering bermasalah dan berkontribusi pada gangguan operasional.
- **Resolution Efficiency by Priority** — Menilai apakah insiden berdampak tinggi benar-benar ditangani lebih cepat.
- **SLA Risk by Priority** — Mengukur tingkat risiko kegagalan SLA berdasarkan tingkat dampak bisnis.
- **Team Workload Distribution** — Melihat ketimpangan distribusi beban kerja antar tim.
- **Team Performance & Bottleneck Risk** — Mengidentifikasi bottleneck operasional dan risiko keterlambatan laten.
- **SLA Exposure by Service Category** — Menentukan kategori layanan dengan eksposur risiko SLA tertinggi.

---

## Executive Summary

<p align="center">
  <img src="charts/overview_trend.png" width="700"/>
</p>

> *(Contoh chart: tren jumlah insiden per bulan + SLA compliance over time)*

Secara umum, layanan terlihat cukup stabil jika dilihat dari angka agregat. Tingkat kepatuhan SLA mencapai **93%**, yang menunjukkan bahwa sebagian besar insiden dapat diselesaikan sesuai target.

Namun, ketika dilihat dari **pergerakan waktu dan dimensi prioritas**, muncul beberapa risiko penting:
- Insiden terkonsentrasi pada periode tertentu, bukan tersebar merata.
- Insiden prioritas tinggi memiliki kecenderungan lebih sering melanggar SLA.
- Beban kerja dan waktu penyelesaian tidak seimbang antar tim.

Kesimpulannya, **layanan tampak stabil di permukaan**, tetapi terdapat **pola risiko laten** yang dapat berdampak signifikan jika terjadi lonjakan atau gangguan besar.

---

## Dataset Structure and ERD

Dataset yang digunakan merupakan **incident management event log** yang diekstraksi dari sistem audit ServiceNow™ dan telah dianonimkan.

**Dataset overview:**
- 36 atribut
- 1 case identifier (incident number)
- 2 dependent variables (resolved_at, closed_at)
- Atribut mencakup state, priority, category, assignment group, SLA, dan waktu

<p align="center">
  <img src="charts/erd_diagram.png" width="700"/>
</p>

> *(ERD sederhana: Incident → Assignment Group → Resolution & SLA)*

Struktur data ini memungkinkan analisis berbasis **alur proses**, bukan hanya status akhir insiden.

---

## Insights Deep-Dive

Insight dibagi berdasarkan **dimensi utama yang relevan bagi stakeholder**.  
Setiap insight menyajikan **angka, konteks bisnis, dan cerita tren historis**.

---

### 1. Time Dimension — Kapan Risiko Layanan Paling Tinggi

<p align="center">
  <img src="charts/incidents_by_month.png" width="700"/>
</p>

**Fakta Data**  
Sekitar **69% event (±98.000)** terjadi hanya dalam **tiga bulan**, dengan puncak tertinggi pada bulan **Maret**.

**Business Metric**  
Jumlah insiden per bulan

**Cerita Tren**  
Lonjakan ini bersifat konsisten dan berulang, menunjukkan bahwa risiko layanan **bersifat musiman**, bukan kejadian acak.

**Makna bagi Stakeholder**  
Tanpa perencanaan kapasitas khusus di periode ini, risiko keterlambatan dan penurunan kualitas layanan akan terus berulang setiap tahun.

---

### 2. Priority Dimension — Insiden Kecil vs Dampak Besar

<p align="center">
  <img src="charts/sla_by_priority.png" width="700"/>
</p>

**Fakta Data**  
Insiden **Critical dan High** memiliki tingkat pelanggaran SLA hingga **12–14%**, jauh di atas rata-rata.

**Business Metric**  
SLA compliance rate per priority

**Cerita Tren**  
Meskipun volumenya kecil, insiden prioritas tinggi secara konsisten lebih sulit diselesaikan tepat waktu.

**Makna bagi Stakeholder**  
Sedikit keterlambatan pada insiden kritis dapat berdampak besar terhadap kepercayaan pengguna dan persepsi kualitas layanan.

---

### 3. Assignment Group Dimension — Ketimpangan Kapasitas Tim

<p align="center">
  <img src="charts/incidents_by_group.png" width="700"/>
</p>

**Fakta Data**  
Satu assignment group menangani **lebih dari 30% total event**, sementara beberapa group lain menunjukkan waktu penyelesaian jauh di atas rata-rata.

**Business Metric**  
Jumlah insiden & rata-rata resolution time per group

**Cerita Tren**  
Distribusi ini relatif konsisten dari waktu ke waktu dan bukan kejadian sesaat.

**Makna bagi Stakeholder**  
Ketergantungan pada tim tertentu meningkatkan risiko operasional jika terjadi lonjakan atau keterbatasan sumber daya.

---

### 4. Resolution Time Dimension — Risiko yang Tidak Terlihat dari Volume

<p align="center">
  <img src="charts/resolution_time_outliers.png" width="700"/>
</p>

**Fakta Data**  
Beberapa group memiliki rata-rata waktu penyelesaian **>80 jam**, meskipun jumlah insidennya rendah.

**Business Metric**  
Average resolution time

**Cerita Tren**  
Outlier ini muncul secara konsisten dan berpotensi menjadi bottleneck laten.

**Makna bagi Stakeholder**  
Risiko layanan tidak selalu datang dari volume besar, tetapi dari **inefisiensi yang dibiarkan berulang**.

---

## Recommendations

Berdasarkan temuan di atas, beberapa langkah strategis yang dapat dipertimbangkan:

1. Gunakan data historis sebagai **early warning** untuk periode berisiko tinggi.
2. Jadikan **insiden prioritas tinggi** sebagai fokus utama evaluasi SLA.
3. Evaluasi dan seimbangkan distribusi beban kerja antar assignment group.
4. Pantau group dengan **resolution time ekstrem** meskipun volumenya kecil.

Pendekatan ini membantu organisasi **mengurangi risiko sebelum berdampak langsung ke pengguna**.

---

## Dataset Reference

Dataset yang digunakan berasal dari penelitian akademik berikut dan digunakan sesuai ketentuan sitasi:

Amaral, C. A. L., Fantinato, M., Reijers, H. A., Peres, S. M. (2019).  
*Enhancing Completion Time Prediction Through Attribute Selection.*  
Proceedings of the 15th International Conference on Advanced Information Technologies for Management (AITM 2018) and 13th International Conference on Information Systems Management (ISM 2018),  
Lecture Notes in Business Information Processing, Vol. 346, pp. 3–23.
