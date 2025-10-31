---
title: "Pengantar Cypress"
author: 
date: 2025-10-31 10:00:00 +0700
categories: [Materi]
tags: [cypress, e2e-testing, automation, javascript, web-testing]
image:
  path: assets/images/post/cypress/cypress.png
  alt: Pengantar Cypress Testing
---

> Cypress adalah next-generation front-end testing tool yang built untuk modern web - menawarkan fast, easy, dan reliable testing untuk anything yang runs in a browser.
{: .prompt-tip }

---

## <i class="fas fa-bolt"></i> Apa itu Cypress?

**Cypress** adalah JavaScript-based end-to-end testing framework yang revolutionize cara developers dan QA engineers write automated tests. Diluncurkan pada 2017, Cypress designed dari ground up untuk address pain points dari traditional testing tools seperti Selenium - slow execution, flaky tests, complex setup, dan difficult debugging.

Bayangkan Anda memiliki time machine yang bisa pause, rewind, dan fast-forward aplikasi web Anda saat testing. Anda bisa see exactly apa yang terjadi di every step, inspect state pada any point, dan debug dengan ease yang previously impossible. Itulah experience yang Cypress bring - visual, interactive, dan developer-friendly testing yang actually enjoyable to use.

### Apa yang Membuat Cypress Berbeda?

**Runs in the Same Loop** - Berbeda dengan Selenium yang execute commands from outside browser, Cypress runs directly dalam browser alongside your application. Ini memberikan native access ke every object, allowing unprecedented control dan visibility.

**Real-Time Reloads** - Saat Anda save test file, Cypress automatically rerun tests. Combine dengan hot reload dari development server, Anda get instant feedback loop - write test, see results immediately, iterate quickly.

**Time Travel** - Cypress takes snapshots saat tests run. Hover over commands dalam Command Log untuk see exactly what happened at each step. Like having video replay dengan frame-by-frame control.

**Automatic Waiting** - No more arbitrary `sleep()` atau complicated wait logic. Cypress automatically wait untuk elements, animations, XHR requests, dan page transitions. Tests are reliable without extra effort.

**Network Traffic Control** - Stub, spy, atau modify network requests dan responses. Test edge cases, error scenarios, dan loading states tanpa needing actual backend atau external services.

**Debuggability** - Use familiar Chrome DevTools untuk debug tests. Access same debugging experience you use untuk application development - breakpoints, console logs, network inspection.

---

## <i class="fas fa-rocket"></i> Mengapa Memilih Cypress?

Mari compare Cypress dengan traditional testing approaches untuk understand value proposition.

### Cypress vs Selenium

| Aspect | Cypress | Selenium WebDriver |
|---|---|---|
| **Architecture** | Runs inside browser | Remote commands via WebDriver |
| **Language** | JavaScript only | Java, Python, C#, Ruby, JS |
| **Setup** | `npm install cypress` | Driver management, dependencies |
| **Speed** | Very fast | Slower (network overhead) |
| **Debugging** | Chrome DevTools, Time Travel | Console logs, screenshots |
| **Auto-waiting** | Built-in, smart | Manual explicit waits |
| **Network stubbing** | Native support | External tools needed |
| **Real-time reload** | Yes | No |
| **Cross-browser** | Chrome, Edge, Firefox, Electron | All browsers |
| **Learning curve** | Easy (if know JS) | Medium to hard |

### Keunggulan Cypress

**Developer Experience** - Cypress built oleh developers untuk developers. Architecture dan APIs designed untuk be intuitive dan enjoyable. Writing tests feels like writing application code.

**Fast Execution** - Tests run significantly faster karena no network latency antara commands. Typical test suite yang butuh 30 minutes dengan Selenium bisa run dalam 5-10 minutes dengan Cypress.

**Reliable Tests** - Automatic waiting dan retry logic eliminate flaky tests caused oleh timing issues. Once test pass, it consistently pass.

**Visual Testing** - Test Runner shows your application running dalam real browser alongside Command Log. See exactly what Cypress sees, making debugging trivial.

**All-in-One Package** - Cypress includes everything needed: assertion library (Chai), mocking/stubbing (Sinon), test runner (Mocha). No decision fatigue tentang which libraries to use.

