---
title: "Pengantar Unit Testing"
author: 
date: 2025-09-03 10:00:00 +0700
categories: [Materi]
tags: [unit-testing, testing, tdd, automation, quality-assurance]
image:
  path: assets/images/post/unit testing/unittesting.jpeg
  alt: Pengantar Unit Testing
---

> Unit Testing adalah praktik menulis kode untuk menguji kode lain pada level terkecil (unit) - memastikan setiap komponen bekerja dengan benar secara independen.
{: .prompt-tip }

---

## <i class="fas fa-cube"></i> Apa itu Unit Testing?

**Unit Testing** adalah metode pengujian perangkat lunak di mana unit individual dari kode - biasanya fungsi, metode, atau class - diuji secara terisolasi untuk memverifikasi bahwa mereka bekerja sesuai yang diharapkan. Ini adalah level pengujian paling fundamental dan granular dalam piramida testing.

Bayangkan Anda sedang membangun sebuah mobil. Sebelum merakit seluruh mobil dan mengujinya di jalan, Anda akan menguji setiap komponen secara terpisah: mesin, rem, suspensi, sistem kelistrikan, dll. Jika setiap komponen sudah terbukti bekerja dengan baik secara individual, kemungkinan besar mobil yang sudah dirakit akan berfungsi dengan baik. Itulah esensi dari unit testing - memastikan setiap "komponen" kode bekerja dengan benar sebelum diintegrasikan.

### Karakteristik Unit Test yang Baik

Unit test yang efektif memiliki karakteristik **F.I.R.S.T**:

**Fast (Cepat)** - Unit test harus eksekusi dalam milidetik. Test suite dengan ribuan unit test harus selesai dalam hitungan detik, bukan menit atau jam. Kecepatan ini penting karena developer akan menjalankan test berkali-kali setiap hari.

**Independent (Independen)** - Setiap test harus dapat berjalan sendiri tanpa bergantung pada test lain atau urutan eksekusi tertentu. Test A tidak boleh mempengaruhi hasil test B. Ini memastikan bahwa ketika test gagal, mudah untuk identify root cause tanpa harus debug dependensi kompleks.

**Repeatable (Dapat Diulang)** - Test harus memberikan hasil yang sama setiap kali dijalankan dalam kondisi yang sama. Tidak boleh ada non-deterministic behavior atau flaky tests yang kadang pass kadang fail tanpa perubahan kode.

**Self-Validating (Validasi Sendiri)** - Test harus otomatis menghasilkan output Pass atau Fail tanpa perlu interpretasi manual. Developer tidak perlu membaca logs atau memeriksa output untuk mengetahui apakah test berhasil.

**Timely (Tepat Waktu)** - Test sebaiknya ditulis sebelum atau bersamaan dengan production code (TDD approach), bukan setelahnya. Test yang ditulis jauh setelah code cenderung kurang comprehensive dan lebih sulit untuk ditulis.

---

## <i class="fas fa-layer-group"></i> Testing Pyramid

Testing Pyramid adalah konsep yang menunjukkan bagaimana berbagai level testing harus didistribusikan dalam strategi testing yang sehat.

```
           /\
          /  \         E2E Tests
         /____\        (UI Tests)
        /      \
       /        \      Integration Tests
      /__________\     (API Tests)
     /            \
    /              \   Unit Tests
   /________________\  (70-80%)
```

### Distribusi Ideal

| Level | Persentase | Kecepatan | Coverage | Biaya Maintenance |
|---|---|---|---|---|
| **Unit Tests** | 70-80% | Sangat cepat (ms) | Detail, granular | Rendah |
| **Integration Tests** | 15-20% | Sedang (detik) | Interaksi antar komponen | Sedang |
| **E2E Tests** | 5-10% | Lambat (menit) | User journeys lengkap | Tinggi |

**Mengapa Pyramid, Bukan Diamond atau Inverted?**

