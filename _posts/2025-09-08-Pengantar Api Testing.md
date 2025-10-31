---
title: "Pengantar API Testing"
author: 
date: 2025-09-08 10:00:00 +0700
categories: [Materi]
tags: [api-testing, rest-api, postman, automation, integration-testing]
image:
  path: assets/images/post/api testing/api testing.jpg
  alt: Pengantar API Testing
---

> API Testing adalah proses memverifikasi bahwa Application Programming Interface (API) berfungsi dengan benar, aman, reliable, dan memenuhi ekspektasi - menjadi fondasi kualitas aplikasi modern.
{: .prompt-tip }

---

## <i class="fas fa-plug"></i> Apa itu API?

**API (Application Programming Interface)** adalah jembatan komunikasi yang memungkinkan aplikasi berbeda untuk saling berbicara dan bertukar data. Bayangkan API seperti pelayan di restoran - Anda (aplikasi client) tidak perlu masuk ke dapur (backend/database) untuk memesan makanan. Anda cukup memberitahu pelayan (API) apa yang Anda inginkan, dan pelayan akan mengambilkannya dari dapur untuk Anda.

Di dunia modern yang terhubung, hampir setiap aplikasi menggunakan API. Ketika Anda login dengan akun Google di aplikasi lain, itu menggunakan Google API. Ketika aplikasi cuaca menampilkan prakiraan, itu mengambil data dari Weather API. Ketika Anda memesan Grab, aplikasi berkomunikasi dengan Grab API untuk booking, tracking, dan payment.

### Jenis-Jenis API

**REST API (Representational State Transfer)** - Jenis API paling populer yang menggunakan HTTP methods (GET, POST, PUT, DELETE) dan biasanya mengirim data dalam format JSON atau XML. REST API stateless dan mudah di-scale.

**SOAP API (Simple Object Access Protocol)** - Protocol yang lebih strict dan formal, menggunakan XML untuk messaging. Lebih complex dari REST tetapi menawarkan built-in error handling dan security standards. Common di enterprise dan financial applications.

**GraphQL API** - Modern alternative untuk REST yang developed oleh Facebook. Client bisa request exactly data yang mereka butuhkan, tidak lebih tidak kurang. Mengurangi over-fetching dan under-fetching data.

**WebSocket API** - Enable two-way communication antara client dan server. Perfect untuk real-time applications seperti chat, live notifications, atau multiplayer games.

**gRPC API** - High-performance RPC framework developed oleh Google, menggunakan Protocol Buffers. Sangat fast dan efficient, popular untuk microservices communication.

---

## <i class="fas fa-search"></i> Apa itu API Testing?

**API Testing** adalah proses testing aplikasi pada layer API untuk memverifikasi fungsionalitas, reliability, performance, dan security. Berbeda dengan UI testing yang fokus pada tampilan dan interaksi user, API testing fokus pada business logic layer dan data exchanges.

API testing terjadi di level integration testing dalam testing pyramid. Ini berada di antara unit tests (testing individual components) dan E2E tests (testing complete user journeys). API tests faster dari E2E tests tetapi lebih comprehensive dari unit tests karena test actual integrations antar components.

### Mengapa API Testing Penting?

**Deteksi Bug Lebih Awal** - API adalah core logic dari aplikasi. Bug di API level akan impact semua clients yang menggunakan API tersebut - web, mobile, third-party integrations. Menemukan bug di API level lebih early dan cheaper daripada menemukan di production.

**Tidak Bergantung pada UI** - UI sering berubah dalam development process, tetapi API contracts biasanya lebih stable. Anda bisa mulai test API sebelum UI selesai, mempercepat overall testing timeline. Jika UI bug, API tests masih bisa run.

**Testing yang Lebih Cepat** - API tests significantly faster dari UI tests karena tidak perlu render UI, wait for page loads, atau handle UI element interactions. Test suite yang butuh hours di UI level bisa selesai dalam minutes di API level.

**Coverage yang Lebih Luas** - Dengan API testing, Anda bisa test scenarios yang sulit atau impossible untuk test via UI. Misalnya, test concurrent requests, simulate network errors, atau test dengan volume data yang besar.

