---
title: "Test Scenario, Test Case & Bug Report"
author: 
date: 2025-09-01 10:00:00 +0700
categories: [Materi]
tags: [test-scenario, test-case, bug-report, testing, qa]
image:
  path: assets/images/post/Test Scenario, Test Case & Bug Report/Test Scenario, Test Case & Bug Report.jpg
  alt: Test Scenario & Test Case Guide
---

> Test Scenario dan Test Case adalah fondasi dari aktivitas pengujian yang sistematis, sementara Bug Report adalah cara kita mengkomunikasikan masalah yang ditemukan untuk diperbaiki.
{: .prompt-tip }

---

## <i class="fas fa-route"></i> Apa itu Test Scenario?

**Test Scenario** adalah deskripsi high-level tentang apa yang akan diuji. Ini adalah pandangan tingkat tinggi yang menjelaskan fungsionalitas end-to-end atau alur pengguna yang perlu divalidasi. Test scenario menjawab pertanyaan "APA yang akan diuji?" tanpa masuk ke detail spesifik tentang bagaimana pengujian akan dilakukan.

Bayangkan Anda sedang merencanakan perjalanan. Test Scenario seperti mengatakan "Saya akan pergi dari Jakarta ke Bali" - itu menjelaskan tujuan akhir dan rute umum, tetapi tidak menjelaskan setiap langkah detail seperti pada jam berapa Anda akan berangkat, maskapai apa yang akan digunakan, atau bagaimana Anda akan ke bandara.

### Karakteristik Test Scenario

**Sederhana dan Ringkas** - Test scenario ditulis dalam bahasa yang mudah dipahami oleh semua stakeholder, termasuk yang non-teknis. Tidak perlu menggunakan jargon teknis yang rumit.

**Berorientasi pada Pengguna** - Fokus pada apa yang akan dilakukan pengguna akhir, bukan pada detail implementasi teknis. Ini membantu memastikan pengujian selaras dengan pengalaman pengguna yang sebenarnya.

**Dapat Diturunkan ke Test Cases** - Setiap test scenario dapat dipecah menjadi beberapa test cases yang lebih detail. Satu scenario bisa menghasilkan banyak test cases tergantung pada kompleksitas fitur.

### Contoh Test Scenario

| ID | Test Scenario | Deskripsi |
|---|---|---|
| **TS_001** | Login Pengguna | Memverifikasi bahwa pengguna dapat login ke aplikasi dengan kredensial yang valid |
| **TS_002** | Pencarian Produk | Memverifikasi fungsionalitas pencarian produk dengan berbagai kriteria |
| **TS_003** | Checkout Keranjang | Memverifikasi proses checkout dari keranjang hingga konfirmasi pembayaran |
| **TS_004** | Reset Password | Memverifikasi bahwa pengguna dapat mereset password mereka |

---

## <i class="fas fa-clipboard-list"></i> Apa itu Test Case?

**Test Case** adalah dokumen yang menjelaskan langkah-langkah spesifik, data input, dan hasil yang diharapkan untuk memvalidasi aspek tertentu dari aplikasi. Jika test scenario menjawab "APA", maka test case menjawab "BAGAIMANA" - bagaimana tepatnya kita akan menguji fungsionalitas tersebut.

Melanjutkan analogi perjalanan sebelumnya, Test Case seperti itinerary detail: "Berangkat pukul 08:00 dengan Garuda Indonesia penerbangan GA-123, check-in online 24 jam sebelumnya, sampai di bandara 2 jam sebelum keberangkatan, bagasi maksimal 20kg." Setiap langkah didefinisikan dengan jelas dan terukur.

### Komponen Test Case

Setiap test case yang baik harus memiliki komponen-komponen berikut untuk memastikan dapat dieksekusi dengan konsisten oleh siapa pun:

**Test Case ID** - Identifier unik untuk pelacakan dan referensi. Format yang umum adalah TC_ModuleName_001, TC_Login_001, dll.

**Test Case Title/Description** - Judul yang jelas menjelaskan apa yang sedang diuji. Harus deskriptif dan mudah dipahami.

**Preconditions** - Kondisi yang harus terpenuhi sebelum test case dapat dieksekusi. Misalnya: "Pengguna sudah terdaftar di sistem" atau "Database dalam keadaan bersih".