Pyramid shape bukan arbitrary - ada reasoning kuat di baliknya. Unit tests di base karena mereka cepat, murah, dan mudah di-maintain, sehingga kita bisa have many of them untuk maximize coverage. Integration tests di tengah karena mereka slower dan lebih complex, jadi kita hanya test critical integrations. E2E tests di top karena mereka paling lambat, paling brittle, dan paling mahal untuk maintain, jadi kita hanya test critical user flows.

Anti-pattern "Ice Cream Cone" (banyak E2E, sedikit unit tests) adalah disaster - test suite lambat, brittle, dan nightmare untuk maintain. Jika build Anda butuh 30 menit untuk run tests, developer akan skip running tests, dan quality akan menurun.

---

## <i class="fas fa-bullseye"></i> Mengapa Unit Testing Penting?

Unit testing bukan hanya "nice to have" - ini adalah practice fundamental yang membedakan codebase professional dari amatir.

### Manfaat untuk Developer

**Confidence dalam Refactoring** - Dengan unit test yang comprehensive, Anda bisa refactor kode dengan percaya diri. Jika Anda ubah internal implementation tetapi tests masih pass, Anda tahu behavior tidak berubah. Tanpa tests, setiap refactoring adalah gamble - Anda tidak tahu apakah Anda accidentally break something.

**Documentation yang Living** - Unit tests adalah dokumentasi terbaik tentang bagaimana kode seharusnya bekerja. Tidak seperti komentar atau dokumen yang bisa outdated, tests selalu up-to-date karena jika tidak, mereka akan fail. Ketika developer baru join atau Anda revisit kode lama, tests menunjukkan exact behavior dan use cases.

**Debugging yang Lebih Mudah** - Ketika bug muncul, unit tests membantu isolate masalah dengan cepat. Jika integration test fail, Anda tahu ada masalah somewhere dalam flow. Tetapi jika unit test fail, Anda tahu exactly komponen mana yang bermasalah. Ini dramatically mengurangi debugging time.

**Design yang Lebih Baik** - Kode yang testable adalah kode yang well-designed. Untuk write unit tests, Anda dipaksa untuk write modular, decoupled code dengan clear responsibilities. Jika kode sulit untuk di-test, itu red flag bahwa design ada masalah.

### Manfaat untuk Tim dan Bisnis

**Mengurangi Bugs di Production** - Studies menunjukkan bahwa teams dengan high test coverage memiliki significantly fewer production bugs. Bugs yang tertangkap di development phase cost 10-100x lebih murah untuk fix dibanding bugs yang sampai production.

**Faster Development di Long Run** - Meskipun writing tests membutuhkan waktu upfront, dalam jangka panjang development menjadi lebih cepat. Tanpa tests, setiap perubahan kecil butuh extensive manual testing. Dengan tests, Anda langsung tahu jika something breaks.

**Onboarding Lebih Cepat** - Developer baru bisa understand codebase lebih cepat dengan membaca tests. Mereka juga bisa make changes dengan confidence karena tests akan catch mistakes mereka.

**Technical Debt Terkontrol** - Tests membuat easier untuk pay down technical debt. Tanpa tests, refactoring adalah risky. Dengan tests, Anda bisa continuously improve code quality.

---

## <i class="fas fa-code"></i> Anatomi Unit Test

Mari kita break down struktur unit test yang baik dengan pattern **Arrange-Act-Assert (AAA)**.

### Pattern AAA

```java
@Test
public void testCalculateDiscount_ValidCoupon_ReturnsDiscountedPrice() {
    // ARRANGE - Setup preconditions dan inputs
    ShoppingCart cart = new ShoppingCart();
    cart.addItem(new Item("Laptop", 10000000));
    Coupon coupon = new Coupon("DISC20", 0.20);
    
    // ACT - Execute method being tested
    double finalPrice = cart.calculateTotal(coupon);
    
    // ASSERT - Verify results
    assertEquals(8000000, finalPrice, 0.01);
}
```

**Arrange (Persiapan)** - Setup semua preconditions, create objects, initialize variables, dan prepare test data. Ini adalah "given" dalam Given-When-Then pattern. Di sini Anda membuat state yang diperlukan untuk test scenario.