**Reusability** - API tests bisa di-reuse across different clients. Satu set API tests bisa validate behavior untuk web app, mobile app, dan third-party integrations simultaneously.

---

## <i class="fas fa-tasks"></i> Apa yang Ditest dalam API Testing?

API testing comprehensive mencakup berbagai aspek untuk ensure quality yang holistic.

### 1. Functional Testing

**Request & Response Validation** - Verify bahwa API menerima request dengan correct parameters dan mengembalikan response yang expected. Check status codes, response body structure, data types, dan values.

**Business Logic** - Validate bahwa API implements business rules dengan benar. Misalnya, jika user order product, inventory harus decrease, order record created, dan notification sent.

**CRUD Operations** - Test Create, Read, Update, Delete operations bekerja correctly untuk semua resources. Verify data persistence, relationships, dan constraints.

**Error Handling** - Test bagaimana API handle invalid inputs, missing parameters, unauthorized access, dan unexpected scenarios. API harus return appropriate error messages dan status codes.

### 2. Integration Testing

**Third-Party Integrations** - Verify bahwa API correctly integrate dengan external services seperti payment gateways, email services, atau cloud storage.

**Database Operations** - Confirm bahwa API correctly read dan write data ke database, handle transactions, dan maintain data integrity.

**Microservices Communication** - Test interactions antar services dalam microservices architecture. Verify data flow, error propagation, dan service dependencies.

### 3. Performance Testing

**Response Time** - Measure berapa lama API memproses request. Typical targets: < 200ms untuk simple queries, < 1s untuk complex operations.

**Load Testing** - Test API behavior under expected load. Misalnya, 1000 concurrent users. Check if response times degrade dan if system remains stable.

**Stress Testing** - Push API beyond normal capacity untuk find breaking point. Identify maximum load yang bisa di-handle before system fails.

**Spike Testing** - Simulate sudden traffic spikes untuk test auto-scaling dan handling unexpected load increases.

### 4. Security Testing

**Authentication & Authorization** - Verify bahwa hanya authenticated users bisa access API dan users hanya bisa access resources yang mereka authorized untuk.

**Data Encryption** - Ensure sensitive data encrypted in transit (HTTPS) dan at rest. Check for exposure of sensitive information dalam responses.

**SQL Injection & XSS** - Test for common vulnerabilities. API harus sanitize inputs dan protect against injection attacks.

**Rate Limiting** - Verify bahwa API enforce rate limits untuk prevent abuse dan DDoS attacks.

**API Keys & Tokens** - Test token expiration, refresh mechanisms, dan secure handling of credentials.

### 5. Reliability Testing

**Availability** - Measure API uptime. Production APIs typically target 99.9%+ availability (< 8.7 hours downtime per year).

**Error Rate** - Track percentage requests yang fail. Healthy APIs typically have < 0.1% error rate.

**Fault Tolerance** - Test bagaimana API handle partial failures, dependency unavailability, dan degraded mode operations.

---

## <i class="fas fa-project-diagram"></i> Komponen API Request & Response

Memahami struktur request dan response adalah fundamental untuk effective API testing.

### HTTP Request Components

```
POST /api/v1/users HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

{
  "username": "johndoe",
  "email": "john@example.com",
  "password": "SecurePass123!"
}
```

**1. HTTP Method** - Action yang akan dilakukan:

| Method | Purpose | Idempotent | Safe |
|---|---|---|---|
| **GET** | Retrieve data | Yes | Yes |
| **POST** | Create new resource | No | No |
| **PUT** | Update entire resource | Yes | No |
| **PATCH** | Partially update resource | No | No |
| **DELETE** | Remove resource | Yes | No |

**2. Endpoint/URL** - Path ke resource yang spesifik. Contoh: `/api/v1/users`, `/api/v1/orders/123`

**3. Headers** - Metadata tentang request:
- `Content-Type`: Format data (application/json, application/xml)
- `Authorization`: Credentials (Bearer token, API key)
- `Accept`: Format response yang diinginkan
- `User-Agent`: Client information

**4. Request Body** - Data yang dikirim dengan request (untuk POST, PUT, PATCH). Usually dalam format JSON atau XML.