**Test Steps** - Langkah-langkah detail yang harus diikuti untuk menjalankan pengujian. Setiap langkah harus spesifik dan actionable.

**Test Data** - Data yang akan digunakan selama pengujian. Ini bisa berupa username, password, nilai input, dll.

**Expected Result** - Hasil yang diharapkan untuk setiap langkah atau untuk test case secara keseluruhan. Ini adalah kriteria pass/fail.

**Actual Result** - Hasil aktual yang diamati saat eksekusi. Diisi saat menjalankan test case.

**Status** - Status eksekusi: Pass, Fail, Blocked, Skip, atau In Progress.

**Priority** - Tingkat kepentingan: Critical (P0), High (P1), Medium (P2), Low (P3).

**Test Type** - Jenis pengujian: Functional, Regression, Smoke, Integration, dll.

### Contoh Test Case Detail

| Field | Value |
|---|---|
| **Test Case ID** | TC_Login_001 |
| **Title** | Verifikasi login dengan kredensial valid |
| **Precondition** | Aplikasi terbuka, pengguna memiliki akun valid |
| **Priority** | High (P1) |
| **Test Type** | Functional |

**Test Steps:**

| Step | Action | Test Data | Expected Result |
|---|---|---|---|
| 1 | Buka halaman login | URL: /login | Halaman login ditampilkan |
| 2 | Masukkan username | user@example.com | Username muncul di field |
| 3 | Masukkan password | Password123! | Password ter-mask dengan *** |
| 4 | Klik tombol "Login" | - | User diarahkan ke dashboard |
| 5 | Verifikasi dashboard | - | Nama user ditampilkan di header |

**Status:** Pass ✅  
**Actual Result:** Sesuai dengan expected result, user berhasil login dan diarahkan ke dashboard.

---

## <i class="fas fa-balance-scale"></i> Perbedaan Test Scenario vs Test Case

Memahami perbedaan antara test scenario dan test case penting untuk membuat dokumentasi pengujian yang efektif.

| Aspek | Test Scenario | Test Case |
|---|---|---|
| **Definisi** | Deskripsi high-level tentang apa yang diuji | Langkah-langkah detail bagaimana menguji |
| **Level** | Tingkat tinggi (High-level) | Tingkat detail (Low-level) |
| **Fokus** | APA yang diuji | BAGAIMANA menguji |
| **Detail** | Satu liner, ringkas | Multi-step, sangat detail |
| **Derivasi** | Dari requirement | Dari test scenario |
| **Jumlah** | Lebih sedikit | Lebih banyak (1 scenario = n cases) |
| **Audience** | Business stakeholders | Testers, QA Engineers |
| **Contoh** | "Verifikasi login functionality" | "Login dengan user valid, invalid, kosong, dll" |

**Hubungan:**
```
Requirement
    ↓
Test Scenario (1)
    ↓
Test Cases (n)
    ↓
Test Steps (n×m)
```

Satu requirement bisa menghasilkan beberapa test scenarios, dan setiap scenario bisa menghasilkan beberapa test cases yang masing-masing memiliki banyak test steps.

---

## <i class="fas fa-pen-fancy"></i> Cara Menulis Test Case yang Efektif

Menulis test case yang baik adalah seni dan sains. Test case yang berkualitas tinggi dapat dieksekusi oleh siapa saja dengan hasil yang konsisten.

### Prinsip SMART

Test case yang baik mengikuti prinsip SMART:

**Specific (Spesifik)** - Setiap test case harus fokus pada satu fungsionalitas atau aspek tertentu. Jangan mencoba menguji terlalu banyak hal dalam satu test case karena akan menyulitkan debugging ketika test gagal.

**Measurable (Terukur)** - Hasil harus dapat diukur dan diverifikasi secara objektif. Hindari kriteria subjektif seperti "UI terlihat bagus" - gunakan kriteria yang jelas seperti "Tombol login berwarna biru (#0066CC) dengan ukuran 120x40 pixels".

**Achievable (Dapat Dicapai)** - Test case harus realistis dan dapat dieksekusi dengan resources yang tersedia. Jangan membuat test case yang memerlukan akses atau tools yang tidak tersedia untuk tim.