**Great Documentation** - Comprehensive, well-written docs dengan lots of examples. Active community dan excellent error messages.

### Trade-offs

**JavaScript Only** - Jika team primarily uses Java atau Python, switching languages bisa be overhead. However, JavaScript's ubiquity dalam web development makes this less of issue.

**Same-Origin Limitations** - Cypress runs dalam browser, subject ke same-origin policy. Testing across multiple domains dalam single test requires workarounds (though possible).

**No Mobile Native Apps** - Cypress is untuk web applications only. Untuk mobile testing, need different tool (Appium, Detox).

**Limited Browser Support** - Focused pada Chromium-based browsers, Firefox, dan Edge. No Internet Explorer atau Safari (though Safari support in roadmap).

---

## <i class="fas fa-download"></i> Installation dan Setup

Getting started dengan Cypress incredibly simple - no complex configuration atau driver management.

### Prerequisites

**Node.js** - Cypress requires Node.js 12 atau higher:
```bash
# Check Node version
node --version

# Should be v12+ (v18+ recommended)
```

**npm atau yarn** - Package manager untuk install Cypress:
```bash
# Check npm
npm --version

# Or yarn
yarn --version
```

### Installation Steps

**1. Create Project (jika belum ada)**
```bash
mkdir my-cypress-tests
cd my-cypress-tests
npm init -y
```

**2. Install Cypress**
```bash
# Using npm
npm install cypress --save-dev

# Using yarn
yarn add cypress --dev
```

Installation downloads Cypress binary (~300MB) dan set up everything needed.

**3. Open Cypress**
```bash
# Using npx
npx cypress open

# Or add to package.json scripts
{
  "scripts": {
    "cy:open": "cypress open",
    "cy:run": "cypress run"
  }
}

# Then run
npm run cy:open
```

**4. First Launch**
Saat first open, Cypress create folder structure:
```
my-cypress-tests/
├── cypress/
│   ├── e2e/              # Test files go here
│   ├── fixtures/         # Test data (JSON files)
│   ├── support/          # Custom commands, utilities
│   └── videos/           # Recorded test runs
├── cypress.config.js     # Configuration
└── package.json
```

Dan generate example tests yang bisa langsung run.

### Configuration

**cypress.config.js:**
```javascript
const { defineConfig } = require('cypress')

module.exports = defineConfig({
  e2e: {
    baseUrl: 'http://localhost:3000',
    viewportWidth: 1280,
    viewportHeight: 720,
    video: true,
    screenshotOnRunFailure: true,
    
    setupNodeEvents(on, config) {
      // implement node event listeners here
    },
  },
})
```

**Common Configuration Options:**

| Option | Default | Description |
|---|---|---|
| `baseUrl` | null | Base URL untuk `cy.visit()` |
| `viewportWidth` | 1000 | Viewport width dalam pixels |
| `viewportHeight` | 660 | Viewport height dalam pixels |
| `defaultCommandTimeout` | 4000 | Time to wait untuk commands (ms) |
| `video` | true | Record video dari test runs |
| `screenshotOnRunFailure` | true | Auto screenshot saat test fail |
| `chromeWebSecurity` | true | Enable/disable web security |

---

## <i class="fas fa-code"></i> Anatomy of Cypress Test

Mari breakdown struktur dan syntax dari Cypress test.

### Basic Test Structure

```javascript
describe('Login Functionality', () => {
  beforeEach(() => {
    // Runs before each test
    cy.visit('/login')
  })

  it('should login with valid credentials', () => {
    // Test code
    cy.get('#username').type('testuser')
    cy.get('#password').type('password123')
    cy.get('button[type="submit"]').click()
    
    // Assertion
    cy.url().should('include', '/dashboard')
    cy.get('.welcome-message').should('contain', 'Welcome')
  })

  it('should show error with invalid credentials', () => {
    cy.get('#username').type('invalid')
    cy.get('#password').type('wrong')
    cy.get('button[type="submit"]').click()
    
    cy.get('.error-message')
      .should('be.visible')
      .and('contain', 'Invalid credentials')
  })
})
```

