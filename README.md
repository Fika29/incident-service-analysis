<!-- Header Image -->
<p align="center">
  <img src="https://i2.wp.com/theonlinecorner.com/wp-content/uploads/2020/02/image-3.png?fit=1024%2C294&ssl=1" width="800"/>
</p>

# ServiceNow Incident Log Analysis
Analysis of service incidents, SLA performance, and operational risk.

---

## Client Background
Sistem incident management ini berasal dari platform ServiceNow™ yang digunakan oleh sebuah perusahaan IT untuk menangani gangguan layanan operasional. Dataset mencakup 24.918 incident dengan 141.712 event log, merepresentasikan seluruh siklus hidup insiden mulai dari pembukaan hingga penutupan. Analisis ini dilakukan untuk memahami stabilitas layanan, efektivitas penyelesaian insiden, serta tingkat kepatuhan terhadap SLA.

### Northstar Metrics
- **Service Stability Trends** — Melihat tren stabilitas layanan dan mengidentifikasi periode dengan risiko lonjakan insiden.
- **Incident Concentration by Category** — Mengidentifikasi kategori layanan yang sering bermasalah dan berkontribusi pada gangguan operasional.
- **Resolution Efficiency by Priority** — Menilai apakah insiden berdampak tinggi benar-benar ditangani lebih cepat.
- **SLA Risk by Priority** — Mengukur tingkat risiko kegagalan SLA berdasarkan tingkat dampak bisnis.
- **Team Workload Distribution** — Melihat ketimpangan distribusi beban kerja antar tim.
- **Team Performance & Bottleneck Risk** — Mengidentifikasi bottleneck operasional dan risiko keterlambatan laten.
- **SLA Exposure by Service Category** — Menentukan kategori layanan dengan eksposur risiko SLA tertinggi.