**Relevant (Relevan)** - Harus selaras dengan requirement dan tujuan bisnis. Fokus pada pengujian yang memberikan value, bukan hanya untuk mencapai coverage metric.

**Time-bound (Tepat Waktu)** - Dapat diselesaikan dalam waktu yang wajar. Jika sebuah test case memerlukan waktu berjam-jam, pertimbangkan untuk memecahnya menjadi beberapa test case yang lebih kecil.

### Best Practices

**Gunakan Bahasa yang Jelas** - Hindari ambiguitas. Gunakan kata kerja aktif seperti "Klik", "Masukkan", "Verifikasi" daripada kata-kata pasif atau vague. Setiap orang yang membaca harus memahami apa yang harus dilakukan.

**Satu Test Case = Satu Skenario** - Jangan menggabungkan beberapa skenario dalam satu test case. Jika sebuah step gagal di tengah jalan, akan sulit untuk mengetahui apakah step selanjutnya akan berhasil atau tidak.

**Independen** - Test case harus dapat dijalankan sendiri tanpa bergantung pada eksekusi test case lain. Dependensi antar test cases membuat maintenance sulit dan dapat menyebabkan false failures.

**Reusable** - Tulis test case yang dapat digunakan kembali untuk regression testing. Investasi waktu di awal akan terbayar di iterasi-iterasi berikutnya.

**Include Negative Testing** - Jangan hanya test happy path. Uji juga boundary conditions, invalid inputs, dan error scenarios. Bug sering ditemukan di edge cases.

**Maintainable** - Struktur test case dengan cara yang mudah di-update ketika aplikasi berubah. Gunakan naming convention yang konsisten dan organisasi yang logis.

---

## <i class="fas fa-list-ol"></i> Jenis-Jenis Test Case

Test case dapat dikategorikan berdasarkan tujuan dan cara pengujiannnya.

### Berdasarkan Tipe Pengujian

**Functional Test Cases** - Menguji apakah fitur berfungsi sesuai spesifikasi. Contoh: "Verifikasi bahwa user dapat menambahkan produk ke keranjang".

**Non-Functional Test Cases** - Menguji aspek seperti performance, security, usability. Contoh: "Verifikasi bahwa halaman load dalam < 2 detik".

**UI Test Cases** - Menguji elemen visual dan interaksi user interface. Contoh: "Verifikasi bahwa tombol disabled berwarna abu-abu".

**Integration Test Cases** - Menguji interaksi antar modul atau sistem. Contoh: "Verifikasi bahwa order tersinkronisasi dengan inventory system".

**Regression Test Cases** - Menguji bahwa perubahan baru tidak merusak fungsi existing. Contoh: "Setelah update payment gateway, verifikasi bahwa checkout masih bekerja".

### Berdasarkan Pendekatan

| Pendekatan | Deskripsi | Kapan Digunakan |
|---|---|---|
| **Positive Testing** | Menguji dengan input valid dan expected behavior | Memvalidasi happy path bekerja |
| **Negative Testing** | Menguji dengan input invalid dan unexpected behavior | Memverifikasi error handling |
| **Boundary Testing** | Menguji di batas nilai minimum, maksimum, dan edge | Menemukan off-by-one errors |
| **Exploratory Testing** | Menguji tanpa pre-defined test cases, ad-hoc | Menemukan bug yang tidak terduga |

---

## <i class="fas fa-bug"></i> Apa itu Bug Report?

**Bug Report (Laporan Bug)** adalah dokumen yang menjelaskan masalah atau defect yang ditemukan selama pengujian. Bug report yang baik adalah jembatan komunikasi antara QA dan Developer - membantu developer memahami masalah dengan cepat dan memperbaikinya secara efisien.

Bug report yang buruk: "Login tidak bekerja" - ini tidak memberikan informasi cukup untuk developer.

Bug report yang baik: "Login gagal dengan error 'Invalid credentials' ketika menggunakan username dengan karakter spesial (@, #, $) pada environment staging, browser Chrome 120, langkah untuk reproduce: 1) Buka /login, 2) Masukkan username 'user@test.com', 3) Masukkan password valid, 4) Klik Login. Expected: Login berhasil. Actual: Error message muncul."

