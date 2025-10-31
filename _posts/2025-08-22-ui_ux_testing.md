---
title: "UI/UX Testing"
author: 
date: 2025-08-22 10:00:00 +0700
categories: [Materi]
tags: [ui-testing, ux-testing, usability, user-experience]
image:
  path: assets/images/post/ui_ux_testing/ui&ux testing.png
  alt: UI/UX Testing Guide
---

> Memahami perbedaan dan pentingnya UI/UX Testing untuk menciptakan produk digital yang tidak hanya menarik, tapi juga mudah digunakan.
{: .prompt-tip }

---

## <i class="fas fa-palette"></i> Apa itu UI/UX Testing?

**UI (User Interface) Testing** dan **UX (User Experience) Testing** adalah dua aspek penting dalam pengembangan produk digital yang saling melengkapi.

### Perbedaan UI vs UX Testing

| Aspek | UI Testing | UX Testing |
|-------|-----------|-----------|
| **Fokus** | Tampilan visual aplikasi | Pengalaman pengguna secara keseluruhan |
| **Yang Ditest** | Warna, font, layout, button, responsiveness | Kemudahan penggunaan, alur kerja, kepuasan user |
| **Tujuan** | Memastikan tampilan konsisten dan menarik | Memastikan aplikasi mudah dan nyaman digunakan |
| **Metrik** | Visual consistency, responsiveness | Task completion, satisfaction score |
| **Tools** | Percy, Applitools, BrowserStack | Hotjar, UserTesting, Google Analytics |

> **Analogi Sederhana:** UI adalah bagaimana rumah terlihat (cat, furniture, dekorasi). UX adalah bagaimana nyamannya tinggal di rumah itu (tata ruang, pencahayaan, aksesibilitas).
{: .prompt-info }

---

## <i class="fas fa-eye"></i> UI Testing

UI Testing memastikan bahwa tampilan aplikasi konsisten, menarik, dan berfungsi dengan baik di berbagai device dan browser.

### 1. Konsistensi Visual

#### <i class="fas fa-palette"></i> Warna & Brand Identity

**Elemen yang harus konsisten:**

- **Primary Button** - Warna, hover state, active state, disabled state
- **Text Color** - Heading, body, secondary text, link
- **Background** - Konsisten di semua halaman
- **Alert Messages** - Success (hijau), Error (merah), Warning (kuning), Info (biru)

**Test Case Example:**
```
1. Capture screenshot button di halaman Login
2. Capture screenshot button di halaman Register  
3. Capture screenshot button di halaman Dashboard
4. Bandingkan hex color code
✓ Expected: Semua menggunakan warna yang sama
```

#### <i class="fas fa-font"></i> Tipografi & Hierarchy

| Level | Font Size | Font Weight | Usage |
|-------|-----------|-------------|-------|
| **H1** | 32-36px | Bold (700) | Page title |
| **H2** | 24-28px | Semi-Bold (600) | Section heading |
| **H3** | 20-22px | Medium (500) | Sub-section |
| **Body** | 16px | Regular (400) | Content |
| **Caption** | 14px | Regular (400) | Helper text |

**Best Practices:**
- Line height minimal 1.5x untuk readability
- Maximum line length: 60-80 karakter
- Font family konsisten di seluruh aplikasi
- Gunakan max 2-3 font weights

#### <i class="fas fa-ruler"></i> Spacing & Layout

**Spacing System (kelipatan 8px):**
- Padding button: `12px 24px`
- Margin antar section: `48px` atau `64px`
- Gap antar card: `24px` atau `32px`
- Margin antar paragraph: `16px`

---

### 2. Responsivitas

#### Breakpoint Standards

| Device | Width | Layout Strategy |
|--------|-------|----------------|
| **Mobile** | 320px - 767px | Single column, hamburger menu |
| **Tablet** | 768px - 1023px | 2 columns, collapsible sidebar |
| **Desktop** | 1024px - 1440px | Multi-column, full sidebar |
| **Wide** | 1441px+ | Max-width container, centered |

**Testing Checklist:**

- <i class="fas fa-check-circle"></i> Tidak ada horizontal scroll
- <i class="fas fa-check-circle"></i> Text tetap readable (min 16px di mobile)
- <i class="fas fa-check-circle"></i> Image responsive (tidak overflow)
- <i class="fas fa-check-circle"></i> Touch target minimal 44x44px (Apple HIG)
- <i class="fas fa-check-circle"></i> Layout tidak pecah saat resize