### Test Structure Components

**describe()** - Test suite, group related tests:
```javascript
describe('Feature Name', () => {
  // Tests go here
})

// Can be nested
describe('User Management', () => {
  describe('User Registration', () => {
    // Registration tests
  })
  
  describe('User Login', () => {
    // Login tests
  })
})
```

**it() / specify()** - Individual test case:
```javascript
it('should do something', () => {
  // Test implementation
})

// Or using specify (alias)
specify('user can logout', () => {
  // Test implementation
})
```

**Hooks** - Setup dan teardown:
```javascript
before(() => {
  // Runs once before all tests in block
  cy.task('seedDatabase')
})

beforeEach(() => {
  // Runs before each test
  cy.visit('/')
  cy.login('user', 'pass')  // Custom command
})

afterEach(() => {
  // Runs after each test
  cy.clearCookies()
})

after(() => {
  // Runs once after all tests in block
  cy.task('resetDatabase')
})
```

**Context** - Alias untuk describe, useful untuk grouping scenarios:
```javascript
context('When logged in', () => {
  beforeEach(() => {
    cy.login()
  })
  
  it('should display dashboard', () => {
    // Test
  })
})

context('When not logged in', () => {
  it('should redirect to login', () => {
    // Test
  })
})
```

---

## <i class="fas fa-mouse-pointer"></i> Core Commands

Cypress provides rich API untuk interacting dengan elements dan making assertions.

### Navigation Commands

```javascript
// Visit URL (relative to baseUrl)
cy.visit('/products')

// Visit absolute URL
cy.visit('https://example.com')

// Go back
cy.go('back')

// Go forward
cy.go('forward')

// Reload
cy.reload()
```

### Querying Commands

```javascript
// Get element by selector
cy.get('.btn-primary')
cy.get('#username')
cy.get('[data-testid="submit"]')

// Get by text content
cy.contains('Submit')
cy.contains('button', 'Submit')  // Button containing "Submit"

// Get within specific element
cy.get('.form').within(() => {
  cy.get('input').type('test')
  cy.contains('Submit').click()
})

// Find child elements
cy.get('.parent').find('.child')

// Filter elements
cy.get('li').filter('.active')

// Get first/last
cy.get('li').first()
cy.get('li').last()

// Get by index
cy.get('li').eq(2)  // Third item (0-indexed)

// Get parent
cy.get('.child').parent()

// Get siblings
cy.get('.item').siblings()

// Get closest ancestor
cy.get('.nested').closest('.container')
```

### Action Commands

```javascript
// Click
cy.get('button').click()
cy.get('.item').dblclick()       // Double click
cy.get('.link').rightclick()     // Right click

// Type
cy.get('input').type('Hello World')
cy.get('input').type('{enter}')  // Special keys
cy.get('input').type('{ctrl}A')  // Key combinations

// Clear
cy.get('input').clear()

// Check/Uncheck
cy.get('[type="checkbox"]').check()
cy.get('[type="checkbox"]').uncheck()
cy.get('[type="radio"]').check('option2')

// Select dropdown
cy.get('select').select('Option 1')
cy.get('select').select(['opt1', 'opt2'])  // Multiple

// Submit form
cy.get('form').submit()

// Focus/Blur
cy.get('input').focus()
cy.get('input').blur()

// Scroll
cy.scrollTo('bottom')
cy.scrollTo(0, 500)
cy.get('.footer').scrollIntoView()

// Trigger events
cy.get('.item').trigger('mouseenter')
```

### Assertions

```javascript
// Should syntax (recommended)
cy.get('.error')
  .should('be.visible')
  .and('contain', 'Error message')
  .and('have.class', 'error-red')

// Common assertions
.should('exist')
.should('not.exist')
.should('be.visible')
.should('be.hidden')
.should('be.enabled')
.should('be.disabled')
.should('be.checked')
.should('have.text', 'exact text')
.should('contain', 'partial text')
.should('have.value', 'input value')
.should('have.class', 'class-name')
.should('have.attr', 'href', '/path')
.should('have.length', 5)
.should('be.empty')

// Expect syntax (alternative)
cy.get('input').then(($input) => {
  expect($input).to.have.value('test')
  expect($input).to.be.visible
})

// Multiple assertions
cy.get('.list li')
  .should('have.length', 3)
  .and(($items) => {
    expect($items[0]).to.contain('First')
    expect($items[1]).to.contain('Second')
    expect($items[2]).to.contain('Third')
  })
```