### Komponen Bug Report

Setiap bug report yang efektif harus mencakup komponen-komponen berikut:

**Bug ID** - Identifier unik, biasanya di-generate otomatis oleh bug tracking tool seperti Jira.

**Title/Summary** - Deskripsi singkat dan jelas tentang masalah. Harus informatif dalam 1 baris.

**Description** - Penjelasan detail tentang bug, termasuk konteks dan dampaknya.

**Steps to Reproduce** - Langkah-langkah detail untuk mereproduksi bug. Ini adalah bagian paling penting - jika developer tidak bisa reproduce, mereka tidak bisa fix.

**Expected Result** - Apa yang seharusnya terjadi (behavior yang benar).

**Actual Result** - Apa yang sebenarnya terjadi (behavior yang salah).

**Severity** - Seberapa parah dampak bug terhadap sistem.

**Priority** - Seberapa urgent bug harus diperbaiki.

**Environment** - Informasi tentang OS, browser, device, app version, dll.

**Attachments** - Screenshot, video, logs yang membantu menjelaskan masalah.

**Assignee** - Developer yang bertanggung jawab memperbaiki.

**Status** - Open, In Progress, Fixed, Verified, Closed, Reopened.

---

## <i class="fas fa-exclamation-triangle"></i> Severity vs Priority

Dua konsep yang sering membingungkan tetapi sangat penting untuk dipahami dalam bug reporting.

### Severity (Keparahan)

Severity mengukur **dampak teknis** dari bug terhadap fungsionalitas sistem. Ini adalah assessment objektif tentang seberapa parah bug memengaruhi aplikasi.

| Severity | Definisi | Contoh | Dampak |
|---|---|---|---|
| **Critical** | Sistem crash/tidak bisa digunakan | Aplikasi crash saat launch | Sistem down |
| **Major** | Fitur utama tidak bekerja | Payment gagal | Kehilangan revenue |
| **Minor** | Fitur bekerja tapi ada masalah | Button salah warna | Pengalaman kurang optimal |
| **Trivial** | Masalah kosmetik kecil | Typo pada label | Tidak ada dampak fungsional |

### Priority (Prioritas)

Priority mengukur **urgensi bisnis** untuk memperbaiki bug. Ini adalah keputusan bisnis tentang kapan bug harus diperbaiki.

| Priority | Definisi | Timeline | Contoh |
|---|---|---|---|
| **P0 (Critical)** | Harus diperbaiki segera | Hari ini | Bug di production yang block user |
| **P1 (High)** | Perbaiki di sprint ini | Minggu ini | Bug pada fitur penting |
| **P2 (Medium)** | Perbaiki di sprint berikutnya | Sprint depan | Bug pada fitur sekunder |
| **P3 (Low)** | Perbaiki jika ada waktu | Kapan saja | Nice to have fixes |

### Kombinasi Severity & Priority

Tidak selalu severity tinggi = priority tinggi. Berikut adalah matriks yang menunjukkan berbagai kombinasi:

| Kombinasi | Contoh | Action |
|---|---|---|
| **High Severity + High Priority** | Pembayaran gagal di production | Fix segera! |
| **High Severity + Low Priority** | Crash pada fitur deprecated yang jarang digunakan | Schedule untuk removal |
| **Low Severity + High Priority** | Typo nama brand di homepage | Fix cepat untuk reputasi |
| **Low Severity + Low Priority** | Button warna sedikit off di halaman jarang dikunjungi | Backlog |

---

## <i class="fas fa-clipboard-check"></i> Template Bug Report

Berikut adalah template bug report yang dapat Anda gunakan sebagai standar tim.

