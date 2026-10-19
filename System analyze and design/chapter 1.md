---
title: Data Models
aliases:
  - Data Model
  - Database Design
tags:
  - database
  - data-model
  - dbms
  - lecture
created: 2026-10-19
source: class slides
---

# Data Models

> [!summary] Summary
> A **data model** represents real-world data in a clear form and hides storage details. Its building blocks are **structure**, **constraints**, and **query language**. It has three levels: **conceptual**, **logical**, and **physical**.

## Contents
- [[#Why analysts need a data model]]
- [[#Key terms]]
- [[#Building blocks]]
- [[#Three levels of data models]]
- [[#Database design process]]
- [[#Types of data models]]
- [[#Choosing a data model]]
- [[#Uses and importance]]
- [[Data base]]

---

## Why analysts need a data model

**Analysis phase**
- Analysts need to understand the data the business uses and creates (for example, customer and order data).
- A data model shows the logical organization of data without saying how it is stored, created, or manipulated. This lets analysts focus on the business, not technical details.

**Design phase**
- The data model is later changed to show exactly how data will be stored in databases and files.

> [!example] Example: online bookstore
> - **Analysis:** "A customer places orders for books."
> - **Design:** an `ORDERS` table with `order_id`, `order_date`, and `customer_id` columns.

## Key terms

| Term             | Meaning                                                           | Example                    |
| ---------------- | ----------------------------------------------------------------- | -------------------------- |
| **Data model**   | Describes and standardizes how data elements relate to each other |                            |
| **Entity**       | A real-world object or concept                                    | Customer                   |
| **Attribute**    | A property of an entity                                           | Name, phone number         |
| **Relationship** | A connection between entities                                     | A customer places an order |
| **Constraint**   | A rule that defines valid data                                    | A unique customer ID       |
| **Schema**       | The structure of a database: tables, columns, keys                |                            |

## Building blocks

- **Entities:** real-world objects or concepts with a distinct existence, such as Customer, Product, Order.
- **Attributes:** properties of an entity, such as ID, name, address, phone, email.
- **Relationships:** connections between entities, such as a customer places an order, or a product belongs to a category.
- **Constraints:** rules for valid data, such as a customer must have a unique ID, or an order cannot exist without products.

## Three levels of data models

| Level             | Abstraction | Shows                                       | Used by                         | Output                         |
| ----------------- | ----------- | ------------------------------------------- | ------------------------------- | ------------------------------ |
| **1. Conceptual** | High        | Entities, relationships, constraints        | Business stakeholders, analysts | ER diagram                     |
| **2. Logical**    | Medium      | Tables, columns, primary keys, foreign keys | Analysts, database designers    | Relational schema              |
| **3. Physical**   | Low         | DBMS, data types, indexes, storage          | DBAs, developers                | SQL schema and technical specs |

### 1. Conceptual 
- Gives a global view of the data. It identifies entities, relationships, and constraints without implementation details.
- Example: an ER diagram with Customer and Order.
- *One customer makes many orders. An order includes many products, and a product can appear in many orders.* Key attributes are underlined in the ER diagram.

### 2. Logical model
- Refines the conceptual model by specifying each entity's attributes and relationships in more detail. It is still independent of the physical implementation.

**Conversion rules (conceptual → logical)**

| Conceptual | Logical |
|---|---|
| Entity | Table |
| Attribute | Column |
| Identifier | Primary key (PK) |
| One-to-many relationship | Foreign key (FK) in the "many" table |
| Many-to-many relationship | Link table with two FKs |

**Pizza ordering example**
- **Customer:** CustomerID (PK), Fname, Lname, Address, Phone, E-mail
- **OrderHeader:** OrderID (PK), OrderDate, OrderTime, CustomerID (FK)
- **OrderLine:** OrderID (PK, FK), LineID (PK), PizzaID (PK, FK), Quantity
- **Pizza:** PizzaID (PK), Name, Specification, Price
- **Delivery:** DeliveryID (PK), OrderID (FK), Type, Status, Departure, Arrival
- **Payment:** PaymentID (PK), PDate, Type, OrderID (FK), CustomerID (FK), Total

> [!tip] Reading the diagram
> - PK = primary key, FK = foreign key.
> - A bar means "one"; a crow's foot (three prongs) means "many."
> - `OrderLine` is the link table between `OrderHeader` and `Pizza`. Its key is (OrderID, LineID).

### 3. Physical model
- Adds DBMS details: data types, indexes, partitions, and storage.

```sql
CREATE TABLE Customer (
    Customer_OID   CHAR(16) PRIMARY KEY,
    Customer_Number INTEGER,
    First_Name     CHAR(20),
    Surname        CHAR(20),
    Salutation     CHAR(5),
    Phone_Number   CHAR(20)
);

CREATE INDEX idx_customer_surname
ON Customer (Surname);
```

> Data types, indexes, and partitions are DBMS-specific.

## Database design process

### Functional (application) side
1. **Functional requirements:** from requirements collection and analysis
2. **Functional analysis:** output is a high-level transaction specification
3. **Application program design:** uses the logical schema
4. **Transaction implementation:** output is application programs

### Data (database) side
1. **Requirements collection and analysis:** output is data requirements
2. **Conceptual design:** output is the conceptual schema (high-level model)
3. **Logical design (data model mapping):** output is the logical schema (specific to a DBMS)
4. **Physical design:** output is the internal schema

### Design steps

| Step                             | Description                                                                           | Issues                                               | Input                                                  | Output            |
| -------------------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------ | ----------------- |
| **a. Conceptual design**         | Capture major entities, relationships, and attributes                                 | Capturing all data and relationships; data integrity | Functional specs; general understanding of the problem | ER diagram        |
| **b. Logical design**            | Turn entities, attributes, and relationships into a high-level database specification | Providing a location for all data; data integrity    | ER diagram                                             | Relational schema |
| **b2. Improving logical design** | Improve the high-level specification                                                  | Minimizing redundancy and ambiguity                  | Relational schema                                      |                   |
+ 4 types of attributes:
	 - unique key attribute : using unique entity
	 - calculate able attribute : using dash entity
	 - normal attribute : using normal entity
	 - more then one attributes : phone number, using two layer entity

+ Relationship : using diamond shape to make relation between entities
+ 3 types of cardinality : 
	 - one to one : 1 - 1
	 - one to many : 1 - n
	 - many to many : m - n
+ one entity should has one unique key only unless that unique key has to combine with another to different unique keys to make another one unique