---

### 3. Cross-Browser Testing

#### Priority Browsers

| Priority | Browser | Market Share | Notes |
|----------|---------|--------------|-------|
| **High** | Chrome | ~65% | Desktop & mobile |
| **High** | Safari | ~20% | iOS & macOS users |
| **High** | Firefox | ~8% | Privacy-focused |
| **Medium** | Edge | ~5% | Windows default |

**Common Issues:**
- CSS Grid/Flexbox compatibility
- JavaScript ES6+ features
- Custom fonts rendering
- Animation performance
- Form autofill styling

---

## <i class="fas fa-users"></i> UX Testing

UX Testing fokus pada bagaimana pengguna berinteraksi dengan produk dan seberapa mudah mereka mencapai tujuan.

### 1. User Flow Analysis

**Prinsip Good User Flow:**

- **Minimal Steps** - Idealnya 3-5 langkah untuk complete task
- **Clear Navigation** - User tahu di mana mereka berada
- **Logical Progression** - Urutan yang masuk akal
- **Easy to Reverse** - Mudah kembali/undo

**Example: E-commerce Purchase Flow**

| Step | Action | Expected Time |
|------|--------|---------------|
| 1 | Browse products | 30-60s |
| 2 | Select product | 20s |
| 3 | Add to cart | 5s |
| 4 | Review cart | 15s |
| 5 | Checkout | 2-3 min |

**Key Metrics:**
- **Success Rate** - Berapa % user berhasil complete task
- **Time on Task** - Waktu yang dibutuhkan
- **Error Rate** - Jumlah kesalahan yang dibuat
- **Clicks to Complete** - Jumlah klik yang dibutuhkan

---

### 2. Usability Principles

#### <i class="fas fa-bullseye"></i> Clarity (Kejelasan)

**Label & Instructions yang Baik:**

| ❌ Bad | ✅ Good |
|-------|--------|
| "Submit" | "Create Account" |
| "Email" | "Enter your email address" |
| "Error occurred" | "Email format invalid. Use: name@example.com" |
| "Click here" | "Download user guide (PDF)" |

#### <i class="fas fa-comment-dots"></i> Feedback & Communication

**User harus selalu tahu apa yang terjadi:**

| State | Feedback Required | Example |
|-------|-------------------|---------|
| **Loading** | Spinner/progress bar | "Loading your data..." |
| **Success** | Confirmation message | "✓ Changes saved successfully" |
| **Error** | Clear error + solution | "Unable to save. Check your internet connection." |
| **Processing** | Progress indicator | "Step 2 of 3 - Payment details" |

**Feedback Timeline:**
- **Instant** (< 0.1s) - Feels immediate (button click)
- **Short** (0.1s - 1s) - Show loading state
- **Long** (> 1s) - Show progress indicator with percentage

#### <i class="fas fa-exclamation-triangle"></i> Error Handling

**3-Part Error Message:**

1. **What happened** - Apa yang terjadi
2. **Why** - Kenapa terjadi (optional)
3. **How to fix** - Cara memperbaiki

**Examples:**

| ❌ Poor | ✅ Good |
|--------|--------|
| "Error 500" | "Unable to process your request. Our team has been notified. Please try again in a few minutes." |
| "Invalid input" | "Password must be at least 8 characters and include one number." |
| "Failed" | "Payment declined. Please check your card details or try another payment method." |

---

### 3. Accessibility (A11y)

#### <i class="fas fa-keyboard"></i> Keyboard Navigation

**Must-Have Features:**
- **Tab** - Navigate between interactive elements
- **Enter/Space** - Activate buttons/links
- **Esc** - Close modals/dropdowns
- **Arrow Keys** - Navigate within components (dropdown, carousel)

**Test Method:**
```
1. Unplug your mouse
2. Navigate entire application with keyboard only
3. Can you access all features?
4. Is the focus indicator visible?
```

#### <i class="fas fa-adjust"></i> Color Contrast

**WCAG 2.1 Standards:**

| Text Type | Minimum Ratio | Example |
|-----------|--------------|---------|
| Normal text | 4.5:1 | #595959 on #FFFFFF |
| Large text (18pt+) | 3:1 | #767676 on #FFFFFF |
| UI Components | 3:1 | Button borders, focus states |

