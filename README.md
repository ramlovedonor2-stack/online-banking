🏦 Online Banking System

A modular Online Banking and Accounting System built using Java, Spring, Spring Security, Spring Batch, PostgreSQL, Liquibase, Maven, and JUnit.

The system simulates core banking operations while separating customer-facing banking functionality, back-office customer onboarding, shared banking components, and scheduled transaction processing into independent modules.

---

📌 Project Overview

The application is designed around four major modules:

- BackOfficeSystem — manages customer onboarding through Capturer and Authoriser workflows.
- OnlineBanking — customer-facing banking application for account information and transactions.
- TransactionScheduling — background Spring Batch application for processing future-dated transactions.
- BankData — reusable shared library containing common banking functionality.

The modular structure follows the DRY (Don't Repeat Yourself) principle by keeping common functionality inside the reusable "BankData" library.

---

✨ Key Features

👤 Customer Banking

- Secure customer login
- Token-based authentication
- View account balance
- View transaction history
- Schedule future-dated transactions
- Receive account credentials through SMS

🏦 Back-Office Management

The back-office system follows a Maker-Checker / Capturer-Authoriser workflow.

Capturer

- Enter prospective customer details
- Submit account creation requests
- Update customer information when required
- Resubmit declined requests after corrections

Authoriser

- Review account creation requests
- Approve customer requests
- Decline requests with a reason
- Trigger customer account creation after approval
- Generate a unique account number
- Initiate delivery of customer login credentials

⏰ Scheduled Transactions

The system supports future-dated transactions.

A dedicated Spring Batch application:

1. Runs in the background.
2. Identifies transactions that are due for processing.
3. Processes the eligible transactions.
4. Completes the scheduled banking operation.
5. Records the transaction log in the database.

This architecture helps separate scheduled transaction processing from the customer-facing application.

🔐 Security

- Spring Security-based authentication
- Token-based authentication for subsequent requests
- Separate authentication for back-office users
- Role-based Capturer and Authoriser workflow

🧪 Testing

JUnit is used for unit and integration testing, particularly around the Online Banking customer system.

---

🏗️ System Architecture

                         ┌──────────────────────┐
                         │     Customer UI      │
                         │    Online Banking    │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   Spring Security   │
                         │ Authentication &    │
                         │ Token Validation    │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │     OnlineBanking    │
                         │  Customer Services   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │     PostgreSQL       │
                         │      Database        │
                         └──────────▲───────────┘
                                    │
                ┌───────────────────┴───────────────────┐
                │                                       │
                ▼                                       ▼
     ┌──────────────────────┐             ┌────────────────────────┐
     │   BackOfficeSystem   │             │ TransactionScheduling  │
     │                      │             │                        │
     │ Capturer             │             │ Spring Batch            │
     │ Authoriser           │             │ Future-dated payments  │
     │ Customer onboarding  │             │ Background processing  │
     └──────────┬───────────┘             └────────────┬───────────┘
                │                                      │
                └──────────────────┬───────────────────┘
                                   ▼
                         ┌──────────────────────┐
                         │       BankData       │
                         │   Shared Library     │
                         │ Common Components    │
                         └──────────────────────┘

---

🔄 Customer Account Creation Flow

Prospective Customer
        │
        ▼
   ┌───────────┐
   │ Capturer  │
   └─────┬─────┘
         │ Submit Request
         ▼
   ┌────────────┐
   │ Authoriser │
   └─────┬──────┘
         │
     ┌───┴───────────────┐
     │                   │
     ▼                   ▼
  APPROVE              DECLINE
     │                   │
     ▼                   ▼
Create Account       Send Back
     │                With Reason
     ▼
Generate Account
Number & Credentials
     │
     ▼
Send Credentials
to Customer

---

💳 Future-Dated Transaction Flow

Customer
   │
   ▼
Schedule Transaction
   │
   ▼
Store Future-Dated Transaction
   │
   ▼
PostgreSQL
   │
   ▼
Spring Batch Scheduler
   │
   ▼
Find Due Transactions
   │
   ▼
Process Transaction
   │
   ▼
Write Transaction Log

---

🧩 Project Structure

online-banking/
│
├── BackOfficeSystem/
│   └── Customer onboarding and Capturer/Authoriser workflows
│
├── OnlineBanking/
│   └── Customer-facing banking application
│
├── TransactionScheduling1/
│   └── Spring Batch application for scheduled transactions
│
├── BankData/
│   └── Shared reusable banking library
│
├── docs/
│   ├── architecture/
│   └── screenshots/
│
├── README.md
│
└── RequirementDoc_AccountingSystem.docx

---

🛠️ Technology Stack

Category| Technology
Programming Language| Java
Framework| Spring
Security| Spring Security
Batch Processing| Spring Batch
Database| PostgreSQL
Database Management| Liquibase
Build Tool| Maven
Testing| JUnit
Architecture| Modular / Microservice-oriented
Notifications| Fast2SMS

---

🔐 Authentication & Authorization

The application uses Spring Security to provide authentication.

The customer-facing application uses token-based authentication for requests after login.

The BackOffice module separates administrative responsibilities into two roles:

Role| Responsibility
Capturer| Creates and updates customer requests
Authoriser| Reviews, approves, or rejects requests

This separation implements a Maker-Checker style workflow, preventing a single role from completing the entire customer onboarding process.

---

⏱️ Spring Batch Processing

"TransactionScheduling1" is responsible for processing future-dated transactions.

The application runs a scheduled background process that checks for transactions that need to be processed and records the resulting transaction information.

This is particularly useful for scenarios such as:

- Future-dated payments
- Multiple transactions scheduled for the same day
- Salary/payment processing
- Background transaction execution

---

🗄️ Database

The project uses PostgreSQL for persistent banking data.

Liquibase is used for managing database changes and entries.

The database stores information required for:

- Customers
- Accounts
- Transactions
- Scheduled transactions
- Transaction logs
- Back-office workflows

---

🔌 API Modules

The application is divided into multiple functional areas.

Online Banking APIs

Responsible for customer-facing operations such as:

Authentication
Account information
Balance inquiry
Transaction history
Future-dated transaction scheduling

Back Office APIs

Responsible for:

Customer onboarding
Customer information updates
Capturer operations
Authoriser operations
Account approval/rejection

Transaction Scheduling

Responsible for:

Scheduled transaction retrieval
Transaction processing
Transaction completion
Transaction logging

«Add your actual endpoint URLs here once you document the controllers in the project.»

---

📸 Screenshots

Screenshots of the running application can be added here.

🔐 Customer Login

"Customer Login" (docs/screenshots/customer-login.png)

👤 Customer Dashboard

"Customer Dashboard" (docs/screenshots/customer-dashboard.png)

💰 Account Balance

"Account Balance" (docs/screenshots/account-balance.png)

📜 Transaction History

"Transaction History" (docs/screenshots/transaction-history.png)

📅 Schedule Transaction

"Schedule Transaction" (docs/screenshots/schedule-transaction.png)

🏦 Back Office — Capturer

"Capturer Dashboard" (docs/screenshots/capturer-dashboard.png)

✅ Back Office — Authoriser

"Authoriser Dashboard" (docs/screenshots/authoriser-dashboard.png)

---

🚀 Getting Started

Prerequisites

Install the following:

- Java JDK
- Maven
- PostgreSQL
- Git

Verify the installations:

java -version
mvn -version
psql --version
git --version

---

📥 Clone the Repository

git clone https://github.com/ramlovedonor2-stack/online-banking.git

cd online-banking

---

🗄️ Configure PostgreSQL

Create a PostgreSQL database for the application.

Then configure the database connection using environment-specific configuration rather than committing passwords or secrets to GitHub.

Example:

spring.datasource.url=jdbc:postgresql://localhost:5432/your_database
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}