### Network Commands

```javascript
// Intercept network requests
cy.intercept('GET', '/api/users').as('getUsers')
cy.visit('/users')
cy.wait('@getUsers')

// Stub response
cy.intercept('POST', '/api/login', {
  statusCode: 200,
  body: {
    user: 'test',
    token: 'abc123'
  }
})

// Spy on request
cy.intercept('POST', '/api/analytics').as('tracking')
cy.get('button').click()
cy.wait('@tracking').its('request.body')
  .should('deep.equal', { event: 'button_click' })

// Simulate network errors
cy.intercept('GET', '/api/data', {
  statusCode: 500,
  body: 'Internal Server Error'
})
```

---

## <i class="fas fa-graduation-cap"></i> Contoh Lengkap: E-Commerce Testing

Mari create comprehensive test suite untuk e-commerce application.

### Test Scenario: Product Purchase Flow

**cypress/e2e/purchase-flow.cy.js:**
```javascript
describe('Product Purchase Flow', () => {
  beforeEach(() => {
    // Visit homepage before each test
    cy.visit('/')
  })

  it('should complete full purchase journey', () => {
    // 1. Search for product
    cy.get('[data-testid="search-input"]')
      .type('Laptop')
    cy.get('[data-testid="search-button"]').click()

    // 2. Verify search results
    cy.get('.product-card')
      .should('have.length.greaterThan', 0)
      .first()
      .within(() => {
        cy.contains('Laptop').should('be.visible')
        cy.get('.price').should('exist')
        cy.contains('Add to Cart').click()
      })

    // 3. Verify cart updated
    cy.get('.cart-icon .badge')
      .should('contain', '1')

    // 4. Go to cart
    cy.get('.cart-icon').click()
    cy.url().should('include', '/cart')

    // 5. Verify cart contents
    cy.get('.cart-item')
      .should('have.length', 1)
      .within(() => {
        cy.contains('Laptop').should('be.visible')
        cy.get('.quantity').should('have.value', '1')
      })

    // 6. Proceed to checkout
    cy.contains('Proceed to Checkout').click()
    cy.url().should('include', '/checkout')

    // 7. Fill shipping information
    cy.get('#name').type('John Doe')
    cy.get('#email').type('john@example.com')
    cy.get('#address').type('123 Main St')
    cy.get('#city').type('Jakarta')
    cy.get('#postal').type('12345')

    // 8. Select payment method
    cy.get('[name="payment"]').check('credit-card')

    // 9. Fill payment details
    cy.get('#card-number').type('4111111111111111')
    cy.get('#card-name').type('John Doe')
    cy.get('#card-expiry').type('12/25')
    cy.get('#card-cvv').type('123')

    // 10. Submit order
    cy.get('[type="submit"]').click()

    // 11. Verify success
    cy.url().should('include', '/order-confirmation')
    cy.get('.success-message')
      .should('be.visible')
      .and('contain', 'Order placed successfully')
    
    // 12. Verify order number exists
    cy.get('.order-number')
      .should('match', /^ORD-\d+$/)
  })

  it('should handle out-of-stock products', () => {
    // Intercept API to simulate out-of-stock
    cy.intercept('GET', '/api/products/*', {
      statusCode: 200,
      body: {
        id: 1,
        name: 'Laptop',
        stock: 0,
        available: false
      }
    })

    cy.visit('/product/1')

    cy.get('.add-to-cart-button')
      .should('be.disabled')
    
    cy.get('.stock-status')
      .should('contain', 'Out of Stock')
      .and('have.class', 'text-danger')
  })

  it('should validate checkout form', () => {
    // Add item to cart first
    cy.visit('/product/1')
    cy.get('.add-to-cart-button').click()
    cy.get('.cart-icon').click()
    cy.contains('Proceed to Checkout').click()

    // Try to submit empty form
    cy.get('[type="submit"]').click()

    // Verify validation errors
    cy.get('#name-error')
      .should('be.visible')
      .and('contain', 'Name is required')
    
    cy.get('#email-error')
      .should('be.visible')
      .and('contain', 'Email is required')

    // Fill with invalid email
    cy.get('#name').type('John')
    cy.get('#email').type('invalid-email')
    cy.get('[type="submit"]').click()

    cy.get('#email-error')
      .should('contain', 'Invalid email format')
  })

  it('should calculate total correctly', () => {
    // Add multiple items
    cy.visit('/product/1')
    cy.get('.price').invoke('text').as('price1')
    cy.get('.add-to-cart-button').click()

    cy.visit('/product/2')
    cy.get('.price').invoke('text').as('price2')
    cy.get('.add-to-cart-button').click()

    // Go to cart
    cy.get('.cart-icon').click()

    // Verify subtotal
    cy.get('@price1').then((price1) => {
      cy.get('@price2').then((price2) => {
        const total = parseFloat(price1.replace(/[^0-9.-]+/g, '')) +
                     parseFloat(price2.replace(/[^0-9.-]+/g, ''))
        
        cy.get('.subtotal')
          .invoke('text')
          .then((subtotal) => {
            const subtotalValue = parseFloat(subtotal.replace(/[^0-9.-]+/g, ''))
            expect(subtotalValue).to.equal(total)
          })
      })
    })
  })
})
```