**5. Query Parameters** - Additional parameters dalam URL untuk filtering, sorting, pagination:
```
GET /api/v1/products?category=electronics&sort=price&limit=20
```

### HTTP Response Components

```
HTTP/1.1 201 Created
Content-Type: application/json
Location: /api/v1/users/456

{
  "id": 456,
  "username": "johndoe",
  "email": "john@example.com",
  "created_at": "2025-09-08T10:30:00Z",
  "status": "active"
}
```

**1. Status Code** - Indicates result dari request:

| Range | Category | Common Codes |
|---|---|---|
| **2xx** | Success | 200 OK, 201 Created, 204 No Content |
| **3xx** | Redirection | 301 Moved, 304 Not Modified |
| **4xx** | Client Error | 400 Bad Request, 401 Unauthorized, 404 Not Found |
| **5xx** | Server Error | 500 Internal Error, 502 Bad Gateway, 503 Unavailable |

**2. Response Headers** - Metadata tentang response:
- `Content-Type`: Format response data
- `Content-Length`: Size of response body
- `Cache-Control`: Caching directives
- `Location`: URL of newly created resource (untuk 201)

**3. Response Body** - Actual data returned. Biasanya JSON object atau array dengan requested data atau error details.

---

## <i class="fas fa-check-double"></i> Validasi dalam API Testing

Setiap API test harus validate berbagai aspects untuk ensure correctness.

### Response Validation Checklist

**Status Code** - Verify correct HTTP status code returned:
```javascript
// Postman example
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

**Response Time** - Ensure API responds within acceptable timeframe:
```javascript
pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

**Response Body Structure** - Validate JSON schema:
```javascript
pm.test("Response has correct structure", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('username');
    pm.expect(jsonData.username).to.be.a('string');
});
```

**Response Data Values** - Check actual values:
```javascript
pm.test("User data is correct", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.username).to.eql("johndoe");
    pm.expect(jsonData.email).to.include("@example.com");
});
```

**Headers Validation** - Verify response headers:
```javascript
pm.test("Content-Type is application/json", function () {
    pm.response.to.have.header("Content-Type", "application/json");
});
```

**Data Persistence** - Untuk POST/PUT/PATCH, verify data tersimpan dengan GET request:
```javascript
// After creating user, fetch it
pm.test("Created user can be retrieved", function () {
    pm.sendRequest({
        url: pm.environment.get("baseUrl") + "/users/" + userId,
        method: 'GET'
    }, function (err, response) {
        pm.expect(response.json().username).to.eql("johndoe");
    });
});
```

---

## <i class="fas fa-tools"></i> Tools untuk API Testing

Berbagai tools tersedia untuk manual dan automated API testing, masing-masing dengan strengths dan use cases.

### Manual Testing Tools

**Postman** - Tool paling popular untuk API testing dengan UI yang user-friendly. Features:
- Collection management untuk organize requests
- Environment variables untuk different setups (dev, staging, prod)
- Pre-request scripts dan tests dalam JavaScript
- Mock servers untuk simulate APIs
- Automated testing dengan Newman CLI
- Collaboration features untuk teams

**Insomnia** - Alternative untuk Postman dengan focus pada simplicity dan speed. Clean interface, GraphQL support yang excellent, dan plugin ecosystem.

**cURL** - Command-line tool untuk make HTTP requests. Powerful untuk quick tests dan scripting:
```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"username":"johndoe","email":"john@example.com"}'
```

**HTTPie** - Modern command-line HTTP client dengan syntax yang lebih user-friendly dari cURL:
```bash
http POST api.example.com/users username=johndoe email=john@example.com
```

### Automated Testing Tools

**REST Assured (Java)** - Powerful library untuk testing REST APIs dengan DSL yang expressive:
```java
given()
    .contentType(ContentType.JSON)
    .body(user)
.when()
    .post("/api/users")
.then()
    .statusCode(201)
    .body("username", equalTo("johndoe"));
```