**Act (Aksi)** - Execute method atau function yang sedang diuji. Ini harus ideally satu line of code - call ke method yang ditest. Ini adalah "when" dalam Given-When-Then. Keep this section simple dan focused.

**Assert (Verifikasi)** - Verify bahwa hasil sesuai ekspektasi. Check return values, object state, atau side effects. Ini adalah "then" dalam Given-When-Then. Use assertion methods yang clear dan descriptive.

### Naming Convention

Test method names harus descriptive dan follow pattern yang konsisten:

```
testMethodName_StateUnderTest_ExpectedBehavior
```

**Contoh Good Names:**
- `testLogin_ValidCredentials_ReturnsSuccessToken`
- `testCalculateTotal_EmptyCart_ReturnsZero`
- `testWithdraw_InsufficientBalance_ThrowsException`

**Contoh Bad Names:**
- `testLogin()` - Terlalu generic
- `test1()` - Meaningless
- `loginShouldWork()` - Vague

Good naming membantu ketika test fail - Anda immediately tahu apa yang break tanpa perlu baca test code.

---

## <i class="fas fa-toolbox"></i> Framework dan Tools Unit Testing

Setiap bahasa pemrograman memiliki framework unit testing yang populer dan mature.

### Framework per Bahasa

| Bahasa | Framework | Fitur Utama |
|---|---|---|
| **Java** | JUnit 5, TestNG | Annotations, parameterized tests, assertions kaya |
| **Python** | pytest, unittest | Fixtures, parametrize, simple syntax |
| **JavaScript/TypeScript** | Jest, Mocha | Mocking built-in, snapshot testing, async support |
| **C#** | NUnit, xUnit, MSTest | Attributes, theory tests, fluent assertions |
| **PHP** | PHPUnit | Data providers, test doubles, code coverage |
| **Ruby** | RSpec, Minitest | BDD style, descriptive syntax |
| **Go** | testing package | Built-in, table-driven tests, benchmarking |

### Tools Tambahan

**Mocking Libraries** membantu create test doubles untuk dependencies. Mockito untuk Java, unittest.mock untuk Python, Sinon untuk JavaScript - tools ini essential untuk isolate units being tested.

**Code Coverage Tools** mengukur percentage kode yang di-cover oleh tests. JaCoCo untuk Java, Coverage.py untuk Python, Istanbul untuk JavaScript. Target ideal adalah 80%+ coverage, tetapi remember: high coverage tidak guarantee quality tests.

**Test Runners** execute tests dan report results. Maven Surefire, pytest, Jest - mereka provide parallel execution, filtering, dan reporting yang rich.

**Continuous Integration** integrate testing dengan CI/CD pipeline. Jenkins, GitHub Actions, GitLab CI - run tests automatically pada setiap commit atau pull request.

---

## <i class="fas fa-check-circle"></i> Best Practices Unit Testing

Mengikuti best practices membuat tests lebih valuable dan maintainable.

### Do's ✅

**Test Behavior, Bukan Implementation** - Focus pada what method does, bukan how it does it. Jika Anda refactor internal implementation, tests seharusnya tidak perlu berubah selama behavior sama.

**One Assert per Test (Ideal)** - Setiap test sebaiknya verify satu behavior atau outcome. Jika test punya multiple asserts untuk different things, pecah menjadi separate tests. Ini makes failures easier to diagnose.

**Keep Tests Simple** - Test code harus lebih simple dari production code. Jika test complex, hard to understand, atau butuh tests untuk test, ada yang salah. Avoid logic dalam tests - no loops, no conditionals.

**Test Edge Cases** - Jangan hanya test happy path. Test boundary conditions, null inputs, empty collections, maximum values, etc. Bugs sering hide di edge cases.

**Meaningful Test Data** - Use test data yang representative dan meaningful. Jika testing user registration, use realistic names dan emails, bukan "test1" dan "a@b.c". This makes tests more readable.