**Tools untuk Testing:**
- WebAIM Contrast Checker
- Chrome DevTools Lighthouse
- Figma Contrast Plugin

#### <i class="fas fa-image"></i> Alternative Text

**Checklist:**
- Images memiliki `alt` text deskriptif
- Icon buttons memiliki `aria-label`
- Form inputs memiliki associated labels
- Videos memiliki captions/subtitles

---

## <i class="fas fa-tools"></i> Metode Testing

### 1. Manual Testing

**Kelebihan:**
- Menemukan unexpected issues
- Human perspective & intuition
- Fleksibel untuk exploratory testing

**Kekurangan:**
- Time-consuming
- Tidak scalable
- Subjektif

**Best For:** New features, exploratory testing, usability evaluation

---

### 2. A/B Testing

**Definisi:** Membandingkan 2 versi untuk menentukan mana yang perform lebih baik.

**Example Test:**

| Variant | Change | Conversion Rate |
|---------|--------|-----------------|
| **A (Control)** | Blue button "Sign Up" | 3.2% |
| **B (Test)** | Green button "Start Free Trial" | 4.8% |

**Result:** Version B menang (+50% conversion) ✓

**Metrics yang Diukur:**
- Click-through rate (CTR)
- Conversion rate
- Bounce rate
- Time on page
- Revenue per visitor

---

### 3. Heatmaps & Session Recording

#### Types of Heatmaps

| Type | Shows | Insight |
|------|-------|---------|
| **Click Heatmap** | Where users click | Are CTAs being clicked? |
| **Scroll Heatmap** | How far users scroll | Content placement effectiveness |
| **Move Heatmap** | Mouse movement | Attention points |
| **Attention Heatmap** | Time spent per area | Engagement zones |

**How to Read:**
- 🔴 **Red (Hot)** = High interaction
- 🟡 **Yellow (Warm)** = Medium interaction  
- 🔵 **Blue (Cool)** = Low interaction
- ⚪ **White (Cold)** = No interaction

---

### 4. User Testing

**5-Step Process:**

1. **Define Objectives** - What do you want to learn?
2. **Recruit Participants** - 5-8 users (representative sample)
3. **Prepare Scenarios** - Realistic tasks
4. **Conduct Sessions** - Observe, don't guide
5. **Analyze & Report** - Find patterns, recommend changes

**Success Metrics:**

| Metric | Good | Needs Improvement |
|--------|------|-------------------|
| Success Rate | > 80% | < 60% |
| Time on Task | Within expected range | 2x expected time |
| Error Count | 0-1 per task | 3+ errors |
| Satisfaction (SUS) | ≥ 68 (average) | < 50 |

---

## <i class="fas fa-list-check"></i> 10 Usability Heuristics

### Jakob Nielsen's Heuristics

| # | Heuristic | Quick Guide |
|---|-----------|-------------|
| **1** | Visibility of System Status | Selalu beri feedback tentang apa yang terjadi |
| **2** | Match Real World | Gunakan bahasa user, bukan jargon teknis |
| **3** | User Control & Freedom | User bisa undo/cancel dengan mudah |
| **4** | Consistency & Standards | Desain dan behavior harus konsisten |
| **5** | Error Prevention | Cegah error, jangan hanya tampilkan error |
| **6** | Recognition > Recall | Tampilkan opsi, jangan suruh mengingat |
| **7** | Flexibility & Efficiency | Sediakan shortcuts untuk power users |
| **8** | Aesthetic & Minimalist | Fokus pada yang penting, hindari clutter |
| **9** | Help Recover Errors | Error message jelas dengan solusi |
| **10** | Help & Documentation | Dokumentasi mudah diakses dan searchable |

---

## <i class="fas fa-wrench"></i> Testing Tools

### UI Testing

- **Percy** - Visual regression testing
- **BrowserStack** - Cross-browser & device testing
- **Responsively** - Responsive design testing
- **Chromatic** - Visual testing for Storybook

### UX Testing

- **Hotjar** - Heatmaps & session recordings
- **UserTesting** - Remote user research
- **Maze** - Rapid testing & prototype validation
- **Fullstory** - Session replay & analytics

### Accessibility