**Pytest + Requests (Python)** - Combination yang popular untuk API testing:
```python
def test_create_user():
    response = requests.post(
        f"{BASE_URL}/users",
        json={"username": "johndoe", "email": "john@example.com"}
    )
    assert response.status_code == 201
    assert response.json()["username"] == "johndoe"
```

**SuperTest (JavaScript/Node.js)** - Testing library untuk Node.js applications:
```javascript
request(app)
    .post('/api/users')
    .send({ username: 'johndoe', email: 'john@example.com' })
    .expect(201)
    .expect('Content-Type', /json/)
    .end((err, res) => {
        expect(res.body.username).toBe('johndoe');
    });
```

**Karate DSL** - BDD-style testing framework untuk API testing:
```gherkin
Scenario: Create new user
    Given url 'https://api.example.com/users'
    And request { username: 'johndoe', email: 'john@example.com' }
    When method post
    Then status 201
    And match response.username == 'johndoe'
```

### Performance Testing Tools

| Tool | Best For | Learning Curve |
|---|---|---|
| **JMeter** | Comprehensive load testing, extensive protocols | Medium |
| **K6** | Modern, developer-friendly load testing | Low |
| **Gatling** | High-performance load testing, Scala-based | Medium |
| **Locust** | Python-based, distributed load testing | Low |
| **Artillery** | Quick load tests, YAML configuration | Low |

---

## <i class="fas fa-route"></i> API Testing Workflow

Effective API testing mengikuti systematic workflow untuk ensure comprehensive coverage.

### 1. Understanding API Documentation

Sebelum mulai testing, pahami API thoroughly:
- Read API documentation (Swagger/OpenAPI, README)
- Understand endpoints, methods, parameters
- Review request/response examples
- Identify authentication requirements
- Check rate limits dan constraints

### 2. Test Planning

**Identify Test Scenarios** - List semua scenarios yang perlu ditest:
- Happy path (valid inputs, expected behavior)
- Negative scenarios (invalid inputs, error handling)
- Edge cases (boundary values, empty data)
- Integration scenarios (dependent operations)

**Prioritize Tests** - Focus pada:
- Critical business flows
- High-risk areas
- Frequently used endpoints
- Complex operations

### 3. Test Environment Setup

**Environment Configuration** - Setup variables untuk:
```json
{
  "dev": {
    "baseUrl": "https://dev-api.example.com",
    "apiKey": "dev-key-123"
  },
  "staging": {
    "baseUrl": "https://staging-api.example.com",
    "apiKey": "staging-key-456"
  },
  "production": {
    "baseUrl": "https://api.example.com",
    "apiKey": "prod-key-789"
  }
}
```

**Test Data Preparation** - Create test datasets:
- Valid test data untuk happy path
- Invalid data untuk negative testing
- Boundary values
- Large datasets untuk performance testing

### 4. Test Execution

**Manual Execution** - Run tests manually menggunakan Postman atau similar tools untuk:
- Exploratory testing
- Ad-hoc validation
- Debugging issues

**Automated Execution** - Run test suites automatically:
```bash
# Newman (Postman CLI)
newman run collection.json -e environment.json

# Pytest
pytest tests/api/ -v

# REST Assured (Maven)
mvn test
```

### 5. Test Reporting & Analysis

**Collect Metrics:**
- Pass/Fail rate
- Response times
- Error rates
- Coverage (endpoints tested)

**Analyze Results:**
- Identify failing tests
- Review error messages
- Check logs dan traces
- Correlate with system metrics

**Report Findings:**
- Document bugs dengan details
- Share test results dengan team
- Update test cases based on findings

---

## <i class="fas fa-graduation-cap"></i> Contoh Praktis: E-Commerce API Testing

Mari kita lihat comprehensive example untuk testing e-commerce API.

### API Endpoints

```
GET    /api/v1/products           - List products
GET    /api/v1/products/{id}      - Get product details
POST   /api/v1/products           - Create product (admin)
PUT    /api/v1/products/{id}      - Update product (admin)
DELETE /api/v1/products/{id}      - Delete product (admin)

POST   /api/v1/cart               - Add to cart
GET    /api/v1/cart               - Get cart items
DELETE /api/v1/cart/{itemId}      - Remove from cart

POST   /api/v1/orders             - Create order
GET    /api/v1/orders/{id}        - Get order details
GET    /api/v1/orders             - List user orders
```