### Test dengan Custom Commands

**cypress/support/commands.js:**
```javascript
// Custom command untuk login
Cypress.Commands.add('login', (username, password) => {
  cy.visit('/login')
  cy.get('#username').type(username)
  cy.get('#password').type(password)
  cy.get('button[type="submit"]').click()
  cy.url().should('include', '/dashboard')
})

// Custom command untuk add product to cart
Cypress.Commands.add('addToCart', (productId) => {
  cy.visit(`/product/${productId}`)
  cy.get('.add-to-cart-button').click()
  cy.get('.success-toast')
    .should('be.visible')
    .and('contain', 'Added to cart')
})

// Custom command untuk clear cart
Cypress.Commands.add('clearCart', () => {
  cy.visit('/cart')
  cy.get('body').then(($body) => {
    if ($body.find('.cart-item').length > 0) {
      cy.get('.clear-cart-button').click()
      cy.get('.confirm-button').click()
    }
  })
})
```

**Usage dalam test:**
```javascript
describe('Logged in user flow', () => {
  beforeEach(() => {
    cy.login('testuser', 'password123')
    cy.clearCart()
  })

  it('should purchase product', () => {
    cy.addToCart(1)
    cy.get('.cart-icon').click()
    // Continue checkout...
  })
})
```

---

## <i class="fas fa-network-wired"></i> Network Testing

Cypress excels dalam testing applications yang heavily rely on network requests.

### Intercepting Requests

```javascript
describe('API Integration', () => {
  it('should load users from API', () => {
    // Intercept dan wait
    cy.intercept('GET', '/api/users').as('getUsers')
    
    cy.visit('/users')
    
    cy.wait('@getUsers').then((interception) => {
      expect(interception.response.statusCode).to.equal(200)
      expect(interception.response.body).to.have.length(10)
    })

    cy.get('.user-card').should('have.length', 10)
  })

  it('should handle API errors gracefully', () => {
    // Stub error response
    cy.intercept('GET', '/api/users', {
      statusCode: 500,
      body: {
        error: 'Internal Server Error'
      }
    }).as('getUsersError')

    cy.visit('/users')
    cy.wait('@getUsersError')

    cy.get('.error-message')
      .should('be.visible')
      .and('contain', 'Failed to load users')
  })

  it('should retry failed requests', () => {
    let attemptCount = 0

    cy.intercept('GET', '/api/data', (req) => {
      attemptCount++
      
      if (attemptCount < 3) {
        req.reply({
          statusCode: 500
        })
      } else {
        req.reply({
          statusCode: 200,
          body: { data: 'success' }
        })
      }
    }).as('getData')

    cy.visit('/data')
    
    // Should eventually succeed after retries
    cy.get('.data-display')
      .should('contain', 'success')
  })
})
```