**Isolate Dependencies** - Use mocking untuk isolate unit dari dependencies seperti database, external APIs, file system. Unit test harus test logic, bukan infrastructure.

### Don'ts ❌

**Jangan Test Framework atau Library Code** - Jangan test bahwa ArrayList works atau database saves data. Test YOUR code's logic, assume framework works.

**Jangan Copy-Paste Tests** - DRY (Don't Repeat Yourself) applies to test code juga. Use helper methods, test fixtures, atau parameterized tests untuk reduce duplication.

**Jangan Ignore Failing Tests** - Jika test fail, either fix kode atau fix test. Jangan comment out atau skip tests karena "nanti fix". Broken window theory applies.

**Jangan Test Private Methods Directly** - Private methods adalah implementation details. Test them indirectly through public API. Jika perlu test private method directly, maybe it should be public atau extracted ke separate class.

**Jangan Hardcode Paths atau Environment-Specific Values** - Tests harus run anywhere - local machine, CI server, colleague's laptop. Use relative paths, environment variables, atau configuration.

---

## <i class="fas fa-book-open"></i> Contoh Praktis: Testing Calculator Class

Mari kita lihat contoh lengkap unit testing untuk class sederhana.

### Production Code

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int subtract(int a, int b) {
        return a - b;
    }
    
    public int multiply(int a, int b) {
        return a * b;
    }
    
    public double divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Cannot divide by zero");
        }
        return (double) a / b;
    }
}
```

### Test Code

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    private Calculator calculator;
    
    @BeforeEach
    public void setUp() {
        calculator = new Calculator();
    }
    
    @Test
    public void testAdd_PositiveNumbers_ReturnsSum() {
        // Arrange
        int a = 5;
        int b = 3;
        
        // Act
        int result = calculator.add(a, b);
        
        // Assert
        assertEquals(8, result);
    }
    
    @Test
    public void testAdd_NegativeNumbers_ReturnsSum() {
        int result = calculator.add(-5, -3);
        assertEquals(-8, result);
    }
    
    @Test
    public void testSubtract_PositiveNumbers_ReturnsDifference() {
        int result = calculator.subtract(10, 3);
        assertEquals(7, result);
    }
    
    @Test
    public void testMultiply_ByZero_ReturnsZero() {
        int result = calculator.multiply(5, 0);
        assertEquals(0, result);
    }
    
    @Test
    public void testDivide_ValidNumbers_ReturnsQuotient() {
        double result = calculator.divide(10, 2);
        assertEquals(5.0, result, 0.001);
    }
    
    @Test
    public void testDivide_ByZero_ThrowsException() {
        Exception exception = assertThrows(
            IllegalArgumentException.class,
            () -> calculator.divide(10, 0)
        );
        assertEquals("Cannot divide by zero", exception.getMessage());
    }
}
```

**Analysis dari Tests:**
- ✅ Each test focuses on one scenario
- ✅ Descriptive names clearly state what's being tested
- ✅ Covers happy path dan edge cases
- ✅ Tests exception handling
- ✅ Uses AAA pattern consistently

---

## <i class="fas fa-sync-alt"></i> Test-Driven Development (TDD)

TDD adalah methodology di mana tests ditulis SEBELUM production code. Ini membalik traditional workflow dan memberikan benefits yang powerful.

### Red-Green-Refactor Cycle

**1. Red - Write Failing Test** - Tulis test untuk feature yang belum exist. Test harus fail karena implementation belum ada. Ini verify bahwa test actually testing something.

**2. Green - Make Test Pass** - Write minimal code untuk make test pass. Fokus pada "make it work", bukan "make it perfect". Quick and dirty implementation adalah OK di stage ini.

**3. Refactor - Improve Code** - Dengan safety net dari passing tests, refactor code untuk improve design, remove duplication, improve readability. Tests ensure behavior tidak berubah.

**Repeat** - Cycle ini repeat untuk setiap new feature atau behavior.

### Benefits TDD

**Better Design** - TDD forces Anda think tentang API dan design sebelum implementation. Hasil: more testable, modular code.