### Test Scenario 1: Create Product (Admin)

**Request:**
```json
POST /api/v1/products
Authorization: Bearer admin_token_xyz
Content-Type: application/json

{
  "name": "Wireless Mouse",
  "description": "Ergonomic wireless mouse with 3 buttons",
  "price": 250000,
  "stock": 100,
  "category": "Electronics"
}
```

**Expected Response:**
```json
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1234,
  "name": "Wireless Mouse",
  "description": "Ergonomic wireless mouse with 3 buttons",
  "price": 250000,
  "stock": 100,
  "category": "Electronics",
  "created_at": "2025-09-08T10:00:00Z",
  "updated_at": "2025-09-08T10:00:00Z"
}
```

**Test Cases:**

| Test Case | Input | Expected Result |
|---|---|---|
| **Valid creation** | Complete valid data | 201 Created, product returned |
| **Missing required field** | No "name" field | 400 Bad Request, error message |
| **Invalid price** | price: -100 | 400 Bad Request, validation error |
| **Unauthorized** | No auth token | 401 Unauthorized |
| **Non-admin user** | Regular user token | 403 Forbidden |
| **Duplicate name** | Existing product name | 409 Conflict |

### Test Scenario 2: Get Products (Public)

**Request:**
```
GET /api/v1/products?category=Electronics&sort=price&limit=10
```

**Expected Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [
    {
      "id": 1234,
      "name": "Wireless Mouse",
      "price": 250000,
      "stock": 100
    },
    {
      "id": 1235,
      "name": "Keyboard",
      "price": 500000,
      "stock": 50
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 25
  }
}
```

**Postman Tests:**
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is acceptable", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

pm.test("Products array exists", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('data');
    pm.expect(jsonData.data).to.be.an('array');
});

pm.test("Products are sorted by price", function () {
    var jsonData = pm.response.json();
    var prices = jsonData.data.map(p => p.price);
    var sortedPrices = [...prices].sort((a, b) => a - b);
    pm.expect(prices).to.eql(sortedPrices);
});

pm.test("Pagination info is present", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.pagination).to.have.property('page');
    pm.expect(jsonData.pagination).to.have.property('total');
});
```

### Test Scenario 3: Complete Purchase Flow

**End-to-End Test:**
```javascript
// 1. Get product
GET /api/v1/products/1234
→ Verify product exists dan available

// 2. Add to cart
POST /api/v1/cart
{
  "product_id": 1234,
  "quantity": 2
}
→ Verify cart item created

// 3. Get cart
GET /api/v1/cart
→ Verify product in cart dengan correct quantity

// 4. Create order
POST /api/v1/orders
{
  "shipping_address": "Jl. Example No. 123",
  "payment_method": "credit_card"
}
→ Verify order created
→ Verify cart cleared
→ Verify stock decreased

// 5. Get order details
GET /api/v1/orders/{orderId}
→ Verify order details correct
```

**Python Test Implementation:**
```python
import requests
import pytest

BASE_URL = "https://api.example.com/v1"
AUTH_TOKEN = "Bearer user_token_abc"

def test_complete_purchase_flow():
    headers = {"Authorization": AUTH_TOKEN}
    
    # 1. Get product
    response = requests.get(f"{BASE_URL}/products/1234")
    assert response.status_code == 200
    product = response.json()
    initial_stock = product["stock"]
    
    # 2. Add to cart
    response = requests.post(
        f"{BASE_URL}/cart",
        json={"product_id": 1234, "quantity": 2},
        headers=headers
    )
    assert response.status_code == 201
    
    # 3. Get cart
    response = requests.get(f"{BASE_URL}/cart", headers=headers)
    assert response.status_code == 200
    cart = response.json()
    assert len(cart["items"]) == 1
    assert cart["items"][0]["product_id"] == 1234
    assert cart["items"][0]["quantity"] == 2
    
    # 4. Create order
    response = requests.post(
        f"{BASE_URL}/orders",
        json={
            "shipping_address": "Jl. Example No. 123",
            "payment_method": "credit_card"
        },
        headers=headers
    )
    assert response.status_code == 201
    order = response.json()
    order_id = order["id"]
    
    # 5. Verify cart cleared
    response = requests.get(f"{BASE_URL}/cart", headers=headers)
    assert response.status_code == 200
    assert len(response.json()["items"]) == 0
    
    # 6. Verify stock decreased
    response = requests.get(f"{BASE_URL}/products/1234")
    assert response.status_code == 200
    new_stock = response.json()["stock"]
    assert new_stock == initial_stock - 2
    
    # 7. Get order details
    response = requests.get(
        f"{BASE_URL}/orders/{order_id}",
        headers=headers
    )
    assert response.status_code == 200
    assert response.json()["status"] == "pending"
```