### Testing Loading States

```javascript
it('should show loading spinner while fetching', () => {
  // Delay response
  cy.intercept('GET', '/api/products', (req) => {
    req.reply((res) => {
      res.delay = 2000  // 2 second delay
      res.send({
        statusCode: 200,
        body: [{ id: 1, name: 'Product' }]
      })
    })
  }).as('getProducts')

  cy.visit('/products')

  // Verify loading spinner shown
  cy.get('.loading-spinner').should('be.visible')

  cy.wait('@getProducts')

  // Verify spinner hidden after load
  cy.get('.loading-spinner').should('not.exist')
  cy.get('.product-card').should('be.visible')
})
```

### Mocking Data

```javascript
describe('Product Listing', () => {
  beforeEach(() => {
    // Load fixture data
    cy.fixture('products.json').then((products) => {
      cy.intercept('GET', '/api/products', {
        statusCode: 200,
        body: products
      }).as('getProducts')
    })
  })

  it('should display products from fixture', () => {
    cy.visit('/products')
    cy.wait('@getProducts')

    cy.get('.product-card')
      .should('have.length', 5)
      .first()
      .should('contain', 'Laptop')
  })
})
```

**cypress/fixtures/products.json:**
```json
[
  {
    "id": 1,
    "name": "Laptop",
    "price": 10000000,
    "stock": 10
  },
  {
    "id": 2,
    "name": "Mouse",
    "price": 200000,
    "stock": 50
  }
]
```

---

## <i class="fas fa-cog"></i> Advanced Features

### Custom Commands

Create reusable commands untuk common operations:

```javascript
// cypress/support/commands.js

// Login command
Cypress.Commands.add('login', (email, password) => {
  cy.session([email, password], () => {
    cy.visit('/login')
    cy.get('#email').type(email)
    cy.get('#password').type(password)
    cy.get('button[type="submit"]').click()
    cy.url().should('not.include', '/login')
  })
})

// Select dropdown by label
Cypress.Commands.add('selectByLabel', { 
  prevSubject: 'element' 
}, (subject, label) => {
  cy.wrap(subject)
    .find('option')
    .contains(label)
    .then(($option) => {
      cy.wrap(subject).select($option.val())
    })
})

// Wait for page load
Cypress.Commands.add('waitForPageLoad', () => {
  cy.window().then((win) => {
    return new Cypress.Promise((resolve) => {
      win.addEventListener('load', resolve)
    })
  })
})

// Check accessibility
Cypress.Commands.add('checkA11y', () => {
  cy.injectAxe()
  cy.checkA11y()
})
```

### Visual Testing

```javascript
// Using Percy for visual regression
describe('Visual Tests', () => {
  it('should match homepage snapshot', () => {
    cy.visit('/')
    cy.percySnapshot('Homepage')
  })

  it('should match product page snapshot', () => {
    cy.visit('/product/1')
    cy.percySnapshot('Product Detail Page')
  })
})

// Using native screenshots
it('should capture element screenshot', () => {
  cy.visit('/')
  cy.get('.hero-section').screenshot('hero-section')
})
```

### File Upload

```javascript
it('should upload profile picture', () => {
  cy.visit('/profile')
  
  cy.get('input[type="file"]')
    .selectFile('cypress/fixtures/avatar.jpg')
  
  cy.get('.upload-preview')
    .should('have.attr', 'src')
    .and('include', 'avatar')
})

// Upload multiple files
it('should upload multiple documents', () => {
  cy.get('input[type="file"]')
    .selectFile([
      'cypress/fixtures/doc1.pdf',
      'cypress/fixtures/doc2.pdf'
    ])
  
  cy.get('.file-list .file-item')
    .should('have.length', 2)
})
```

### Geolocation

```javascript
it('should use custom geolocation', () => {
  cy.visit('/', {
    onBeforeLoad(win) {
      cy.stub(win.navigator.geolocation, 'getCurrentPosition')
        .callsArgWith(0, {
          coords: {
            latitude: -6.2088,
            longitude: 106.8456
          }
        })
    }
  })

  cy.get('.location-display')
    .should('contain', 'Jakarta')
})
```