---

⚙️ Build the Project

Navigate into the required module and build it using Maven:

mvn clean install

For the complete modular project, build the shared "BankData" component first so that dependent modules can use it.

---

▶️ Run the Applications

Start the required Spring applications individually.

For example:

mvn spring-boot:run

The exact command and configuration may vary depending on the module being started.

---

🧪 Run Tests

Execute the test suite using:

mvn test

JUnit is used for unit and integration testing.

---

📁 Module Responsibilities

BackOfficeSystem

Handles the administrative side of the banking platform.

Main responsibilities:

- Customer onboarding
- Capturer operations
- Authoriser operations
- Account approval
- Account rejection
- Customer information management

OnlineBanking

The customer-facing banking application.

Main responsibilities:

- Customer authentication
- Account balance
- Transaction history
- Future-dated transaction creation

TransactionScheduling1

A background Spring Batch application.

Main responsibilities:

- Identify due transactions
- Process scheduled transactions
- Record transaction logs

BankData

A reusable shared Java library.

Main responsibilities:

- Common banking functionality
- Shared components
- Avoiding duplicate implementation across modules

---

🎯 Key Technical Concepts Demonstrated

This project demonstrates practical experience with:

- Java
- Spring Framework
- Spring Security
- Authentication and authorization
- Token-based security
- Spring Batch
- Scheduled/background processing
- PostgreSQL
- Liquibase database management
- Maven multi-module development
- Reusable shared libraries
- REST-based application architecture
- JUnit testing
- Role-based workflows
- Transaction processing

---

🔮 Future Improvements

Potential improvements include:

- Docker and Docker Compose support
- CI/CD using GitHub Actions
- OpenAPI / Swagger documentation
- Centralized logging
- Improved API exception handling
- Integration tests using Testcontainers
- Monitoring and health checks
- Containerized PostgreSQL
- Production-ready environment configuration

---

👨‍💻 Author

Ramanjineyulu Nakka

GitHub:
https://github.com/ramlovedonor2-stack

---

⭐ Project

If you find this project useful or interesting, consider giving the repository a ⭐.

---

📄 License

This project is intended for educational and portfolio purposes.