---

## <i class="fas fa-shield-alt"></i> Security Testing dalam API

Security adalah critical aspect yang tidak boleh diabaikan dalam API testing.

### Authentication Testing

**Test Invalid Credentials:**
```javascript
pm.test("Invalid token returns 401", function () {
    pm.sendRequest({
        url: pm.environment.get("baseUrl") + "/api/protected",
        method: 'GET',
        header: {
            'Authorization': 'Bearer invalid_token_xyz'
        }
    }, function (err, response) {
        pm.expect(response).to.have.status(401);
    });
});
```

**Test Expired Tokens:**
- Use expired JWT token
- Verify API returns 401 Unauthorized
- Verify error message mentions token expiration

**Test Missing Authentication:**
```javascript
pm.test("No auth token returns 401", function () {
    pm.sendRequest({
        url: pm.environment.get("baseUrl") + "/api/protected",
        method: 'GET'
    }, function (err, response) {
        pm.expect(response).to.have.status(401);
    });
});
```

### Authorization Testing

**Test Access Control:**
```javascript
// Regular user trying to access admin endpoint
pm.test("Regular user cannot access admin endpoint", function () {
    pm.sendRequest({
        url: pm.environment.get("baseUrl") + "/api/admin/users",
        method: 'GET',
        header: {
            'Authorization': 'Bearer regular_user_token'
        }
    }, function (err, response) {
        pm.expect(response).to.have.status(403);
    });
});
```

**Test Resource Ownership:**
- User A trying to access User B's orders
- Should return 403 Forbidden atau 404 Not Found
- Verify no data leakage

### Input Validation Testing

**SQL Injection:**
```javascript
// Try SQL injection in query parameter
GET /api/users?username=admin' OR '1'='1

// Expected: 400 Bad Request atau properly escaped query
// Should NOT return all users
```

**XSS (Cross-Site Scripting):**
```javascript
// Try XSS in input field
POST /api/comments
{
  "text": "<script>alert('XSS')</script>"
}

// Expected: Input sanitized, script tags removed atau escaped
```

**Path Traversal:**
```javascript
// Try accessing files outside intended directory
GET /api/files?path=../../etc/passwd

// Expected: 400 Bad Request, path validation error
```

### Rate Limiting Testing

**Test Rate Limit Enforcement:**
```python
def test_rate_limiting():
    headers = {"Authorization": "Bearer token_abc"}
    
    # Make requests up to limit
    for i in range(100):
        response = requests.get(f"{BASE_URL}/api/data", headers=headers)
        
        if i < 60:  # Assume limit is 60/minute
            assert response.status_code == 200
        else:
            assert response.status_code == 429  # Too Many Requests
            assert "rate limit exceeded" in response.json()["error"].lower()
```

---

## <i class="fas fa-rocket"></i> Performance Testing Best Practices

Performance testing memastikan API dapat handle expected load dan scale appropriately.

### Metrics to Monitor

| Metric | Description | Target |
|---|---|---|
| **Response Time** | Time untuk process request | p95 < 500ms |
| **Throughput** | Requests processed per second | > 1000 req/s |
| **Error Rate** | % failed requests | < 0.1% |
| **CPU Usage** | Server CPU utilization | < 70% |
| **Memory Usage** | Server memory utilization | < 80% |
| **Database Connections** | Active DB connections | < pool limit |

### Load Testing Scenario