**Higher Coverage** - Karena tests ditulis first, coverage naturally high. No forgotten edge cases atau "I'll write tests later" (yang never happens).

**Confidence** - Every line of code justified by failing test. No speculative code atau "might need this someday".

**Regression Prevention** - Comprehensive test suite dari start catch regressions early.

### Contoh TDD Flow

```
1. Write test: testGetUser_ValidId_ReturnsUser()
   → Test FAILS (method doesn't exist)

2. Implement: public User getUser(int id) { return null; }
   → Test FAILS (returns null instead of User)

3. Implement: public User getUser(int id) { 
      return database.findById(id); 
   }
   → Test PASSES

4. Refactor: Extract database logic, improve naming
   → Tests still PASS

5. Next feature: Write next test...
```

---

## <i class="fas fa-chart-line"></i> Code Coverage

Code coverage mengukur percentage kode yang executed oleh tests. Ini useful metric tetapi harus interpreted dengan hati-hati.

### Jenis Coverage

| Jenis | Deskripsi | Contoh |
|---|---|---|
| **Line Coverage** | % lines of code executed | 100 dari 120 lines = 83% |
| **Branch Coverage** | % decision branches taken | if-else, switch cases |
| **Function Coverage** | % functions called | 20 dari 25 functions = 80% |
| **Statement Coverage** | % statements executed | Similar to line coverage |

### Interpretation

**80%+ adalah Good Target** - Tidak perlu 100%. Beberapa code memang sulit atau tidak perlu di-test (getters/setters, toString, simple constructors).

**Coverage Tinggi ≠ Quality Tests** - Anda bisa have 100% coverage dengan tests yang tidak assert anything atau hanya test happy path. Coverage shows apa yang tested, bukan seberapa baik tested.

**Focus on Critical Code** - Prioritize coverage untuk business logic, algorithms, complex conditionals. UI glue code atau simple DTOs bisa have lower coverage.

### Coverage Report Example

```
PackageName          Line Coverage    Branch Coverage
-----------------------------------------------------
com.app.service      94% (150/160)    88% (44/50)
com.app.model        78% (120/154)    N/A
com.app.controller   85% (98/115)     75% (30/40)
com.app.util         100% (45/45)     100% (12/12)
-----------------------------------------------------
TOTAL                89% (413/474)    84% (86/102)
```

---

## <i class="fas fa-users-cog"></i> Mocking dan Test Doubles

Unit test harus isolated, tetapi real code often memiliki dependencies. Test doubles membantu mengisolasi unit under test.

### Jenis Test Doubles

**Dummy** - Objects yang passed around tetapi never actually used. Hanya untuk fill parameter lists.

```java
// Dummy - tidak benar-benar digunakan
User dummy = new User();
emailService.send(dummy, "message"); // dummy tidak diakses
```

**Stub** - Provides canned answers to calls. Digunakan untuk control input ke system under test.

```java
// Stub - return predefined value
when(userRepository.findById(1)).thenReturn(testUser);
```

**Spy** - Records information tentang how they were called. Useful untuk verify interactions.

```java
// Spy - track calls
verify(emailService).send(any(User.class), eq("Welcome"));
```

**Mock** - Pre-programmed dengan expectations. Verify bahwa expected calls made.

```java
// Mock - expect specific calls
EmailService mock = mock(EmailService.class);
when(mock.send(any(), any())).thenReturn(true);
verify(mock, times(1)).send(user, "Welcome");
```

**Fake** - Working implementation tetapi simplified. Contoh: in-memory database instead of real database.

```java
// Fake - simplified implementation
public class FakeUserRepository implements UserRepository {
    private Map<Integer, User> users = new HashMap<>();
    
    public User findById(int id) {
        return users.get(id);
    }
}
```

### Kapan Use What?

| Test Double | Kapan Digunakan |
|---|---|
| **Dummy** | Parameter yang required tetapi tidak digunakan |
| **Stub** | Control input untuk force specific paths |
| **Spy** | Verify interaction terjadi tanpa change behavior |
| **Mock** | Verify complex interactions dan call sequences |
| **Fake** | Need working implementation untuk integration-like tests |