---

## <i class="fas fa-sync"></i> CI/CD Integration

Run Cypress tests dalam continuous integration pipeline.

### GitHub Actions

**.github/workflows/cypress.yml:**
```yaml
name: Cypress Tests

on: [push, pull_request]

jobs:
  cypress-run:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
      
      - name: Install dependencies
        run: npm ci
      
      - name: Start application
        run: |
          npm start &
          npx wait-on http://localhost:3000
      
      - name: Run Cypress tests
        uses: cypress-io/github-action@v5
        with:
          wait-on: 'http://localhost:3000'
          browser: chrome
          record: true
        env:
          CYPRESS_RECORD_KEY: ${{ secrets.CYPRESS_RECORD_KEY }}
      
      - name: Upload screenshots
        uses: actions/upload-artifact@v3
        if: failure()
        with:
          name: cypress-screenshots
          path: cypress/screenshots
      
      - name: Upload videos
        uses: actions/upload-artifact@v3
        if: always()
        with:
          name: cypress-videos
          path: cypress/videos
```

### Parallel Execution

```yaml
jobs:
  cypress-run:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        containers: [1, 2, 3, 4]  # 4 parallel jobs
    
    steps:
      - uses: actions/checkout@v3
      - uses: cypress-io/github-action@v5
        with:
          record: true
          parallel: true
          group: 'UI - Chrome'
        env:
          CYPRESS_RECORD_KEY: ${{ secrets.CYPRESS_RECORD_KEY }}
```

### Docker

**Dockerfile:**
```dockerfile
FROM cypress/included:12.17.0

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

CMD ["npx", "cypress", "run"]
```

**Run in Docker:**
```bash
docker build -t my-cypress-tests .
docker run -it my-cypress-tests
```

---

## <i class="fas fa-lightbulb"></i> Best Practices

### Do's ✅

**Use Data Attributes** - Prefer `data-testid` attributes untuk stable selectors:
```html
<button data-testid="submit-button">Submit</button>
```
```javascript
cy.get('[data-testid="submit-button"]').click()
```

**Avoid Hardcoded Waits** - Trust Cypress automatic waiting:
```javascript
// BAD
cy.wait(5000)
cy.get('.element').click()

// GOOD
cy.get('.element').should('be.visible').click()
```

**Use Aliases untuk Readability**:
```javascript
cy.get('.user-list').as('userList')
cy.get('@userList').should('have.length', 10)
cy.get('@userList').first().click()
```

**Keep Tests Independent** - Each test should run standalone:
```javascript
beforeEach(() => {
  cy.visit('/')
  cy.clearCookies()
  cy.clearLocalStorage()
})
```

**Test User Flows, Not Implementation**:
```javascript
// BAD - Testing implementation
it('should call API with correct params', () => {
  cy.intercept('POST', '/api/save').as('save')
  cy.get('button').click()
  cy.wait('@save').its('request.body')
    .should('have.property', 'id', 123)
})

// GOOD - Testing user perspective
it('should save changes', () => {
  cy.get('input').type('New value')
  cy.get('button').click()
  cy.get('.success-message')
    .should('contain', 'Saved successfully')
})
```

### Don'ts ❌

**Don't Use Arbitrary Waits** - `cy.wait(number)` should only untuk debugging:
```javascript
// Avoid
cy.wait(3000)

// Use instead
cy.get('.loading').should('not.exist')
```

**Don't Chain Too Many Commands** - Break complex chains untuk better error messages:
```javascript
// Hard to debug if fails
cy.get('.form').find('input').first().type('test').should('have.value', 'test')

// Better
cy.get('.form').find('input').first().type('test')
cy.get('.form').find('input').first().should('have.value', 'test')
```

**Don't Test Third-Party Integrations** - Mock external services:
```javascript
// Don't actually call payment gateway
cy.intercept('POST', '/api/payment', {
  statusCode: 200,
  body: { success: true }
})
```

**Don't Use cy.pause() in CI** - Only untuk local debugging.