Berikut merupakan detail dataset [klik di sini](https://docs.google.com/spreadsheets/d/17DfAtrhOkbuS4jRxa-D6CEiXiAdRiC1x/edit?usp=sharing&ouid=103087631584714947994&rtpof=true&sd=true)

---

## Executive Summary
![Incident Volume & SLA Trend](images/Incident_Volume_&_SLA_Trend.png)

1. **Konsentrasi Volume Insiden**  
   - Insiden tidak merata, terkonsentrasi tajam pada Maret–Mei, puncak tertinggi di Maret.  
   - Periode risiko operasional dapat diprediksi.

2. **Kinerja SLA di Bawah Tekanan**  
   - Tingkat kepatuhan SLA relatif tinggi (±93%).  
   - Penurunan SLA terjadi saat volume insiden meningkat, khususnya pada insiden berprioritas tinggi dan kritikal.

3. **Stabilitas di Luar Periode Puncak**  
   - Volume insiden rendah dan kinerja SLA lebih stabil.  
   - Ada ketergantungan performa pada beban operasional.

4. **Executive Takeaways & Recommendation**  
   - Rata-rata performa sehat, namun rentan pada periode puncak dan insiden kritikal.  
   - Perkuat kesiapan operasional sebelum periode puncak melalui capacity planning dan eskalasi lebih ketat.

---

## Dataset Structure and ERD
Struktur basis data ini terdiri dari 141.712 catatan event yang merepresentasikan 24.918 insiden unik dengan 36 atribut yang menggambarkan siklus hidup insiden, prioritas, penugasan, dan kinerja SLA.  

![ERD](images/ERD.jpeg)

- **INCIDENT**: Satu kasus insiden beserta waktu, status, dampak, prioritas, dan kategori layanan.  
- **ASSIGNMENT_GROUP**: Tim atau unit yang menangani insiden.  
- **USER**: Peran pengguna dalam pelaporan dan penyelesaian insiden.  
- **SLA**: Indikator kepatuhan terhadap Service Level Agreement.  
- **TIME_DIMENSION**: Pelacakan waktu pembukaan dan penyelesaian insiden.  

---

## Insights Deep-Dive

### 1) Service Stability Trends (Dimensi: Number / Bulan)
![Service Stability Trends](images/Service_Stability_Trends.png)  
- Total incident per bulan: 141.712  
- Lonjakan ekstrem hanya di Maret–Mei, bulan lain stabil.  
- Menunjukkan seasonality operasional atau efek perubahan sistem.  
- Tanpa penyesuaian kapasitas tim, periode puncak berisiko menjadi gangguan layanan berskala luas.

### 2) Incident Concentration by Category (Dimensi: Kategori Layanan)
![Incident Concentration by Category](images/Incident_Concentration_by_Category.png)  
- 3 kategori menyumbang >33% dari total incident.  
- Incident berulang pada kategori yang sama menunjukkan masalah struktural.  
- Fokus perbaikan pada kategori inti → penurunan incident signifikan.

### 3) Resolution Efficiency by Priority (Dimensi: Prioritas)
![Resolution Efficiency by Priority](images/Resolution_Efficiency_by_Priority.png)  
- 93% incident selesai sesuai SLA.  
- Kepatuhan SLA tinggi tapi incident kompleks berulang tetap terjadi.  
- Pelanggaran kecil berulang dapat mengikis kepercayaan pengguna.

### 4) SLA Risk by Priority (Dimensi: Prioritas vs SLA)
![SLA Risk by Priority](images/SLA_Risk_by_Priority.png)  
- Incident Critical & High paling sering melanggar SLA.  
- Semakin tinggi dampak → semakin besar kemungkinan terlambat.  
- Incident kritikal → komplain besar, tekanan manajemen, gangguan bisnis.

### 5) Team Workload Distribution (Dimensi: Assignment Group)
![Team Workload Distribution](images/Team_Workload_Distribution.png)  
- 1 tim menangani ±33% dari total incident.  
- Ketergantungan ini menciptakan single point of failure.  
- Ketidakseimbangan → risiko gangguan layanan tinggi.

### 6) Team Performance & Bottleneck Risk (Dimensi: Group Performance)
![Team Performance & Bottleneck Risk](images/Team_Performance_Bottleneck_Risk.png)  
- Rata-rata cepat, tapi kasus ekstrem sangat lama.  
- Bottleneck tersembunyi, meningkatkan biaya operasional dan backlog.

### 7) SLA Exposure by Service Category (Dimensi: Kategori vs SLA)
![SLA Exposure by Service Category](images/SLA_Exposure_by_Service_Category.png)  
- Kategori dengan incident terbanyak paling sering melanggar SLA.  
- Volume tinggi → kegagalan SLA tinggi, pola konsisten.  
- Perbaikan di kategori ini → stabilitas layanan terbesar.

---

## Recommendation

1. **Time-Based Stability (Incident per Month)**  
   - Audit aktivitas sistem dan change pada Maret–Mei, siapkan capacity planning.  
   - Prioritas: High | Owner: IT Ops Lead, Change Management  

2. **Service Concentration Risk (Incident by Category)**  
   - RCA terfokus pada 3 kategori penyumbang terbesar.  
   - Prioritas: Critical | Owner: System Owner, Risk Management  

3. **Resolution Efficiency Control (Resolution Time by Priority)**  
   - Tetapkan early-warning SLA, monitoring rutin.  
   - Prioritas: Moderate | Owner: Service Delivery  

4. **Critical Incident Handling (SLA by Priority)**  
   - Perkuat escalation playbook untuk Critical & High.  
   - Prioritas: High | Owner: IT Ops Manager  

5. **Workload Resilience (Incident by Assignment Group)**  
   - Redistribusi beban dan cross-training.  
   - Prioritas: High | Owner: Ops Head  

6. **Hidden Bottleneck Detection (Resolution Time by Group)**  
   - Tambahkan KPI median & P95, deep dive group outlier.  
   - Prioritas: Moderate–High | Owner: ITSM Lead, Process Improvement  

7. **SLA Exposure Hotspots (SLA by Category)**  
   - Prioritaskan automation & defect prevention pada kategori risiko tinggi.  
   - Prioritas: Critical | Owner: Application Owner  

---

## Citation Dataset
Amaral, C. A. L., Fantinato, M., Reijers, H. A., Peres, S. M. (2019). *Enhancing Completion Time Prediction Through Attribute Selection*. Proceedings of the 15th International Conference on Advanced Information Technologies for Management (AITM 2018).