---

## <i class="fas fa-exclamation-triangle"></i> Common Pitfalls dan Cara Menghindarinya

### Flaky Tests

**Problem:** Tests yang kadang pass, kadang fail tanpa code changes.

**Causes:**
- Dependency pada external resources (network, database)
- Race conditions dalam async code
- Dependency pada system clock atau random values
- Tests yang depend on execution order

**Solutions:**
- Mock external dependencies
- Use deterministic test data
- Proper async/await handling
- Make tests independent

### Slow Tests

**Problem:** Test suite butuh terlalu lama untuk run.

**Causes:**
- Hitting real database atau external services
- Terlalu banyak integration tests, kurang unit tests
- Unnecessary waits atau sleeps

**Solutions:**
- Use in-memory databases untuk tests
- Mock external services
- Rebalance testing pyramid
- Run tests in parallel

### Brittle Tests

**Problem:** Tests break frequently dengan small code changes.

**Causes:**
- Testing implementation details instead of behavior
- Tight coupling antara tests dan code structure
- Over-mocking

**Solutions:**
- Focus on testing public API dan observable behavior
- Use behavior verification, bukan state verification
- Mock only direct dependencies

---

## <i class="fas fa-trophy"></i> Metrics dan KPIs

Untuk measure effectiveness dari unit testing efforts, track metrics ini:

### Key Metrics

| Metric | Target | Indikator |
|---|---|---|
| **Code Coverage** | > 80% | Seberapa banyak kode ter-cover |
| **Test Pass Rate** | 100% | Berapa % tests pass |
| **Test Execution Time** | < 5 min | Kecepatan feedback loop |
| **Mutation Score** | > 70% | Quality dari tests (mutation testing) |
| **Defect Density** | Trend menurun | Bugs per KLOC di production |

### Mutation Testing

Mutation testing adalah advanced technique untuk test YOUR tests. Tools seperti PIT (Java) atau Mutmut (Python) deliberately introduce bugs (mutations) ke code dan check apakah tests catch them.

```
Original Code:    if (balance > amount)
Mutated Code:     if (balance >= amount)

If tests still PASS → Tests incomplete, mutation "survived"
If tests FAIL → Tests caught mutation, good coverage
```

**Mutation Score = (Killed Mutations / Total Mutations) × 100%**

High mutation score indicates quality tests yang actually test logic, bukan just execute code.

---

## <i class="fas fa-rocket"></i> Integrasi dengan CI/CD

Unit tests paling powerful ketika integrated dengan CI/CD pipeline.

### CI/CD Workflow

```
Developer Commits Code
    ↓
CI Server Detects Commit
    ↓
Build Project
    ↓
Run Unit Tests ← FAST FEEDBACK (2-5 min)
    ↓
Run Integration Tests
    ↓
Run E2E Tests
    ↓
Deploy to Staging
    ↓
Deploy to Production
```

**Benefits:**
- **Immediate Feedback** - Developer tahu dalam minutes jika commit broke something
- **Prevent Bad Code** - Tests must pass sebelum merge
- **Automated Quality Gates** - Enforce coverage minimums
- **Deployment Confidence** - All tests pass = safe to deploy

### GitHub Actions Example

```yaml
name: Unit Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: '11'
    
    - name: Run tests
      run: mvn clean test
    
    - name: Generate coverage report
      run: mvn jacoco:report
    
    - name: Check coverage
      run: mvn jacoco:check
```

---

## <i class="fas fa-graduation-cap"></i> Studi Kasus: E-Commerce Shopping Cart

Mari kita lihat contoh comprehensive untuk fitur shopping cart.

### Requirements

- User dapat add items ke cart
- User dapat remove items dari cart
- User dapat update quantity
- Cart menghitung total dengan benar
- Apply discount codes
- Clear cart

### Production Code