```markdown
**Bug ID:** BUG-1234

**Title:** Login gagal dengan email mengandung karakter spesial

**Reported By:** John Doe (QA Engineer)
**Reported Date:** 2025-09-01
**Assigned To:** Jane Smith (Backend Developer)

**Environment:**
- OS: Windows 11
- Browser: Chrome 120.0.6099.130
- App Version: v2.3.1
- Environment: Staging
- URL: https://staging.example.com/login

**Severity:** Major
**Priority:** High (P1)
**Status:** Open

**Description:**
User tidak dapat login ketika menggunakan email yang mengandung 
karakter spesial seperti + atau . di local part email. Sistem 
mengembalikan error "Invalid email format" meskipun format email 
secara teknis valid menurut RFC 5322.

**Steps to Reproduce:**
1. Buka halaman login: https://staging.example.com/login
2. Masukkan email: user+test@example.com
3. Masukkan password valid: Password123!
4. Klik tombol "Login"

**Expected Result:**
- User berhasil login
- Diarahkan ke dashboard
- Session cookie dibuat

**Actual Result:**
- Error message ditampilkan: "Invalid email format"
- User tetap di halaman login
- Login gagal

**Attachments:**
- Screenshot error: bug-1234-error.png
- Browser console logs: bug-1234-console.log
- Network tab: bug-1234-network.har

**Additional Notes:**
- Bug tidak terjadi dengan email regular: user@example.com ✅
- Bug terjadi konsisten dengan: user+tag@example.com ❌
- Bug terjadi konsisten dengan: user.name@example.com ❌
- Validation regex mungkin perlu di-update untuk support RFC 5322
```

---

## <i class="fas fa-project-diagram"></i> Bug Life Cycle

Bug memiliki siklus hidup dari ditemukan hingga ditutup. Memahami lifecycle membantu tim mengelola bug dengan efisien.

### Status Bug

**1. New/Open** - Bug baru dilaporkan oleh QA atau user. Belum di-review oleh tim development.

**2. Assigned** - Bug telah di-assign ke developer tertentu untuk investigasi dan perbaikan.

**3. In Progress** - Developer sedang aktif mengerjakan fix untuk bug ini.

**4. Fixed** - Developer telah menyelesaikan fix dan deploy ke test environment untuk verifikasi.

**5. Verified** - QA telah memverifikasi bahwa fix bekerja dan bug tidak lagi terjadi.

**6. Reopened** - Bug masih terjadi setelah fix atau muncul lagi (regression). Kembali ke status Assigned atau In Progress.

**7. Closed** - Bug telah diperbaiki, diverifikasi, dan di-deploy ke production. Issue diselesaikan.

**8. Rejected** - Bug ditolak karena working as intended, duplicate, atau not reproducible.

### Flow Diagram

```
New → Assigned → In Progress → Fixed → Verified → Closed
                                 ↓         ↓
                              Rejected  Reopened
                                           ↓
                                      In Progress
```

**Best Practices dalam Bug Lifecycle:**

Jangan langsung close bug setelah developer fix - QA harus verify terlebih dahulu. Jika bug reopen lebih dari 2 kali, lakukan root cause analysis untuk memahami mengapa fix tidak efektif. Untuk bug yang rejected, pastikan ada penjelasan yang jelas mengapa ditolak agar QA tidak report hal yang sama lagi.

---

## <i class="fas fa-tools"></i> Tools untuk Test Management & Bug Tracking

Menggunakan tools yang tepat dapat meningkatkan efisiensi proses testing dan bug tracking secara signifikan.

### Test Management Tools

| Tool | Kelebihan | Cocok Untuk |
|---|---|---|
| **TestRail** | UI intuitif, reporting bagus, integrasi luas | Tim enterprise yang butuh tracking detail |
| **Zephyr** | Terintegrasi dengan Jira, familiar untuk Jira users | Tim yang sudah menggunakan Jira |
| **qTest** | Analytics powerful, scalable | Large organizations dengan multiple teams |
| **TestLink** | Open source, gratis | Small teams dengan budget terbatas |
| **PractiTest** | All-in-one solution, cloud-based | Teams yang butuh solusi comprehensive |

### Bug Tracking Tools

**Jira** adalah standar industri untuk bug tracking dengan customization tinggi dan ecosystem plugin yang kaya. Cocok untuk tim dari kecil hingga enterprise.

**Bugzilla** adalah open-source tool yang mature dengan fitur lengkap. Cocok untuk tim yang prefer self-hosted solution.

**GitHub Issues** terintegrasi langsung dengan code repository, bagus untuk open source projects atau tim yang heavily use GitHub.