- **WAVE** - Accessibility evaluation tool
- **axe DevTools** - Browser extension untuk a11y testing
- **Lighthouse** - Chrome DevTools audit
- **Screen Reader** - NVDA (Windows), VoiceOver (Mac)

---

## <i class="fas fa-clipboard-check"></i> Testing Checklist

### UI Checklist

**Visual Consistency:**
- [ ] Warna konsisten di semua halaman
- [ ] Typography hierarchy jelas dan readable
- [ ] Spacing menggunakan system (8px grid)
- [ ] Icons dari 1 library yang konsisten

**Responsive Design:**
- [ ] Tested di mobile (375px minimum)
- [ ] Tested di tablet (768px, 1024px)
- [ ] Tested di desktop (1440px, 1920px)
- [ ] Tidak ada horizontal scroll
- [ ] Touch targets ≥ 44x44px

**Cross-Browser:**
- [ ] Chrome - Layout & functionality OK
- [ ] Safari - iOS/macOS compatible
- [ ] Firefox - All features work
- [ ] Edge - Windows compatible

---

### UX Checklist

**User Flow:**
- [ ] Task completion dalam ≤ 5 steps
- [ ] Navigation intuitif dan mudah dipahami
- [ ] CTA (Call-to-Action) jelas dan prominent
- [ ] Progress indicator untuk multi-step process

**Feedback & Communication:**
- [ ] Loading states untuk async operations
- [ ] Success messages setelah actions
- [ ] Error messages jelas dengan solusi
- [ ] Form validation inline (real-time)

**Accessibility:**
- [ ] Keyboard navigation berfungsi 100%
- [ ] Focus indicator visible dan jelas
- [ ] Color contrast ≥ 4.5:1 (normal text)
- [ ] Alt text untuk semua images
- [ ] ARIA labels untuk icon buttons
- [ ] Screen reader compatible

---

## <i class="fas fa-lightbulb"></i> Key Takeaways

**Poin Penting:**

1. **UI & UX saling melengkapi** - Keduanya sama pentingnya untuk produk sukses
2. **Test dengan real users** - Asumsi sering salah, data lebih akurat
3. **Accessibility bukan optional** - Design untuk semua orang
4. **Iterasi adalah kunci** - Test → Analyze → Improve → Repeat
5. **Data-driven decisions** - Gunakan metrics untuk validate changes

> **Formula Sukses:** Beautiful UI + Seamless UX = Exceptional Product
{: .prompt-tip }

---

## <i class="fas fa-book"></i> Referensi & Resources

**Books:**
- *Don't Make Me Think* - Steve Krug
- *The Design of Everyday Things* - Don Norman
- *About Face: The Essentials of Interaction Design* - Alan Cooper

**Websites:**
- Nielsen Norman Group - nngroup.com
- Smashing Magazine - smashingmagazine.com
- A List Apart - alistapart.com

**Standards:**
- WCAG 2.1 Guidelines
- Material Design Guidelines
- Human Interface Guidelines (Apple)

---

<div class="text-center text-muted small mt-5">
  <p class="mb-1"><i class="fas fa-users me-2"></i><strong>Kelompok 2</strong> • Pekan 2</p>
  <p class="mb-0">Materi UI/UX Testing</p>
</div>

### Perbedaan UI dan UX Testing

| Aspek | UI Testing | UX Testing |
|-------|-----------|-----------|
| **Fokus** | Tampilan visual aplikasi | Pengalaman pengguna |
| **Yang Ditest** | Warna, font, layout, button, responsiveness | Kemudahan penggunaan, alur kerja, kepuasan user |
| **Tujuan** | Memastikan tampilan konsisten dan menarik | Memastikan aplikasi mudah dan nyaman digunakan |
| **Contoh** | Apakah warna button konsisten? | Apakah user mudah menemukan fitur? |
| **Tools** | Percy, Applitools, BrowserStack | Hotjar, UserTesting, Google Analytics |

**Kesimpulan Sederhana:**
- **UI Testing** = Aplikasi terlihat bagus ✓
- **UX Testing** = Aplikasi mudah digunakan ✓
- **Keduanya penting** untuk kesuksesan produk

---

## UI Testing

### 1. Konsistensi Visual

**Tujuan:** Memastikan elemen visual konsisten di seluruh aplikasi.

#### Elemen yang Harus Konsisten:

**a) Warna**