```java
public class ShoppingCart {
    private Map<String, CartItem> items = new HashMap<>();
    
    public void addItem(String productId, String name, 
                       double price, int quantity) {
        if (items.containsKey(productId)) {
            CartItem existing = items.get(productId);
            existing.setQuantity(existing.getQuantity() + quantity);
        } else {
            items.put(productId, 
                     new CartItem(productId, name, price, quantity));
        }
    }
    
    public void removeItem(String productId) {
        items.remove(productId);
    }
    
    public void updateQuantity(String productId, int newQuantity) {
        if (items.containsKey(productId)) {
            if (newQuantity <= 0) {
                removeItem(productId);
            } else {
                items.get(productId).setQuantity(newQuantity);
            }
        }
    }
    
    public double getTotal() {
        return items.values().stream()
            .mapToDouble(item -> item.getPrice() * item.getQuantity())
            .sum();
    }
    
    public double applyDiscount(String code) {
        // Simplified - in real app, validate code against service
        double total = getTotal();
        if ("DISC10".equals(code)) {
            return total * 0.9; // 10% off
        } else if ("DISC20".equals(code)) {
            return total * 0.8; // 20% off
        }
        return total;
    }
    
    public void clear() {
        items.clear();
    }
    
    public int getItemCount() {
        return items.size();
    }
}
```

### Comprehensive Tests

```java
public class ShoppingCartTest {
    private ShoppingCart cart;
    
    @BeforeEach
    public void setUp() {
        cart = new ShoppingCart();
    }
    
    @Test
    public void testAddItem_NewItem_IncreasesCount() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        assertEquals(1, cart.getItemCount());
    }
    
    @Test
    public void testAddItem_ExistingItem_UpdatesQuantity() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        cart.addItem("P001", "Laptop", 10000000, 2);
        assertEquals(1, cart.getItemCount()); // Still 1 unique item
    }
    
    @Test
    public void testRemoveItem_ExistingItem_DecreasesCount() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        cart.removeItem("P001");
        assertEquals(0, cart.getItemCount());
    }
    
    @Test
    public void testUpdateQuantity_ToZero_RemovesItem() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        cart.updateQuantity("P001", 0);
        assertEquals(0, cart.getItemCount());
    }
    
    @Test
    public void testGetTotal_MultipleItems_ReturnsCorrectSum() {
        cart.addItem("P001", "Laptop", 10000000, 2);
        cart.addItem("P002", "Mouse", 200000, 3);
        double expected = (10000000 * 2) + (200000 * 3);
        assertEquals(expected, cart.getTotal(), 0.01);
    }
    
    @Test
    public void testApplyDiscount_ValidCode_ReturnsDiscountedPrice() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        double discounted = cart.applyDiscount("DISC20");
        assertEquals(8000000, discounted, 0.01);
    }
    
    @Test
    public void testApplyDiscount_InvalidCode_ReturnsOriginalPrice() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        double price = cart.applyDiscount("INVALID");
        assertEquals(10000000, price, 0.01);
    }
    
    @Test
    public void testClear_EmptiesCart() {
        cart.addItem("P001", "Laptop", 10000000, 1);
        cart.addItem("P002", "Mouse", 200000, 1);
        cart.clear();
        assertEquals(0, cart.getItemCount());
        assertEquals(0, cart.getTotal(), 0.01);
    }
}
```

**Coverage Analysis:**
- ✅ All public methods tested
- ✅ Edge cases covered (zero quantity, invalid discount)
- ✅ Happy path dan negative scenarios
- ✅ State verification (count, total)

---

## <i class="fas fa-lightbulb"></i> Tips untuk Pemula

Jika Anda baru mulai dengan unit testing, ikuti tips ini:

### Start Small

**Jangan Overwhelmed** - Tidak perlu test seluruh codebase sekaligus. Start dengan:
1. New features - Write tests untuk semua new code
2. Bug fixes - Write test yang reproduce bug, then fix
3. Critical paths - Test core business logic first
4. Gradually expand coverage

### Learn by Example

**Study Good Tests** - Lihat open source projects dengan good test coverage. Spring Framework, Apache Commons, popular GitHub projects - learn dari style mereka.

