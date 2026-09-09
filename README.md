# AIHT CSBS TEAM-G09
# College Merchandise & Uniform Store – Pre-Order System

A full-stack web application that lets AIHT students browse, pre-order, and track college merchandise and uniforms. Administrative staff can manage inventory, update order status, and view stock aggregation reports.

---

## Technology Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML5 · CSS3 · JavaScript ES6+ |
| Backend | Spring Boot 3.2 · Java 17 |
| ORM | Spring Data JPA / Hibernate 6 |
| Database | MySQL 8.0 |
| Build | Apache Maven 3.9+ |

---

## Project Structure

```
college-merch-store/
├── phase1-requirements/
│   └── requirements.md          # Personas, user stories, MoSCoW, NFRs
│
├── phase2-architecture/
│   ├── architecture.md          # 3-tier diagram + Mermaid
│   ├── schema.sql               # MySQL schema + 5 sample rows/table
│   ├── data-dictionary.md       # Column-level documentation
│   └── api-contract.md          # REST API reference
│
├── phase3-frontend/
│   ├── index.html               # Product catalogue + cart + checkout
│   ├── orders.html              # Order tracker
│   ├── admin.html               # Admin dashboard (3 tabs)
│   ├── css/styles.css           # Responsive stylesheet
│   └── js/
│       ├── api.js               # REST API fetch wrappers
│       └── utils.js             # Shared utilities (toast, formatINR, etc.)
│
├── phase3-backend/
│   ├── pom.xml                  # Maven build file
│   └── src/main/
│       ├── java/com/aiht/merch/
│       │   ├── MerchStoreApplication.java
│       │   ├── config/CorsConfig.java
│       │   ├── controller/
│       │   │   ├── ProductController.java
│       │   │   ├── OrderController.java
│       │   │   └── StudentController.java
│       │   ├── service/
│       │   │   ├── ProductService.java
│       │   │   ├── OrderService.java
│       │   │   └── StudentService.java
│       │   ├── repository/
│       │   │   ├── ProductRepository.java
│       │   │   ├── ProductSizeRepository.java
│       │   │   ├── OrderRepository.java
│       │   │   ├── PaymentRepository.java
│       │   │   └── StudentRepository.java
│       │   ├── entity/
│       │   │   ├── Student.java
│       │   │   ├── Product.java
│       │   │   ├── ProductSize.java
│       │   │   ├── Order.java
│       │   │   ├── OrderItem.java
│       │   │   └── Payment.java
│       │   ├── dto/
│       │   │   ├── ApiResponse.java
│       │   │   ├── ProductDTO.java
│       │   │   ├── StudentDTO.java
│       │   │   ├── OrderDTO.java
│       │   │   └── SizeSummaryDTO.java
│       │   └── exception/
│       │       └── GlobalExceptionHandler.java
│       └── resources/
│           └── application.properties
│
└── phase4-deployment/
    ├── run_project.bat          # Windows one-click launcher
    ├── presentation.html        # 8-slide interactive presentation
    └── runbook-sheets-8-12.md   # Deployment + test runbook
```

---

## Quick Start

### Prerequisites
- JDK 17+ — [Download Adoptium](https://adoptium.net/)
- Apache Maven 3.9+ — [Download Maven](https://maven.apache.org/download.cgi)
- MySQL 8.0 running on `localhost:3306`

### Step 1 – Create the Database
```sql
mysql -u root -p
source phase2-architecture/schema.sql;
```

### Step 2 – Configure Your MySQL Password
Edit `phase3-backend/src/main/resources/application.properties`:
```properties
spring.datasource.password=YOUR_MYSQL_PASSWORD
```

### Step 3 – Build & Run

**Windows (one click):**
```bat
phase4-deployment\run_project.bat
```

**Manual:**
```bat
cd phase3-backend
mvn clean package -DskipTests
java -jar target\merch-store-1.0.0.jar
```

### Step 4 – Open the Frontend
Open `phase3-frontend/index.html` in your browser while the backend is running.

The frontend works **offline in demo mode** even without the backend running.

---

## API Base URL

```
http://localhost:8080/api
```

Key endpoints:

| Method | Endpoint | Description |
|--------|---------|-------------|
| GET | /api/products | List all products |
| GET | /api/products/size-summary | Stock per size |
| POST | /api/orders | Place a pre-order |
| GET | /api/orders | List all orders |
| PUT | /api/orders/{id}/status | Update order status |
| POST | /api/students | Register a student |

All responses follow: `{ "success": true, "data": {...}, "message": "..." }`

---

## Default Test Data

After running schema.sql, 5 students, 5 products, 5 orders, and 5 payments are loaded.

- Student IDs: 1–5
- Default password for all students: `Password@1`

---

## Security Notes

- Passwords are stored as BCrypt hashes (cost 12)
- All user input is HTML-escaped (XSS prevention)
- JPA parameterised queries prevent SQL injection
- For production: restrict CORS origins in `CorsConfig.java` and add JWT authentication

---

## Team

**AIHT CSBS TEAM-G09** · Academic Year 2024–25 · Arulmigu Institute of Technology and Humanities