| Elemen | Harus Sama |
|--------|-----------|
| Primary Button | Warna, hover state, disabled state |
| Text Color | Heading, body text, secondary text |
| Background | Konsisten di semua halaman |
| Alert/Error | Success (hijau), Error (merah), Warning (kuning) |

**Contoh Test Case:**
```
Test: Konsistensi Warna Button
1. Buka halaman Login → Screenshot button
2. Buka halaman Register → Screenshot button
3. Buka halaman Checkout → Screenshot button
4. Bandingkan warna (hex code)

Expected: Semua button menggunakan warna yang sama
Result: Pass/Fail
```

---

**b) Tipografi**

| Level | Font Size | Font Weight | Line Height |
|-------|-----------|-------------|-------------|
| H1 | 32px | Bold (700) | 1.2 |
| H2 | 24px | Semi-Bold (600) | 1.3 |
| H3 | 20px | Medium (500) | 1.4 |
| Body | 16px | Regular (400) | 1.5 |
| Small | 14px | Regular (400) | 1.5 |

**Test Checklist:**
- [ ] Font family konsisten di semua halaman
- [ ] Font size sesuai hierarchy
- [ ] Line height readable (tidak terlalu rapat)
- [ ] Text alignment konsisten

---

**c) Spacing**

**Aturan Spacing:**
- Gunakan kelipatan 8px: 8, 16, 24, 32, 48, 64
- Padding button: 12px 24px (konsisten)
- Margin antar section: 48px
- Margin antar element: 16px

---

### 2. Responsivitas

**Breakpoint yang Harus Ditest:**

| Device | Screen Width | Layout |
|--------|-------------|---------|
| Mobile | 320px - 767px | Single column, hamburger menu |
| Tablet | 768px - 1023px | 2 columns, sidebar collapse |
| Desktop | 1024px+ | Multi-column, full sidebar |

**Test Checklist:**
- [ ] Tidak ada horizontal scroll
- [ ] Text tetap readable di semua ukuran
- [ ] Image responsive (tidak overflow)
- [ ] Button/link mudah diklik (min 44x44px di mobile)
- [ ] Layout tidak pecah saat resize

**Simple Test:**
1. Buka aplikasi di browser
2. Resize dari max width ke min width
3. Cek apakah ada elemen yang overlap/terpotong

---

### 3. Cross-Browser Testing

**Browser yang Harus Ditest:**

| Priority | Browser | Reason |
|----------|---------|---------|
| High | Chrome (Latest) | 65% market share |
| High | Safari (Latest) | iOS users |
| High | Firefox (Latest) | Privacy-focused users |
| Medium | Edge (Latest) | Windows default |

**Test Checklist:**
- [ ] Tampilan konsisten di semua browser
- [ ] Fungsi berjalan normal di semua browser
- [ ] CSS styling tidak ada yang broken
- [ ] JavaScript error tidak muncul

---

## UX Testing

### 1. User Flow

**Definisi:** Langkah-langkah yang dilalui user untuk menyelesaikan task.

**Prinsip Good User Flow:**
- Minimal steps (max 3-5 langkah)
- Logical dan intuitif
- Clear Call-to-Action (CTA)
- Easy to go back

**Contoh User Flow - E-commerce:**

| Step | Action | Time |
|------|--------|------|
| 1 | Browse product | 30s |
| 2 | Filter by category | 10s |
| 3 | View product detail | 20s |
| 4 | Add to cart | 5s |
| 5 | Checkout | 2min |

**Total:** Max 3-5 menit untuk complete purchase

**Metrics yang Diukur:**
- Success rate (berapa % user berhasil complete task)
- Time on task
- Error rate
- Number of clicks

---

### 2. Usability

**Aspek Usability:**

#### a) Clarity (Kejelasan)

**Good Practice:**

| Bad | Good |
|-----|------|
| "Submit" | "Create Account" |
| "Email" | "Email Address" |
| "Error" | "Email format is invalid. Example: user@example.com" |

**Prinsip:**
- Label jelas dan spesifik
- Instruksi mudah dipahami
- Tidak menggunakan jargon teknis

---

#### b) Feedback

**User harus selalu tahu apa yang terjadi:**

| State | Feedback Required |
|-------|-------------------|
| Loading | Loading spinner/skeleton screen |
| Success | Success message + icon |
| Error | Error message + solution |
| Processing | Progress indicator |

