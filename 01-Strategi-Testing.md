# Strategi Testing

## Daftar Isi
- [Review Pengenalan Testing](#review-pengenalan-testing)
- [Siklus Hidup Testing](#siklus-hidup-testing)
- [Klasifikasi Strategi Testing](#klasifikasi-strategi-testing)

---

## Review Pengenalan Testing

### Apa itu Testing?
Testing adalah proses evaluasi sistem atau komponen perangkat lunak untuk menemukan perbedaan antara kondisi yang diharapkan dengan kondisi aktual. Testing dilakukan untuk memastikan kualitas produk perangkat lunak.

### Tujuan Testing
- Menemukan bug/kesalahan dalam software
- Memastikan produk memenuhi requirement yang ditentukan
- Meningkatkan kualitas produk
- Memverifikasi bahwa software bekerja sesuai harapan
- Membangun kepercayaan terhadap kualitas produk

### Pentingnya Testing dalam Siklus Pengembangan Perangkat Lunak
- Mengurangi biaya perbaikan bug di tahap production
- Meningkatkan kepuasan pengguna
- Memastikan keamanan aplikasi
- Menjamin performa aplikasi
- Mengurangi risiko kegagalan sistem

---

## Siklus Hidup Testing

### 1. Perencanaan Testing (Test Planning)
- Menentukan scope dan objektif testing
- Membuat test plan yang mencakup strategi, resources, dan timeline
- Mengidentifikasi test case yang akan dibuat

### 2. Desain Kasus Uji (Test Case Design)
- Merancang test case berdasarkan requirement
- Menentukan test data yang diperlukan
- Membuat test scenario
- Menyiapkan expected result

### 3. Eksekusi Testing (Test Execution)
- Menjalankan test case yang telah dirancang
- Mencatat hasil testing
- Melaporkan bug yang ditemukan

### 4. Pelaporan Hasil Testing (Test Reporting)
- Mendokumentasikan hasil testing
- Membuat bug report
- Menyusun test summary report

### 5. Analisis Hasil dan Perbaikan
- Menganalisis hasil testing
- Melakukan retesting setelah bug diperbaiki
- Regression testing
- Evaluasi proses testing

---

## Klasifikasi Strategi Testing

### A. Berdasarkan Tingkat Abstraksi

#### 1. Unit Testing
- Testing pada level komponen/unit terkecil dari code
- Biasanya dilakukan oleh developer
- Fokus pada fungsi atau method individual

#### 2. Integration Testing
- Testing interaksi antar modul/komponen
- Memastikan modul yang berbeda dapat bekerja sama
- Mendeteksi masalah pada interface antar modul

#### 3. System Testing
- Testing pada sistem secara keseluruhan
- Memverifikasi sistem memenuhi requirement
- Testing end-to-end functionality

#### 4. Acceptance Testing
- Testing yang dilakukan untuk validasi dari user
- Memastikan sistem memenuhi kebutuhan bisnis
- Biasanya dilakukan oleh client/end user

### B. Berdasarkan Fungsi

#### 1. Functional Testing
- Testing fungsionalitas aplikasi
- Memastikan fitur bekerja sesuai requirement
- Contoh: test login, test CRUD operations

#### 2. Non-Functional Testing
Meliputi:
- **Performance Testing**: Menguji performa dan kecepatan aplikasi
- **Security Testing**: Menguji keamanan aplikasi
- **Usability Testing**: Menguji kemudahan penggunaan
- **Reliability Testing**: Menguji keandalan sistem

### C. Berdasarkan Struktur

#### 1. Black Box Testing
- Testing tanpa mengetahui struktur internal code
- Fokus pada input dan output
- Tester tidak perlu tahu detail implementasi

#### 2. White Box Testing
- Testing dengan mengetahui struktur internal code
- Memerlukan pengetahuan tentang code
- Fokus pada logic dan struktur internal

### D. Berdasarkan Domain

#### Testing Khusus
- **Security Testing**: Fokus pada aspek keamanan
- **Performance Testing**: Fokus pada kecepatan dan skalabilitas
- **Usability Testing**: Fokus pada user experience
- **Compatibility Testing**: Testing pada berbagai platform/browser

---

## Kesimpulan

Strategi testing yang baik mencakup pemahaman tentang berbagai jenis testing dan kapan menggunakannya. Kombinasi dari berbagai strategi testing akan menghasilkan produk perangkat lunak yang berkualitas tinggi.

---

**Presentasi**: Pekan 2  
**Kelompok**: 1