**Azure DevOps** adalah solusi Microsoft yang terintegrasi dengan ekosistem .NET dan Azure. Bagus untuk tim yang sudah di Microsoft stack.

**Trello** adalah tool sederhana untuk tracking bug informal atau small teams. Lebih visual dan mudah digunakan tetapi kurang powerful untuk large scale.

---

## <i class="fas fa-check-double"></i> Checklist: Bug Report yang Baik

Gunakan checklist ini sebelum submit bug report untuk memastikan kualitasnya.

**Informasi Dasar:**
- [ ] Title jelas dan deskriptif (max 100 karakter)
- [ ] Description menjelaskan konteks dan dampak
- [ ] Severity dan Priority sudah di-set dengan tepat
- [ ] Environment information lengkap (OS, browser, version)

**Reproduksi:**
- [ ] Steps to reproduce detail dan berurutan
- [ ] Setiap step spesifik dan actionable
- [ ] Bug dapat direproduksi secara konsisten
- [ ] Preconditions dijelaskan dengan jelas

**Hasil:**
- [ ] Expected result dijelaskan dengan jelas
- [ ] Actual result didokumentasikan dengan akurat
- [ ] Perbedaan antara expected dan actual jelas

**Pendukung:**
- [ ] Screenshot atau video dilampirkan jika relevan
- [ ] Logs (console, network, server) disertakan
- [ ] Test data yang digunakan didokumentasikan

**Kualitas:**
- [ ] Tidak ada typo atau grammatical errors
- [ ] Bahasa profesional dan objektif
- [ ] Satu bug per report (tidak menggabungkan multiple issues)
- [ ] Dicek tidak duplicate dengan bug existing

---

## <i class="fas fa-lightbulb"></i> Tips Menulis Bug Report yang Efektif

**Gunakan 5W1H Framework:**
- **What:** Apa masalahnya?
- **Where:** Di mana bug terjadi? (halaman, module, feature)
- **When:** Kapan bug terjadi? (after action, timing)
- **Who:** Siapa yang affected? (all users, specific role)
- **Why:** Mengapa ini bug? (expected vs actual)
- **How:** Bagaimana mereproduksi?

**Komunikasi yang Efektif:**

Gunakan bahasa yang objektif dan faktual. Hindari bahasa emosional atau menyalahkan seperti "Developer tidak melakukan testing dengan baik" - fokus pada fakta masalah, bukan blame. Gunakan istilah teknis yang tepat tetapi jangan terlalu jargon sehingga sulit dipahami. Jika perlu menjelaskan konsep kompleks, gunakan analogi atau diagram.

**Prioritaskan Clarity:**

Clarity lebih penting daripada brevity. Lebih baik bug report yang sedikit panjang tetapi jelas daripada singkat tetapi membingungkan. Developer harus bisa memahami masalah tanpa perlu bolak-balik bertanya. Include semua informasi yang relevan di awal, jangan membuat developer menunggu untuk mendapatkan detail penting.

---

## <i class="fas fa-graduation-cap"></i> Contoh Kasus: E-Commerce Testing

Mari kita lihat contoh lengkap dari test scenario, test case, hingga bug report untuk fitur e-commerce.

### Test Scenario

**TS_CART_001:** Verifikasi fungsionalitas keranjang belanja

### Test Cases dari Scenario

#### TC_CART_001: Tambah Produk ke Keranjang

| Field | Value |
|---|---|
| **Precondition** | User login, produk tersedia |
| **Priority** | High |
| **Type** | Functional |

**Steps:**

| Step | Action | Expected Result |
|---|---|---|
| 1 | Buka halaman produk | Produk ditampilkan dengan tombol "Add to Cart" |
| 2 | Klik "Add to Cart" | Notifikasi sukses muncul |
| 3 | Buka keranjang | Produk muncul di keranjang dengan quantity 1 |

**Status:** Pass ✅

---

#### TC_CART_002: Update Quantity di Keranjang

| Field | Value |
|---|---|
| **Precondition** | Produk sudah ada di keranjang |
| **Priority** | High |
| **Type** | Functional |

**Steps:**

| Step | Action | Expected Result |
|---|---|---|
| 1 | Buka keranjang | Keranjang menampilkan produk |
| 2 | Ubah quantity dari 1 ke 3 | Quantity ter-update |
| 3 | Verifikasi subtotal | Subtotal = harga × 3 |

