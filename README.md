# SM-Project
```markdown
# 🏫 Jakarta EE School Management System (SMS)

A modular **Jakarta EE 10** application built with **NetBeans**, **GlassFish 7**, and **MySQL 8**, following the *DICT312 Modular Tutorial Labs* from the University of Mpumalanga (UMP).

This project demonstrates an enterprise-grade **School Management System (SMS)** using multiple Jakarta EE technologies — REST, JSF, CDI, JPA, Security, JMS, WebSockets, and more — all integrated into one system.

---

## 🚀 Features

| Feature | Jakarta EE Module | Status |
|----------|-------------------|---------|
| Dependency Injection | CDI | ✅ Implemented |
| RESTful API | JAX-RS | ✅ Basic CRUD Endpoint |
| JSON Handling | JSON-B / JSON-P | ✅ Supported |
| Web Interface | JSF (Faces) | ✅ Working UI Page |
| Persistence | JPA (EclipseLink) | ⚙️ Partial (Lab 6 to complete) |
| Security | Jakarta Security | ⚙️ Pending (Lab 8) |
| Messaging | JMS + MDB | ⚙️ Pending (Lab 10–11) |
| Validation | Bean Validation | ⚙️ Pending (Lab 12) |
| SOAP Web Services | JAX-WS | ⚙️ Pending (Lab 13) |

---

## 🧩 Project Structure

```

sms-parent/     → Maven parent (manages all modules)
sms-model/      → JPA entities & shared domain model
sms-rest/       → RESTful APIs (JAX-RS)
sms-jsf/        → JSF Admin UI
sms-ejb/        → EJB & scheduled tasks
sql/            → Database schema (MySQL)

````

---

## 🛠️ Technologies Used

- **Jakarta EE 10**
- **GlassFish 7**
- **JDK 17+**
- **MySQL 8**
- **Maven (multi-module)**
- **NetBeans IDE**
- **EclipseLink JPA**
- **Jakarta Faces (JSF)**
- **Jakarta RESTful Web Services (JAX-RS)**
- **Jakarta Messaging (JMS)**

---

## ⚙️ Setup Instructions

### 1️⃣ Prerequisites
Make sure you have installed:
- JDK 17 or newer  
- NetBeans (latest release)
- GlassFish Server 7+  
- MySQL 8.x  

---

### 2️⃣ Database Setup (MySQL)

1. Open MySQL and run the provided SQL file:
   ```bash
   mysql -u root -p < sql/schema.sql
````

2. This creates the database `sms` and the following tables:

   ```
   roles, users, user_roles, lecturers, students, courses, enrollments, grades
   ```
3. The script also inserts default roles: **ADMIN**, **LECTURER**, **STUDENT**.

---

### 3️⃣ GlassFish Configuration

1. Copy **MySQL Connector/J** (`mysql-connector-j-8.x.jar`) into:

   ```
   glassfish/domains/domain1/lib/
   ```

2. Restart GlassFish.

3. Create JDBC & JMS resources (either in Admin Console or using `asadmin`):

   ```bash
   asadmin start-domain domain1

   asadmin create-jdbc-connection-pool \
     --restype javax.sql.DataSource \
     --driverclassname com.mysql.cj.jdbc.Driver \
     --property user=sms_user:password=yourpassword:URL=jdbc\\:mysql\\://localhost\\:3306/sms?serverTimezone\\=Africa/Johannesburg\\&useSSL\\=false mysqlPool

   asadmin create-jdbc-resource --connectionpoolid mysqlPool jdbc/smsDS

   asadmin create-jms-resource --restype jakarta.jms.ConnectionFactory jms/smsCF

   asadmin create-jms-resource --restype jakarta.jms.Queue --property Name=gradeQueue jms/gradeQueue
   ```

---

### 4️⃣ Import & Build

In **NetBeans**:

1. Go to **File → Open Project**
2. Select the folder `sms-parent`
3. Right-click → **Clean and Build**
4. Once built successfully:

   * Right-click → **Run** or **Deploy** each web module.

---

## 🌐 How to Access

### REST API (Test with Postman)

* **GET** → `http://localhost:8080/sms-rest/api/students`
* **POST** → `http://localhost:8080/sms-rest/api/students` (JSON payload)

Example Response:

```json
[
  {
    "id": 1,
    "studentNo": "S0001",
    "firstName": "Test",
    "lastName": "Student",
    "email": "test.student@example.com"
  }
]
```

### JSF Admin UI

Visit:
👉 `http://localhost:8080/sms-jsf/index.xhtml`

---

## 🧠 Learning Objectives

After completing all labs, you will be able to:

* Design a modular Jakarta EE system.
* Expose REST APIs and consume JSON data.
* Implement security using DB identity stores.
* Add asynchronous communication via JMS.
* Integrate WebSockets for live updates.
* Deploy, test, and debug enterprise Java applications.

---

## 🧾 Academic Labs Progress

| Lab    | Description                          | Status         |
| ------ | ------------------------------------ | -------------- |
| Lab 0  | Environment, Database & Server Setup | ✅ Done         |
| Lab 1  | CDI                                  | ✅ Done         |
| Lab 2  | REST (JAX-RS)                        | ✅ Done         |
| Lab 3  | JSON-B/JSON-P                        | ✅ Done         |
| Lab 4  | Microservices Gateway                | ⚙️ Pending     |
| Lab 5  | JSF Admin UI                         | ✅ Done         |
| Lab 6  | Persistence (JPA)                    | ⚙️ In Progress |
| Lab 7  | WebSocket                            | ⚙️ Pending     |
| Lab 8  | Security                             | ⚙️ Pending     |
| Lab 9  | Servlet (CSV Upload)                 | ⚙️ Pending     |
| Lab 10 | EJB                                  | ⚙️ Partial     |
| Lab 11 | Messaging (JMS + MDB)                | ⚙️ Pending     |
| Lab 12 | Bean Validation                      | ⚙️ Pending     |
| Lab 13 | SOAP (JAX-WS)                        | ⚙️ Pending     |
| Final  | Full Integration                     | ⚙️ Pending     |

---

## 📂 Folder Highlights

```
📁 sms-model/
 └── Student.java          → JPA entity class
📁 sms-rest/
 ├── SmsApplication.java   → REST application root
 └── StudentResource.java  → REST endpoints
📁 sms-jsf/
 ├── index.xhtml           → Main admin UI
 └── CourseView.java       → JSF backing bean
📁 sms-ejb/
 └── EnrollmentService.java → EJB for background tasks
📁 sql/
 └── schema.sql            → MySQL setup script
```

---

## 🧑‍💻 Contributors

* **Ashley Mash** – Lead Developer
* **University of Mpumalanga (UMP)** – Academic Guidance
* Contributions welcome! Fork the repo and submit pull requests.

---

## 🧾 License

This project is for educational purposes and academic assessment under the **University of Mpumalanga (UMP) DICT312 Module**.
You are free to reuse and adapt for learning, but please credit the original source.


---

### ⭐ Star this repo if you found it helpful!

```