**K6 Example:**
```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
    stages: [
        { duration: '2m', target: 100 },  // Ramp up to 100 users
        { duration: '5m', target: 100 },  // Stay at 100 users
        { duration: '2m', target: 200 },  // Ramp up to 200 users
        { duration: '5m', target: 200 },  // Stay at 200 users
        { duration: '2m', target: 0 },    // Ramp down to 0
    ],
    thresholds: {
        http_req_duration: ['p(95)<500'],  // 95% requests < 500ms
        http_req_failed: ['rate<0.01'],    // Error rate < 1%
    },
};

export default function () {
    let response = http.get('https://api.example.com/products');
    
    check(response, {
        'status is 200': (r) => r.status === 200,
        'response time < 500ms': (r) => r.timings.duration < 500,
    });
    
    sleep(1);
}
```

### Stress Testing

Push API beyond normal limits:
```javascript
export let options = {
    stages: [
        { duration: '2m', target: 100 },
        { duration: '5m', target: 100 },
        { duration: '2m', target: 200 },
        { duration: '5m', target: 200 },
        { duration: '2m', target: 300 },   // Beyond capacity
        { duration: '5m', target: 300 },
        { duration: '2m', target: 400 },   // Breaking point
        { duration: '5m', target: 400 },
        { duration: '10m', target: 0 },    // Recovery
    ],
};
```

**Monitor untuk:**
- At what load API starts degrading
- Error patterns under stress
- Recovery time after load removed
- Resource exhaustion (memory leaks, connection pools)

---

## <i class="fas fa-sync"></i> API Testing dalam CI/CD

Integrate API tests ke CI/CD pipeline untuk continuous quality assurance.

### GitHub Actions Example

```yaml
name: API Tests

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  api-tests:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
        pip install pytest requests
    
    - name: Start API server
      run: |
        python app.py &
        sleep 10  # Wait for server to start
    
    - name: Run API tests
      run: pytest tests/api/ -v --junit-xml=test-results.xml
      env:
        API_BASE_URL: http://localhost:5000
        API_KEY: ${{ secrets.TEST_API_KEY }}
    
    - name: Publish test results
      uses: EnricoMi/publish-unit-test-result-action@v1
      if: always()
      with:
        files: test-results.xml
    
    - name: Run Postman collection
      run: |
        npm install -g newman
        newman run collection.json -e environment.json --reporters cli,junit
    
    - name: Performance tests
      run: |
        npm install -g k6
        k6 run performance-test.js
```

### Jenkins Pipeline

```groovy
pipeline {
    agent any
    
    stages {
        stage('Setup') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh 'pytest tests/unit/ -v'
            }
        }
        
        stage('API Tests') {
            steps {
                sh 'pytest tests/api/ -v'
            }
        }
        
        stage('Integration Tests') {
            steps {
                sh 'pytest tests/integration/ -v'
            }
        }
        
        stage('Performance Tests') {
            steps {
                sh 'k6 run --out influxdb=http://localhost:8086 performance-test.js'
            }
        }
    }
    
    post {
        always {
            junit 'test-results/**/*.xml'
            publishHTML([
                reportDir: 'coverage',
                reportFiles: 'index.html',
                reportName: 'Coverage Report'
            ])
        }
        failure {
            mail to: 'team@example.com',
                 subject: "API Tests Failed: ${env.JOB_NAME}",
                 body: "Check ${env.BUILD_URL} for details"
        }
    }
}
```

---

## <i class="fas fa-lightbulb"></i> Best Practices API Testing

### Do's ✅

**Organize Tests Logically** - Group tests by:
- Resource/endpoint (`/users`, `/products`, `/orders`)
- Functionality (CRUD, search, authentication)
- Test type (functional, performance, security)

**Use Environment Variables** - Never hardcode:
- Base URLs
- API keys atau credentials
- Test data IDs
- Configuration values

**Test Data Independence** - Each test should:
- Create own test data
- Clean up after execution
- Not depend on other tests
- Use unique identifiers

**Validate Thoroughly** - Check:
- Status codes
- Response structure (schema validation)
- Data values
- Headers
- Response times

**Document Tests** - Include:
- Purpose of test
- Prerequisites
- Expected behavior
- Known issues atau limitations