### Practice TDD on Side Projects

**Experiment** - Use side projects atau katas untuk practice TDD tanpa pressure. Code katas seperti:
- FizzBuzz
- Roman Numerals
- Bowling Game Score
- Bank Account

### Don't Aim for Perfection

**Good Enough > Perfect** - 80% coverage dengan good tests beats 100% coverage dengan poor tests. Focus pada value, bukan arbitrary metrics.

### Ask for Code Reviews

**Learn from Others** - Minta senior developers review test code Anda. Testing adalah skill yang learned through practice dan feedback.

---

## <i class="fas fa-quote-left"></i> Kesimpulan Utama

> "Code tanpa tests adalah legacy code. Tests memberikan confidence untuk evolve, refactor, dan improve code tanpa fear of breaking things."
{: .prompt-info }

**Ringkasan Penting:**

**Unit Testing adalah Investment** - Waktu yang dihabiskan menulis tests akan terbayar berkali lipat dalam reduced debugging time, fewer production bugs, dan easier maintenance. Teams dengan strong testing culture ship faster dan dengan higher quality.

**Testing Pyramid adalah Panduan** - Mayoritas tests harus unit tests karena mereka fast, reliable, dan easy to maintain. Balance dengan integration dan E2E tests untuk comprehensive coverage tanpa sacrificing speed.

**Quality Over Quantity** - Satu test yang well-written dan test critical behavior lebih valuable dari sepuluh tests yang superficial. Focus pada meaningful coverage, bukan just hitting coverage percentage.

**Tests Document Behavior** - Tests adalah executable documentation yang always up-to-date. Good tests communicate intent dan expected behavior lebih clearly daripada comments atau docs.

**TDD Improves Design** - Test-first approach naturally leads ke better design decisions. Kode yang testable adalah kode yang modular, loosely coupled, dan follows SOLID principles.

**Continuous Practice** - Testing adalah skill yang improves dengan practice. Start small, learn from mistakes, iterate, dan gradually build expertise.

1. **Foundation of Quality** - Unit tests adalah base dari quality assurance
2. **Fast Feedback** - Tests provide immediate feedback pada code changes
3. **Living Documentation** - Tests explain how code should behave
4. **Refactoring Safety Net** - Confidence untuk improve code
5. **Professional Practice** - Separates hobbyist dari professional developers

---

## <i class="fas fa-book-open"></i> Referensi & Bacaan Lanjutan

**Buku Essential:**
- *Test Driven Development: By Example* - Kent Beck (Bible of TDD)
- *Working Effectively with Legacy Code* - Michael Feathers
- *Unit Testing Principles, Practices, and Patterns* - Vladimir Khorikov
- *The Art of Unit Testing* - Roy Osherove
- *Growing Object-Oriented Software, Guided by Tests* - Steve Freeman

**Online Resources:**
- **JUnit 5 User Guide** - Official documentation
- **pytest Documentation** - Comprehensive Python testing
- **Jest Documentation** - Modern JavaScript testing
- **Martin Fowler's Blog** - Testing patterns dan best practices
- **Uncle Bob's Clean Code Blog** - TDD dan testing philosophy

**Courses & Tutorials:**
- **Test Automation University** - Free courses dari Applitools
- **Pluralsight** - Unit Testing courses untuk berbagai languages
- **Udemy** - Practical TDD courses
- **YouTube** - Channels seperti Continuous Delivery, Dave Farley

**Tools & Frameworks:**
- **JUnit** - Java testing framework
- **pytest** - Python testing framework
- **Jest** - JavaScript testing framework
- **Mockito** - Java mocking framework
- **JaCoCo** - Java code coverage
- **Mutation Testing** - PIT, Stryker

---

<div class="text-center text-muted small mt-5">
  <p class="mb-1"><i class="fas fa-users me-2"></i><strong>Kelompok 5</strong> • Pekan 5</p>
  <p class="mb-0">Materi Pengantar Unit Testing</p>
</div>