**Don't Over-Use .then()** - Leverage Cypress commands when possible:
```javascript
// Unnecessary .then()
cy.get('.price').then(($price) => {
  const text = $price.text()
  expect(text).to.include('$')
})

// Better
cy.get('.price').should('include.text', '$')
```

---

## <i class="fas fa-quote-left"></i> Kesimpulan Utama

> "Cypress represents paradigm shift dalam end-to-end testing - dari painful, flaky, slow tests ke enjoyable, reliable, fast testing experience yang developers actually want to use."
{: .prompt-info }

**Ringkasan Penting:**

**Developer-First Experience** - Cypress built dengan developer experience sebagai priority. Real-time reload, time travel debugging, automatic waiting, dan clear error messages membuat testing enjoyable rather than chore.

**Architectural Advantages** - Running inside browser gives Cypress unprecedented control dan visibility. Native access ke application, DOM, network traffic, dan browser APIs enable powerful testing capabilities impossible dengan traditional tools.

**All-in-One Solution** - Cypress is complete package - test runner, assertion library, mocking, stubbing, dan visual testing all included. No decision fatigue about which libraries to combine.

**Fast Feedback Loop** - Tests run quickly, reload automatically, dan provide instant visual feedback. Development cycle drastically accelerated - write test, see results immediately, iterate rapidly.

**Reliable by Default** - Automatic waiting, retry logic, dan smart timeouts eliminate flaky tests. Once test passes, it consistently passes. Confidence dalam test results builds trust dalam testing process.

**Modern JavaScript Ecosystem** - Leveraging JavaScript dan Node.js ecosystem provides access ke vast tooling, libraries, dan integrations. Familiar syntax untuk frontend developers.

**Trade-offs Acknowledged** - JavaScript-only dan limited browser support are conscious trade-offs untuk incredible developer experience dan reliability. Right tool untuk right job - excellent untuk modern web apps, less suitable untuk legacy multi-language teams.

1. **Modern Architecture** - Runs in browser untuk unprecedented control
2. **Developer Experience** - Enjoyable testing yang actually gets used
3. **Automatic Waiting** - Reliable tests without explicit waits
4. **Visual Testing** - See exactly what happens at every step
5. **Fast Execution** - Quick feedback loop accelerates development
6. **All-in-One** - Complete testing solution out of box

---

## <i class="fas fa-book-open"></i> Referensi & Bacaan Lanjutan

**Official Resources:**
- **Cypress Documentation** - https://docs.cypress.io/
- **Cypress Blog** - Best practices dan case studies
- **Cypress YouTube Channel** - Tutorials dan webinars
- **Cypress GitHub** - Source code dan discussions

**Buku & Courses:**
- *End-to-End Web Testing with Cypress* - Waweru Mwaura
- *Cypress End-to-End Testing* - Packt Publishing
- **Test Automation University** - Free Cypress courses
- **Cypress Real World App** - Example application dengan tests

**Plugins & Tools:**
- **@testing-library/cypress** - Testing Library queries
- **cypress-axe** - Accessibility testing
- **cypress-visual-regression** - Visual testing
- **cypress-file-upload** - File upload testing
- **@percy/cypress** - Visual regression testing

**Community Resources:**
- **Cypress Discord** - Active community discussions
- **Stack Overflow** - Tag: cypress
- **Reddit** - r/QualityAssurance discussions
- **Gitter Chat** - Real-time help

**Best Practice Guides:**
- **Cypress Best Practices** - Official documentation
- **Real World Testing with Cypress** - Real World App
- **Effective Cypress** - Testing patterns
- **Cypress Anti-Patterns** - What to avoid

**Integration Examples:**
- **Next.js + Cypress** - Modern React testing
- **Vue + Cypress** - Vue application testing
- **React + Cypress** - React testing patterns
- **Angular + Cypress** - Angular integration

---

<div class="text-center text-muted small mt-5">
  <p class="mb-1"><i class="fas fa-users me-2"></i><strong>Kelompok 8</strong> • Pekan 8</p>
  <p class="mb-0">Materi Pengantar Cypress Testing Framework</p>
</div>