**Version Control** - Track:
- Test collections
- Test scripts
- Environment configurations
- Test data templates

### Don'ts ❌

**Jangan Test di Production** - Use dedicated test environments:
- Development
- Testing/QA
- Staging (production-like)

**Jangan Ignore Flaky Tests** - If test sometimes fails:
- Investigate root cause
- Fix timing issues
- Improve test stability
- Don't just re-run until pass

**Jangan Hard-Delete Test Data** - Preserve untuk:
- Debugging
- Audit trails
- Use soft deletes atau separate test database

**Jangan Skip Security Tests** - Security adalah critical:
- Test authentication
- Test authorization
- Validate input sanitization
- Check for common vulnerabilities

---

## <i class="fas fa-quote-left"></i> Kesimpulan Utama

> "API adalah contract antara systems. API testing memastikan contract tersebut honored, reliable, dan secure - foundation untuk aplikasi modern yang robust."
{: .prompt-info }

**Ringkasan Penting:**

**API Testing adalah Critical** - Di era microservices dan distributed systems, APIs adalah backbone dari aplikasi. Quality API testing directly impact reliability, security, dan user experience dari entire application ecosystem.

**Shift Left dengan API Testing** - Test di API level lebih early dalam development cycle daripada UI testing. Ini catch bugs sooner, reduce cost, dan accelerate development. API tests juga run faster dan more reliably dari E2E tests.

**Automation adalah Key** - Manual API testing good untuk exploration, tetapi automation essential untuk:
- Regression testing
- CI/CD integration
- Performance testing
- Continuous quality monitoring

**Security Cannot Be Afterthought** - Security testing harus integral part dari API testing strategy. Test authentication, authorization, input validation, dan common vulnerabilities dari start.

**Balance Different Test Types** - Comprehensive API testing includes:
- Functional tests (does it work?)
- Performance tests (is it fast?)
- Security tests (is it safe?)
- Integration tests (does it play well with others?)

**Tools Empower Testing** - Leverage modern tools seperti Postman, REST Assured, K6 untuk make testing efficient dan effective. Pilih tools yang fit team's tech stack dan workflow.

1. **APIs adalah Contract** - Test untuk ensure contract honored
2. **Test Early, Test Often** - API testing di development phase
3. **Automate Everything** - CI/CD integration untuk continuous quality
4. **Security First** - Security testing bukan optional
5. **Monitor Performance** - Response times dan scalability matter
6. **Comprehensive Coverage** - Functional, performance, security testing

---

## <i class="fas fa-book-open"></i> Referensi & Bacaan Lanjutan

**Buku Rekomendasi:**
- *REST API Design Rulebook* - Mark Massé
- *Continuous API Management* - Mehdi Medjaoui
- *Testing Web APIs* - Mark Winteringham
- *API Testing and Development with Postman* - Dave Westerveld

**Online Resources:**
- **Postman Learning Center** - Comprehensive guides dan tutorials
- **REST API Tutorial** - Best practices dan patterns
- **API Testing Best Practices** - Industry standards
- **Swagger/OpenAPI Specification** - API documentation standards

**Tools Documentation:**
- **Postman Docs** - https://learning.postman.com/
- **REST Assured** - https://rest-assured.io/
- **K6 Documentation** - https://k6.io/docs/
- **Pytest** - https://docs.pytest.org/
- **Karate DSL** - https://github.com/karatelabs/karate

**Learning Platforms:**
- **Test Automation University** - Free API testing courses
- **Postman Student Program** - Learning resources
- **Udemy** - API testing courses
- **YouTube** - Channels: Automation Step by Step, The Testing Academy

**Communities:**
- **Postman Community** - Forums dan discussions
- **Ministry of Testing** - API testing resources
- **Stack Overflow** - Q&A untuk troubleshooting
- **Reddit r/QualityAssurance** - Community discussions

---

<div class="text-center text-muted small mt-5">
  <p class="mb-1"><i class="fas fa-users me-2"></i><strong>Kelompok 6</strong> • Pekan 6</p>
  <p class="mb-0">Materi Pengantar API Testing</p>
</div>