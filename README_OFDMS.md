# 🍔 Online Food Delivery Management System

> **CSC2108 — Introduction to Database** | AIUB | Section M, Group 09 | Fall 2024–25

A relational database system designed to manage the full lifecycle of online food orders — from customer registration and menu browsing to delivery tracking. Built with Oracle SQL and connected to a Java application via JDBC.

---

## 👥 Group Members

| Name | Student ID |
|---|---|
| Fahim Ahmed | 23-55423-3 |
| Sajal Kumar Ghosh | 23-55419-3 |
| Anika Tabassum | 23-55070-3 |
| Md. Towhidul Islam | 23-55036-3 |

**Supervised by:** Jubayer Ahamed

---

## 📋 Project Overview

The system connects three key stakeholders — **customers**, **restaurants**, and **delivery partners** — through a normalised relational database. Customers can browse menus, place orders, and have food delivered to their address. Restaurants prepare and manage incoming orders. Delivery partners are assigned to each order and ensure timely delivery.

### Entities
- **Customers** — CustomerID, Name, Phone, Address (City, Road, HouseNo)
- **FoodMenu** — FoodID, FoodName, Category, Price
- **Orders** — OrderID, OrderTime, OrderDate, Bill
- **DeliveryPartner** — DeliveryID, CompanyName, RiderName, RiderVehicle, Phone
- **Restaurant** — RestaurantID, RestaurantName, HelpLine, Location (City, ZIP, Road)

### Relationships
- Customers **Place** Orders
- Customers **Browse** FoodMenu (via Choice table)
- Orders are **Sent By** a DeliveryPartner
- Orders are **Handled By** a Restaurant

---

## 🗂️ Repository Structure

```
├── sql/
│   ├── ddl_table_creation.sql       # CREATE TABLE statements for all 10 tables
│   ├── dml_data_insertion.sql       # INSERT INTO statements with sample data
│   └── queries.sql                  # All query tests (basic, LIKE, functions, joins, views)
├── java/
│   ├── FoodMenu.java                # JDBC connection — FoodMenu table
│   ├── Customers.java               # JDBC connection — Customers table
│   ├── DeliveryPartner.java         # JDBC connection — DeliveryPartner table
│   └── Orders.java                  # JDBC connection — Orders table
├── docs/
│   └── G_9_M.pdf                    # Full project report
└── README.md
```

---

## 🗄️ Database Schema

### Tables Created (DDL)

| # | Table | Primary Key | Foreign Key(s) |
|---|---|---|---|
| 1 | FoodMenu | FoodID | — |
| 2 | Customers | CustomerID | — |
| 3 | Orders | OrderID | — |
| 4 | Choice | CustomerID | FoodID → FoodMenu |
| 5 | Address | — (City, Road, HouseNo) | — |
| 6 | DeliveryPartner | DeliveryID | — |
| 7 | Location | — (City, ZIP, Road) | — |
| 8 | OrdersPending | OrderID | CustomerID → Customers |
| 9 | OrderProcess | OrderID | DeliveryID → DeliveryPartner |
| 10 | Restaurant | RestaurantID | OrderID → Orders |

---

## 🔄 Normalization

All relations were normalized through **UNF → 1NF → 2NF → 3NF**. The four main relations analyzed were:

- **Browse** (Customer ↔ FoodMenu)
- **Place** (Customer ↔ Orders)
- **Sent By** (Orders ↔ DeliveryPartner)
- **Handled By** (Orders ↔ Restaurant)

Composite attributes like Address (City, Road, HouseNo) and Location (City, ZIP, Road) were decomposed into separate tables to achieve 3NF.

---

## 🔍 SQL Queries Covered

**a) Basic SELECT queries**
- Filter customers by city
- Filter food items by price threshold
- Retrieve restaurant helpline numbers
- Filter delivery partners by vehicle type

**b) LIKE operator**
- Search food names containing a pattern
- Search customer names starting with a letter

**c) Character Manipulation Functions**
- `UPPER()` and `LENGTH()` on customer names
- `SUBSTR()` on rider vehicle names

**d) DECODE Function**
- Conditional bill updates based on OrderID
- Conditional price updates based on FoodID

**e) Joins**
- Equijoin: Customers ↔ OrdersPending on CustomerID
- Non-equijoin: DeliveryPartner ↔ Orders with BETWEEN condition
- Outer join: Customers ↔ OrdersPending with `(+)` operator

**f) Views**
- `CustomersDetails` — simple view of customer info
- `CustomersOrders` — join view of customer names and their food choices

---

## ☕ Java Database Connection (JDBC)

Each member connected a different table to a Java application using **Apache NetBeans IDE 24**, **XAMPP (MySQL)**, and the `mysql-connector-java-8.0.30.jar` driver.

| Member | Table Connected |
|---|---|
| Fahim Ahmed | FoodMenu |
| Sajal Kumar Ghosh | Customers |
| Anika Tabassum | DeliveryPartner |
| Md. Towhidul Islam | Orders |

**Connection setup:**
```java
String url = "jdbc:mysql://localhost:3306/online food delivery management system";
String username = "root";
String password = "";
Connection conn = DriverManager.getConnection(url, username, password);
```

---

## 🛠️ Tools & Technologies

- **Database:** Oracle SQL (primary), MySQL via XAMPP (JDBC demo)
- **IDE:** Apache NetBeans IDE 24
- **Connectivity:** JDBC with `mysql-connector-java-8.0.30.jar`
- **Query Tool:** Oracle SQL Developer / phpMyAdmin

---

## 🚀 How to Run

### Oracle SQL
1. Open Oracle SQL Developer.
2. Run `ddl_table_creation.sql` to create all tables.
3. Run `dml_data_insertion.sql` to populate sample data.
4. Run queries from `queries.sql` to test.

### Java JDBC (MySQL)
1. Install [XAMPP](https://www.apachefriends.org/) and start Apache + MySQL.
2. Create a database named `online food delivery management system` in phpMyAdmin.
3. Create the relevant table and insert data.
4. Add `mysql-connector-java-8.0.30.jar` to your NetBeans project libraries.
5. Run the Java file for the table you want to connect to.

---

## 🔮 Future Scope

- AI-powered food recommendations based on order history
- Real-time GPS tracking for delivery personnel
- Dynamic sales dashboards for restaurants
- Third-party payment gateway integration
- Customer feedback and rating system

---

*Department of Electrical and Electronic Engineering, AIUB — Section M, Group 09 | Fall 2024–25*
