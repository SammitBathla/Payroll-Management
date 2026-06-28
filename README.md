# Payroll Management System

A full-stack web application for managing payroll operations, including batch creation, approval workflows, and transaction management.

## 📋 Project Overview

This project is a comprehensive payroll management system with the following features:

- **User Authentication** - JWT-based authentication
- **Payroll Creation** - Create and manage payroll batches
- **Batch Approval** - Multi-level approval workflow
- **Account Management** - Manage bank accounts and transactions
- **Transaction Printing** - Generate and print transaction reports
- **Dashboard** - Overview of payroll status and analytics
- **File Upload** - Bulk upload support for payroll data

## 🏗️ Architecture

### Tech Stack

**Backend:**

- **Framework:** Spring Boot 3.1.4
- **Language:** Java 17+
- **Database:** H2 (In-Memory for development)
- **Security:** Spring Security with JWT
- **Build Tool:** Maven 3.9.2

**Frontend:**

- **Framework:** React 19.2.0
- **UI Library:** React Bootstrap 2.10.10
- **HTTP Client:** Axios 1.13.1
- **Routing:** React Router DOM 7.9.4
- **Build Tool:** npm/Create React App

## 📁 Project Structure

```
Payroll-Management/
├── Payroll-Backend/
│   └── Payroll-backend/
│       └── Payroll-backend/
│           ├── pom.xml
│           ├── src/
│           │   ├── main/
│           │   │   ├── java/
│           │   │   │   └── com/payrollbackend/
│           │   │   │       ├── PayrollBackendApplication.java
│           │   │   │       ├── config/          # Security, JWT, Database config
│           │   │   │       ├── controller/      # REST API endpoints
│           │   │   │       ├── dto/             # Data Transfer Objects
│           │   │   │       ├── model/           # Entity models
│           │   │   │       ├── repository/      # Database access
│           │   │   │       └── service/         # Business logic
│           │   │   └── resources/
│           │   │       └── application.properties
│           │   └── test/
│           └── target/                          # Compiled artifacts
├── Payroll-Frontend/
│   ├── package.json
│   ├── public/
│   └── src/
│       ├── App.js                               # Main component
│       ├── LoginPage.js                         # Authentication
│       ├── Homepage.jsx                         # Dashboard
│       ├── Payroll.js                           # Payroll management
│       ├── BatchSummary.js                      # Batch operations
│       ├── ApproveHome.js                       # Approval workflow
│       ├── TransactionPrintArea.js              # Print functionality
│       └── ...other components
└── README.md                                    # This file
```

## 🚀 Getting Started

### Prerequisites

- **Java Development Kit (JDK)** 17 or higher
- **Node.js** and **npm** (v16 or higher)
- **Maven** 3.9.2 or higher
- **Git** for version control

### Installation & Setup

#### 1. Clone the Repository

```bash
git clone https://github.com/SammitBathla/Payroll-Management.git
cd Payroll-Management
```

#### 2. Backend Setup

Navigate to the backend directory:

```bash
cd Payroll-Backend/Payroll-backend/Payroll-backend
```

Build the project:

```bash
mvn clean install -DskipTests
```

#### 3. Frontend Setup

Navigate to the frontend directory:

```bash
cd Payroll-Frontend
npm install
```

### Running the Application

#### Start Backend Server

From `Payroll-Backend/Payroll-backend/Payroll-backend/`:

```bash
mvn spring-boot:run
```

The backend will start on **http://localhost:8081**

#### Start Frontend Development Server

From `Payroll-Frontend/`:

```bash
npm start
```

The frontend will start on **http://localhost:3000**

### Access Points

| Service     | URL                              | Purpose             |
| ----------- | -------------------------------- | ------------------- |
| Frontend    | http://localhost:3000            | User Interface      |
| Backend API | http://localhost:8081            | REST API Endpoints  |
| H2 Console  | http://localhost:8081/h2-console | Database Management |

## 📝 API Endpoints

### Authentication

- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login

### Dashboard

- `GET /api/dashboard/stats` - Get dashboard statistics

### Payroll Management

- `POST /api/payroll/create` - Create new payroll batch
- `GET /api/payroll/batches` - Get all payroll batches
- `GET /api/payroll/batch/{id}` - Get specific batch details

### Approval Workflow

- `GET /api/approval/pending` - Get pending approvals
- `POST /api/approval/approve/{id}` - Approve batch
- `POST /api/approval/reject/{id}` - Reject batch

### Account Management

- `GET /api/accounts` - Get all accounts
- `POST /api/accounts` - Create new account
- `PUT /api/accounts/{id}` - Update account

### Transactions

- `GET /api/transactions` - Get all transactions
- `GET /api/transactions/batch/{batchId}` - Get batch transactions

## 🔐 Authentication

The system uses JWT (JSON Web Tokens) for authentication:

1. User logs in with credentials
2. Server returns JWT token
3. Token is stored in local storage
4. Token is sent with each API request in Authorization header
5. Token is validated on backend before processing requests

### Default Test Credentials

The following test user accounts are available for development and testing:

| Role     | Username   | Password      | Permissions                         |
| -------- | ---------- | ------------- | ----------------------------------- |
| Operator | `operator` | `password` | Payroll creation, batch management  |
| Approver | `approver` | `password` | Batch approval, approval workflow   |
| Approver 1 | `approver1` | `password` | Batch approval, approval workflow   |
| Approver 2| `approver2` | `password` | Batch approval, approval workflow   |

**Note:** These are default credentials configured in the database seeding class. Change these credentials in production!

## 🗄️ Database

### H2 Database Console

Access the H2 console at: **http://localhost:8081/h2-console**

**Connection Details:**

- JDBC URL: `jdbc:h2:mem:payrolldb`
- Username: `sa`
- Password: (leave empty)

### Tables

- **account** - Bank accounts for payroll disbursement
- **payroll_batch** - Payroll batch records
- **payroll_batch_payment** - Individual payments in a batch
- **user** - User accounts (if applicable)

## 🔧 Configuration

### Backend Configuration

Edit `Payroll-Backend/Payroll-backend/Payroll-backend/src/main/resources/application.properties`:

```properties
# Server Port
server.port=8081

# Database Configuration
spring.datasource.url=jdbc:h2:mem:payrolldb
spring.datasource.driverClassName=org.h2.Driver
spring.h2.console.enabled=true

# JWT Secret (change in production)
jwt.secret=your-secret-key-here
jwt.expiration=86400000
```

### Frontend Configuration

Edit `Payroll-Frontend/src/api/axiosConfig.js`:

```javascript
const API_BASE_URL = "http://localhost:8081";
```

## 🧪 Testing

### Run Backend Tests

```bash
cd Payroll-Backend/Payroll-backend/Payroll-backend
mvn test
```

### Run Frontend Tests

```bash
cd Payroll-Frontend
npm test
```

## 🛠️ Development

### Backend Development

- Navigate to backend directory
- Use Maven for building: `mvn clean install`
- Use IDE (IntelliJ IDEA recommended) for development
- Run with: `mvn spring-boot:run`

### Frontend Development

- Navigate to frontend directory
- Run development server: `npm start`
- Makes changes to components in `src/`
- Hot-reload is enabled for quick feedback

## 📦 Building for Production

### Backend JAR

```bash
cd Payroll-Backend/Payroll-backend/Payroll-backend
mvn clean package -DskipTests
```

JAR file will be created at: `target/payroll-backend-0.0.1-SNAPSHOT.jar`

Run JAR:

```bash
java -jar target/payroll-backend-0.0.1-SNAPSHOT.jar
```

### Frontend Build

```bash
cd Payroll-Frontend
npm run build
```

Production files will be in `build/` directory.

## 📚 User Stories

### US1 - Authentication

User login and registration functionality with JWT token management.

### US2 - Home Dashboard

Overview page showing payroll status, pending approvals, and recent transactions.

### US3 - Payroll Creation

Create new payroll batches with employee payment details and validation.

### US4 - Batch Summary

View and manage payroll batches with filtering and search capabilities.

### US5 - Approval Workflow

Multi-level approval process for payroll batches before execution.

### US6 - Transaction Printing

Print and export transaction details in various formats (PDF, CSV).

## 🐛 Troubleshooting

### Backend won't start

- Ensure Java 17+ is installed: `java -version`
- Check Maven installation: `mvn -version`
- Clear Maven cache: `mvn clean`
- Check port 8081 is not in use: `netstat -ano | findstr :8081`

### Frontend won't load

- Clear node_modules: `rm -r node_modules && npm install`
- Clear npm cache: `npm cache clean --force`
- Check Node.js version: `node --version`
- Check port 3000 is not in use

### Database connection issues

- Ensure H2 database is properly configured
- Check `application.properties` JDBC URL
- Verify database file permissions

### CORS errors

- Ensure backend CORS configuration includes frontend URL
- Check `SecurityConfig.java` for proper CORS setup
- Frontend should request from `http://localhost:8081`

## 📋 Environment Variables

### Backend

```bash
# Set in application.properties
SERVER_PORT=8081
JWT_SECRET=your-secret-key
JWT_EXPIRATION=86400000
```

### Frontend

```bash
# Set in .env (if using Create React App)
REACT_APP_API_URL=http://localhost:8081
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit changes (`git commit -m 'Add YourFeature'`)
4. Push to branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💼 Author

**Sammit Bathla**

- GitHub: [@SammitBathla](https://github.com/SammitBathla)
- Project: [Payroll-Management](https://github.com/SammitBathla/Payroll-Management)

## 📞 Support

For issues, questions, or suggestions:

- Open an GitHub issue
- Contact: [Your Contact Information]

## 🎯 Roadmap

- [ ] Database migration to PostgreSQL for production
- [ ] Advanced reporting and analytics
- [ ] Mobile app support
- [ ] Multi-currency support enhancement
- [ ] Integration with payment gateways
- [ ] Automated backup and recovery
- [ ] Role-based access control (RBAC) enhancement
- [ ] Audit logging system

---

**Last Updated:** June 28, 2026
**Version:** 0.0.1-SNAPSHOT