**Status:** Fail ❌

**Actual Result:** Subtotal tidak ter-update otomatis, harus refresh halaman.

---

### Bug Report yang Dihasilkan

```markdown
**Bug ID:** BUG-2025

**Title:** Subtotal keranjang tidak update otomatis saat quantity diubah

**Severity:** Major
**Priority:** High (P1)
**Status:** Open

**Environment:**
- Browser: Chrome 120
- Device: Desktop
- Version: v3.1.2

**Steps to Reproduce:**
1. Login dan tambahkan produk ke keranjang
2. Buka halaman keranjang
3. Ubah quantity produk dari 1 ke 3
4. Amati subtotal

**Expected:** Subtotal otomatis update ke (harga × 3)
**Actual:** Subtotal tetap menampilkan (harga × 1), harus refresh untuk update

**Impact:** User melihat total yang salah, bisa menyebabkan kebingungan saat checkout

**Attachments:** bug-2025-video.mp4
```

---

## <i class="fas fa-quote-left"></i> Kesimpulan Utama

> "Test case yang baik adalah investasi - waktu yang Anda habiskan untuk menulis test case yang detail akan terbayar berkali-kali lipat dalam efisiensi testing dan quality product."
{: .prompt-info }

**Poin Penting:**

**Test Scenario vs Test Case** - Scenario adalah "APA", Case adalah "BAGAIMANA". Keduanya bekerja bersama untuk menciptakan coverage testing yang komprehensif. Scenario memberikan gambaran besar, sementara case memberikan detail eksekusi.

**Dokumentasi adalah Kunci** - Dokumentasi yang baik membuat testing repeatable, scalable, dan transferable. Ketika team member baru bergabung atau team member existing leave, dokumentasi yang baik memastikan pengetahuan tidak hilang. Test case yang terdokumentasi dengan baik juga dapat di-automate lebih mudah.

**Bug Report = Communication Tool** - Bug report bukan hanya daftar masalah, tetapi alat komunikasi antara QA dan Developer. Semakin jelas dan detail bug report, semakin cepat bug dapat diperbaiki. Developer tidak perlu menghabiskan waktu mencoba reproduce atau memahami masalah.

**Quality Over Quantity** - Lebih baik memiliki 50 test cases berkualitas tinggi yang cover critical scenarios daripada 500 test cases yang redundant atau tidak jelas. Fokus pada value - test case apa yang paling likely menemukan bug atau validate requirement penting?

**Continuous Improvement** - Review dan update test cases secara berkala. Aplikasi berkembang, test cases juga harus berkembang. Hapus test cases yang obsolete, update yang outdated, dan tambahkan untuk fitur baru.

1. **Hierarchy:** Requirement → Scenario → Case → Steps
2. **Documentation:** Detail, clear, and maintainable
3. **Bug Reporting:** Clear reproduction steps adalah kunci
4. **Severity ≠ Priority:** Pahami perbedaannya
5. **Quality First:** Better fewer good cases than many bad ones

---

## <i class="fas fa-book-open"></i> Referensi & Bacaan Lanjutan

**Standar & Best Practices:**
- **IEEE 829** - Standard untuk dokumentasi test
- **ISO/IEC/IEEE 29119** - Software testing standards
- **ISTQB Syllabus** - Foundation level dan advanced testing

**Buku Rekomendasi:**
- *A Practitioner's Guide to Software Test Design* - Lee Copeland
- *The Art of Software Testing* - Glenford Myers
- *Lessons Learned in Software Testing* - Cem Kaner
- *Explore It!* - Elisabeth Hendrickson

**Online Resources:**
- **Ministry of Testing** - Testing community dan resources
- **Software Testing Help** - Tutorials dan guides
- **Guru99** - Free testing training materials
- **Test Automation University** - Free courses untuk automation

---

<div class="text-center text-muted small mt-5">
  <p class="mb-1"><i class="fas fa-users me-2"></i><strong>Kelompok 4</strong> • Pekan 4</p>
  <p class="mb-0">Materi Test Scenario, Test Case & Bug Report</p>
</div>