**Contoh:**
```
User klik "Save"
→ Button berubah jadi "Saving..." + spinner
→ Button disabled (prevent double-click)
→ Setelah selesai: "✓ Saved successfully"
→ Message hilang setelah 3 detik
```

---

#### c) Error Handling

**Format Error Message yang Baik:**

1. **Apa yang terjadi** (What happened)
2. **Kenapa terjadi** (Why - optional)
3. **Cara memperbaiki** (How to fix)

**Contoh:**

| Bad | Good |
|-----|------|
| "Error 500" | "Unable to save your changes. Please try again or contact support." |
| "Invalid input" | "Email format is invalid. Please use format: user@example.com" |
| "Error" | "Password must be at least 8 characters and include a number" |

---

### 3. Accessibility

**Tujuan:** Aplikasi dapat digunakan oleh semua orang, termasuk penyandang disabilitas.

#### a) Keyboard Navigation

**Test Checklist:**
- [ ] Semua interactive element bisa diakses dengan Tab
- [ ] Focus indicator terlihat jelas
- [ ] Bisa activate dengan Enter/Space
- [ ] Modal bisa close dengan Esc
- [ ] Tidak ada keyboard trap

**Simple Test:**
1. Unplug mouse
2. Navigasi aplikasi hanya dengan keyboard
3. Apakah semua fungsi bisa diakses?

---

#### b) Color Contrast

**WCAG Standard:**

| Text Size | Minimum Contrast Ratio |
|-----------|----------------------|
| Normal text (< 18pt) | 4.5:1 |
| Large text (≥ 18pt) | 3:1 |

**Contoh:**
- Black (#000000) on White (#FFFFFF) = 21:1 ✓ Pass
- Dark Gray (#595959) on White = 7.5:1 ✓ Pass
- Light Gray (#AAAAAA) on White = 2.3:1 ✗ Fail

**Tool:** WebAIM Contrast Checker

---

#### c) Alternative Text

**Checklist:**
- [ ] Semua image punya alt text yang deskriptif
- [ ] Icon button punya aria-label
- [ ] Form input punya label yang jelas
- [ ] Video punya captions/subtitles

**Contoh:**
```html
<!-- Bad -->
<img src="chart.png" alt="chart">
<button><i class="icon-save"></i></button>

<!-- Good -->
<img src="chart.png" alt="Sales chart showing 25% increase in Q4">
<button aria-label="Save document"><i class="icon-save"></i></button>
```

---

## Metode Testing

### 1. Manual Testing

**Kelebihan:**
- Dapat menemukan unexpected issues
- Fleksibel
- Human perspective

**Kekurangan:**
- Time-consuming
- Subjective
- Tidak repeatable

**Best for:** Exploratory testing, usability testing, new features

---

### 2. A/B Testing

**Definisi:** Membandingkan 2 versi (A vs B) untuk melihat mana yang lebih baik.

**Contoh:**

| Variant | Change | Result |
|---------|--------|--------|
| A (Control) | Button biru "Get Started" | CTR: 3.2% |
| B (Test) | Button hijau "Start Free Trial" | CTR: 4.8% |

**Conclusion:** Version B menang (+50% CTR) → Implement B

**Metrics:**
- Click-through rate (CTR)
- Conversion rate
- Time on page
- Bounce rate

---

### 3. Heatmaps

**Jenis Heatmaps:**

| Type | Shows | Insight |
|------|-------|---------|
| Click Heatmap | Di mana user klik | Apakah CTA di-klik? |
| Scroll Heatmap | Seberapa jauh user scroll | Content placement |
| Move Heatmap | Ke mana mouse bergerak | Attention points |

**Cara Membaca:**
- 🔴 Red (Hot) = Banyak interaksi
- 🟡 Yellow (Warm) = Medium interaksi
- 🟢 Green (Cool) = Sedikit interaksi
- ⚪ White (Cold) = Tidak ada interaksi

**Action dari Heatmap:**
- Area penting tapi tidak diklik → Improve visibility
- Non-clickable area banyak diklik → Make it clickable
- Content tidak di-scroll → Move higher atau improve engagement

---

### 4. User Testing

**Process:**

1. **Define objective** - Apa yang mau di-test?
2. **Recruit users** - 5-8 users (representative)
3. **Prepare tasks** - Realistic scenarios
4. **Conduct test** - Observe, don't help
5. **Analyze** - Identify patterns
6. **Report** - Findings & recommendations

**Metrics:**

| Metric | Good | Bad |
|--------|------|-----|
| Success Rate | > 80% | < 60% |
| Time on Task | Within expected | 2x expected |
| Error Count | 0-1 | 3+ |
| Satisfaction (1-10) | ≥ 8 | ≤ 5 |

---

## 10 Heuristic Evaluation (Jakob Nielsen)

### Quick Reference

| # | Heuristic | Artinya |
|---|-----------|---------|
| 1 | Visibility of System Status | Selalu kasih feedback apa yang terjadi |
| 2 | Match Real World | Pakai bahasa user, bukan jargon teknis |
| 3 | User Control & Freedom | User bisa undo/cancel dengan mudah |
| 4 | Consistency & Standards | Konsisten dalam desain dan konvensi |
| 5 | Error Prevention | Cegah error daripada tampilkan error |
| 6 | Recognition > Recall | Tampilkan opsi, jangan suruh ingat |
| 7 | Flexibility & Efficiency | Sediakan shortcuts untuk expert |
| 8 | Aesthetic & Minimalist | Fokus pada hal penting, hindari clutter |
| 9 | Help Recover from Errors | Error message jelas + solusi |
| 10 | Help & Documentation | Sediakan help yang mudah diakses |

---

## Tools

### UI Testing Tools

| Tool | Purpose | Free? |
|------|---------|-------|
| Percy | Visual regression testing | ✓ Free tier |
| BrowserStack | Cross-browser testing | Trial |
| Responsively | Responsive testing | ✓ Free |

### UX Testing Tools

| Tool | Purpose | Free? |
|------|---------|-------|
| Hotjar | Heatmaps & session recording | ✓ Free tier |
| UserTesting | User research | Paid |
| Google Analytics | Analytics | ✓ Free |

### Accessibility Tools

| Tool | Purpose | Free? |
|------|---------|-------|
| WAVE | Accessibility checker | ✓ Free |
| axe DevTools | Browser extension | ✓ Free |
| Lighthouse | Chrome DevTools audit | ✓ Free |

---

## Testing Checklist

### UI Checklist

**Visual:**
- [ ] Warna konsisten di semua halaman
- [ ] Font readable dan hierarchy jelas
- [ ] Spacing konsisten (gunakan kelipatan 8px)
- [ ] Icons konsisten (dari 1 library)

**Responsive:**
- [ ] Tested di mobile (375px)
- [ ] Tested di tablet (768px)
- [ ] Tested di desktop (1920px)
- [ ] Tidak ada horizontal scroll
- [ ] Touch target min 44x44px (mobile)

**Cross-Browser:**
- [ ] Chrome - OK
- [ ] Firefox - OK
- [ ] Safari - OK
- [ ] Edge - OK

---

### UX Checklist

**Flow:**
- [ ] User flow logical (max 5 steps)
- [ ] Navigation mudah dipahami
- [ ] CTA jelas dan mudah ditemukan
- [ ] Progress indicator tersedia (jika multi-step)

**Feedback:**
- [ ] Loading indicator untuk async operations
- [ ] Success message setelah action
- [ ] Error message jelas dan helpful
- [ ] Form validation inline

**Accessibility:**
- [ ] Keyboard navigation works
- [ ] Focus indicator visible
- [ ] Color contrast ≥ 4.5:1
- [ ] Alt text untuk images
- [ ] ARIA labels untuk icon buttons
- [ ] Screen reader compatible

---

## Kesimpulan

**Poin Penting:**

1. **UI Testing** fokus pada tampilan, **UX Testing** fokus pada pengalaman
2. Keduanya **sama pentingnya** untuk kesuksesan produk
3. **Test dengan real users** - data lebih akurat
4. **Accessibility bukan optional** - design untuk semua
5. **Iterasi terus** - test → analyze → improve → repeat

**Formula Sukses:**
```
Beautiful Design (UI) + Easy to Use (UX) = Great Product
```

---

## Referensi

- Nielsen Norman Group - Usability Heuristics
- WCAG 2.1 Guidelines
- Don't Make Me Think by Steve Krug
- The Design of Everyday Things by Don Norman

---

**Kelompok 2** • Presentasi Pekan 2 • Materi UI/UX Testing