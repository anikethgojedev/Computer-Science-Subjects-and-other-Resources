Suggested flow :
Database basics → SQL/DBMS → tables → datatypes → keys/constraints → SELECT → WHERE/operators → LIMIT → ORDER BY → aggregate functions → GROUP BY → HAVING → and the later SQL topics in the document.

The notes and leanrnig now -

---
Part 1
# 1. First: What is data?

Before understanding a database, understand **data**.

Data is information that can be stored and processed.

For example:



```
101
Rahul
22
Delhi
85
```

Individually, these are pieces of data.

Put them together:

| id | name | age | city | marks |
| --- | ---- | --- | ---- | ----- |
| 101                | Rahul | 22 | Delhi  | 85 |
| 102                | Priya | 21 | Mumbai | 91 |
| 103                | Aman  | 23 | Pune   | 78 |

Now the data has **structure**.

This is where databases become useful.

---

# 2. What is a Database?

Your notes define a database as:

> **A collection of interrelated data.**

Think of a database as a **container that organizes related information**.

Imagine Amazon.

It might need to store:



```
Customers
Products
Orders
Payments
Reviews
Addresses
Categories
Employees
```

These aren't random pieces of information.

They are **related**.

For example:



```
Customer
   ↓
places
   ↓
Order
   ↓
contains
   ↓
Product
```

So a database allows an application to organize all of this information and maintain relationships between pieces of data.

### Mental model

Think:



```
DATABASE
│
├── Customers
├── Products
├── Orders
├── Payments
└── Reviews
```

Each of these can be represented by a table in a relational database.

---

# 3. What is a DBMS?

Now comes an extremely important distinction.

A **database is not the software**.

Your notes define:

> **DBMS (Database Management System) is software used to create, manage, and organize databases.**

So:



```
Database = the organized data
DBMS     = software that manages that data
```

### Analogy

Imagine a library.



```
Books       → Database
Librarian   → DBMS
```

The books contain the information.

The librarian helps you:

-  add books
-  find books
-  remove books
-  organize books
-  maintain records

Similarly, a DBMS manages your data.

---

# 4. Why do we need a DBMS?

Suppose you have 10 million customers.

You could theoretically store them in a giant text file:



```
101,Rahul,Delhi
102,Priya,Mumbai
103,Aman,Pune
...
```

But now imagine asking:

> Find every customer from Delhi whose age is greater than 25.

You would need software capable of efficiently:

1.  locating the data
2.  interpreting its structure
3.  filtering it
4.  returning the result

And real databases have much harder requirements:

-  multiple users accessing data simultaneously
-  security
-  data consistency
-  relationships between data
-  backups
-  transactions
-  permissions
-  efficient searching
-  handling millions/billions of records

That's why we use a DBMS.

---

# 5. DBMS vs Database

This is a **classic interview question**.

### Database

The actual organized collection of data.

### DBMS

The software used to manage that data.

So don't say:

> "MySQL is a database."

More precisely:

> **MySQL is a relational database management system (RDBMS).**

Your notes explicitly distinguish SQL and MySQL as well: SQL is the language used to perform operations on relational databases, while MySQL is an RDBMS that uses SQL.

---

# 6. What is an RDBMS?

Now we reach the most important part for your **SQL interview preparation**.

RDBMS =

> **Relational Database Management System**

Your notes describe it as a DBMS based on the concept of **tables (relations)**, where data is organized into rows and columns.

For example:

### `students`

| id | name | age | city |
| --- | ---- | --- | ---- |
| 1             | Rahul | 21 | Delhi  |
| 2             | Priya | 22 | Mumbai |
| 3             | Aman  | 20 | Pune   |

This is a relation/table.

The important idea is:



```
RDBMS
  ↓
Tables
  ↓
Rows + Columns
```

---

# 7. Why "relational"?

This is where beginners often memorize the word without understanding it.

Suppose we have:

### `customers`

| customer\_id | name |
| --------------- | ---- |
| 1                | Rahul |
| 2                | Priya |
| 3                | Aman  |

And:

### `orders`

| order\_id | customer\_id | amount |
| -------- | ----------- | ------ |
| 101                         | 1 | 500 |
| 102                         | 1 | 700 |
| 103                         | 2 | 300 |

Notice:



```
customers.customer_id
          ↑
          │
orders.customer_id
```

The `customer_id` connects the two tables.

Therefore:



```
Customers
    │
    │ customer_id
    │
    ▼
Orders
```

That's the **relational** idea.

And this becomes incredibly important later when we learn:

> **JOINs**

In fact, a huge portion of the LeetCode SQL 50 is basically training you to reason about relationships between tables.

For example:

-  \#1378 Replace Employee ID With The Unique Identifier
-  \#1068 Product Sales Analysis I
-  \#1581 Customer Who Visited but Did Not Make Any Transactions
-  \#577 Employee Bonus
-  \#1280 Students and Examinations

All of these depend on understanding relationships between tables.

---

# 8. Relational vs Non-relational

Your notes introduce two broad categories:



```
Databases
│
├── Relational
│
└── Non-relational (NoSQL)
```

The notes describe relational databases as storing data in tables and non-relational databases as not using tables in the relational sense.

For our learning journey, we're primarily interested in:

# Relational databases

Examples from your notes include:

-  MySQL
-  PostgreSQL
-  Oracle
-  SQL Server

And one NoSQL example shown in the notes is MongoDB.

### Relational example



```
Customers
Orders
Products
Payments
```

with structured tables and relationships.

### Non-relational idea

Data can instead be represented in structures such as documents.

For example, conceptually:



```
{
  "customer_id": 1,
  "name": "Rahul",
  "orders": [
    {
      "product": "Laptop",
      "amount": 50000
    }
  ]
}
```

For **your current goal**, don't get distracted by NoSQL.

Your target is:



```
RDBMS
  ↓
SQL
  ↓
MySQL
  ↓
SQL 50
  ↓
Interviews
```

---

# 9. Then what exactly is SQL?

This distinction is **VERY important**.

Your notes say:

> SQL = Structured Query Language

and describe it as the language used to store, manipulate, and retrieve data from an RDBMS.

So:



```
SQL ≠ Database
SQL ≠ DBMS
SQL ≠ MySQL
```

Instead:



```
SQL
 ↓
Language
```

while:



```
MySQL
 ↓
RDBMS/software
```

And:



```
Database
 ↓
Data
```

---

# 10. The whole relationship

This is the picture I want you to remember:



```
                 YOU
                  │
                  │ SQL query
                  ▼
             ┌─────────┐
             │  MySQL  │
             │  RDBMS  │
             └────┬────┘
                  │
                  │ manages
                  ▼
             ┌──────────┐
             │ DATABASE │
             └────┬─────┘
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
    Customers   Orders   Products
      TABLE      TABLE     TABLE
```

So when you write:



```
SELECT *
FROM customers;
```

you're using **SQL** to ask **MySQL** to retrieve information from a **database/table**.

That's the entire ecosystem.

---

# 11. SQL vs MySQL — interview question

### Question

**What is the difference between SQL and MySQL?**

### Weak answer ❌

> SQL and MySQL are databases.

Wrong.

### Better answer

> SQL is a language used to interact with relational databases, while MySQL is a relational database management system that uses SQL.

That's essentially the distinction made in your notes.

### Interview-quality answer

> **SQL is a standardized language for querying and manipulating relational data. MySQL is an RDBMS that implements SQL and provides the software infrastructure for storing, managing, and retrieving that data.**

That is the level I want you eventually answering at.

---

# 12. What is a table?

A relational database organizes data into tables.

For example:



```
Database: college
```

could contain:



```
students
teachers
courses
departments
```

The `students` table might be:

| id | name | age | city |
| --- | ---- | --- | ---- |
| 1             | Rahul | 21 | Delhi  |
| 2             | Priya | 22 | Mumbai |
| 3             | Aman  | 20 | Pune   |

Now learn two words:

### Row

One complete record.



```
1 | Rahul | 21 | Delhi
```

That's one row.

### Column

One attribute/property.



```
name
age
city
```

are columns.

So:



```
TABLE
│
├── Columns → attributes
│
└── Rows    → records
```

This distinction will become absolutely critical once we reach:



```
WHERE
GROUP BY
COUNT
JOIN
HAVING
```

---

# 13. Database structure

Your notes visually represent the basic structure as:



```
Database
│
├── Table 1
│    └── Data
│
└── Table 2
     └── Data
```

Let's make that more realistic:



```
company_db
│
├── employees
│   ├── employee_id
│   ├── name
│   ├── department_id
│   └── salary
│
├── departments
│   ├── department_id
│   └── department_name
│
└── projects
    ├── project_id
    └── project_name
```

Now we have a **relational database**.

The tables don't exist independently.

They can be related.



```
employees.department_id
          │
          ▼
departments.department_id
```

This is the foundation for JOINs.

---

# 14. CRUD

Your notes introduce SQL in terms of CRUD:



```
C → Create
R → Read
U → Update
D → Delete
```

Conceptually:

| CRUD | Meaning |
| ----- | ------- |
| Create      | Add data      |
| Read        | Retrieve data |
| Update      | Modify data   |
| Delete      | Remove data   |

For example:

### Create



```
INSERT INTO students
VALUES (1, 'Rahul', 21);
```

### Read



```
SELECT *
FROM students;
```

### Update



```
UPDATE students
SET age = 22
WHERE id = 1;
```

### Delete



```
DELETE FROM students
WHERE id = 1;
```

### Important interview precision

Your notes also classify SQL commands into DDL, DQL, DML, DCL, and TCL.

Don't confuse **CRUD** with those categories.

For example:



```
CRUD
│
├── Create → INSERT
├── Read   → SELECT
├── Update → UPDATE
└── Delete → DELETE
```

while SQL command categories are a different classification:



```
SQL
│
├── DDL
├── DQL
├── DML
├── DCL
└── TCL
```

We'll study those separately.

---

# 15. One subtle thing in your notes

There's a beginner-friendly simplification in the notes that I want you to recognize.

The notes say SQL is used for CRUD and describe **CREATE** as including creating databases/tables and inserting tuples.

For interview purposes, keep this distinction:



```
CREATE DATABASE
CREATE TABLE
```

are **DDL operations**.

Whereas:



```
INSERT INTO ...
```

is the operation that creates/adds a **record** in CRUD terminology.

So:



```
Create database/table
        ↓
       DDL

Create a record
        ↓
      INSERT
        ↓
       DML
```

This distinction will save you from confusion later.

---

# 16. Where does MySQL fit?

Now let's put everything together.

Imagine you're building a food-delivery application.

You might have:



```
Database
    │
    ├── users
    ├── restaurants
    ├── orders
    ├── menu_items
    └── payments
```

The data lives in the database.

**MySQL** manages the database.

You communicate with MySQL using **SQL**.

For example:



```
SELECT *
FROM orders
WHERE user_id = 101;
```

The flow is:



```
Your SQL query
      ↓
     MySQL
      ↓
Database
      ↓
orders table
      ↓
matching rows
      ↓
result
```

This mental model is foundational.

---

# 17. Now connect this to LeetCode

Here's the beautiful part.

When LeetCode gives you:

### `Customer`

| id | name | referee\_id |
| -- | ---- | ---------- |
| 1                 | Will | NULL |
| 2                 | Jane | NULL |
| 3                 | Alex | 2    |

and asks:

> Find customers who were not referred by customer 2.

You're not solving an abstract coding problem.

You're interacting with a **relational table**.

You need to think:



```
DATABASE
   ↓
TABLE
   ↓
ROWS
   ↓
FILTER
   ↓
RESULT
```

which eventually becomes:



```
SELECT name
FROM Customer
WHERE referee_id != 2
   OR referee_id IS NULL;
```

That's **LeetCode #584 — Find Customer Referee**.

And notice how Database Basics already matters.

Before we can intelligently write that query, we need to understand:

-  What is a database?
-  What is a table?
-  What is a row?
-  What is a column?
-  What is SQL?
-  What is MySQL?
-  What does retrieving data mean?

That's why we're building the foundation first.

---

# 18. The interview mental model

If an interviewer says:

> **"What happens when you query a MySQL database?"**

Don't immediately start talking about SQL syntax.

Start conceptually:



```
Application
     ↓
SQL query
     ↓
MySQL / RDBMS
     ↓
Database
     ↓
Tables
     ↓
Data
     ↓
Result
```

Later, we'll go much deeper:



```
SQL query
   ↓
Parsing
   ↓
Optimization
   ↓
Execution plan
   ↓
Indexes / storage
   ↓
Rows
   ↓
Result
```

That is where **database fundamentals eventually connect to SQL performance and system design**.

---

# 19. The 7 definitions you should know cold

If you're preparing for an interview, I want you to be able to answer these instantly:

### 1. Database

> A collection of related/organized data.

### 2. DBMS

> Software used to create, manage, organize, and access databases.

### 3. RDBMS

> A DBMS that organizes data using related tables consisting of rows and columns.

### 4. SQL

> Structured Query Language used to interact with relational databases.

### 5. MySQL

> A relational database management system that uses SQL.

### 6. Table

> A structured collection of data organized into rows and columns.

### 7. CRUD

> Create, Read, Update, Delete — the four basic operations performed on stored data.

Your uploaded notes support these foundational definitions.

---

# 20. One diagram to memorize

If you remember only **one diagram from today's lesson**, remember this:



```
                         SQL
                          │
                          │ queries
                          ▼
                ┌─────────────────┐
                │      MySQL      │
                │      RDBMS      │
                └────────┬────────┘
                         │
                         │ manages
                         ▼
                   ┌───────────┐
                   │ DATABASE  │
                   └─────┬─────┘
                         │
             ┌───────────┼───────────┐
             ▼           ▼           ▼
         Customers     Orders      Products
           TABLE        TABLE        TABLE
             │           │            │
             └─────── relationships ──┘
                         │
                     rows/columns
```

And then:



```
SQL
│
├── SELECT  → Read
├── INSERT  → Create data
├── UPDATE  → Update data
└── DELETE  → Delete data
```

---

# 🎯 Interview checkpoint

Before we move to the next concept, **don't look up the answers**.

Imagine I'm interviewing you.

Answer these in your own words:

### Q1.

**What is the difference between a database and a DBMS?**

### Q2.

**What is the difference between DBMS and RDBMS?**

### Q3.

**What is SQL? Is SQL a database?**

### Q4.

**What is the difference between SQL and MySQL?**

### Q5.

Suppose I have:



```
college
 ├── students
 ├── courses
 └── teachers
```

What is `college`? What are `students`, `courses`, and `teachers`?

### Q6. ⭐ Interview-level

Why do we need a DBMS at all? Why can't an application simply store everything in files?

---
Answers - 

## Q1. What is the difference between a Database and a DBMS?

### Answer

A **database** is a collection of interrelated/organized data.

A **DBMS (Database Management System)** is the software used to create, manage, organize, and access that database. 

### Example

Imagine:

```text
Database
│
├── Students
├── Teachers
└── Courses
```

The **data** inside those tables is the database.

Something like **MySQL** is the software that manages that database.

### Interview answer 🎯

> "A database is the organized collection of data, whereas a DBMS is the software that allows us to create, manage, organize, and access that data."

---

# Q2. What is the difference between DBMS and RDBMS?

### DBMS

A **DBMS** is software that manages databases.

### RDBMS

An **RDBMS** is a type of DBMS based on the relational model, where data is organized into **tables (relations)** containing **rows and columns**. 

Think:

```text
DBMS
 │
 └── RDBMS
       │
       ├── Tables
       ├── Rows
       ├── Columns
       └── Relationships
```

Examples of RDBMS mentioned in your notes:

```text
MySQL
PostgreSQL
Oracle
```

### Interview answer 🎯

> "RDBMS is a type of DBMS that follows the relational model. It stores data in tables consisting of rows and columns, with relationships between tables."

---

# Q3. What is SQL? Is SQL a database?

### SQL

SQL stands for:

> **Structured Query Language**

It's a **language used to store, manipulate, and retrieve data from an RDBMS**. 

And importantly:

> **SQL is NOT a database.**

It's the language we use to communicate with the database system.

For example:

```sql
SELECT *
FROM students;
```

Here:

```text
SQL query
   ↓
MySQL
   ↓
Database
   ↓
students table
   ↓
result
```

Your notes explicitly state that SQL is not a database; it is a language used to interact with databases. 

### Interview answer 🎯

> "SQL stands for Structured Query Language. It is a language used to interact with relational databases, including retrieving and manipulating data. SQL itself is not a database."

---

# Q4. What is the difference between SQL and MySQL?

This one is **very important**.

### SQL

```text
SQL
↓
Language
```

### MySQL

```text
MySQL
↓
RDBMS
↓
Software
```

Your notes explicitly summarize it as:

> SQL is a language used to perform CRUD operations in a relational database, while MySQL is an RDBMS that uses SQL. 

### Example

You write:

```sql
SELECT name
FROM students;
```

That's **SQL**.

MySQL is the system that receives and executes that SQL query against your database.

### Interview answer 🎯

> "SQL is a language used to interact with relational databases, whereas MySQL is a relational database management system that implements and uses SQL."

### Very common mistake ❌

Don't say:

> "SQL is a database and MySQL is another database."

No.

Think:

```text
SQL       → Language
MySQL     → RDBMS
Database  → Data
```

---

# Q5. Suppose I have:

```text
college
 ├── students
 ├── courses
 └── teachers
```

What is `college`? What are `students`, `courses`, and `teachers`?

`college` is the **database**.

Inside it, `students`, `courses`, and `teachers` are **tables**.

For example:

```text
college DATABASE
│
├── students TABLE
│     ├── id
│     ├── name
│     └── age
│
├── courses TABLE
│     ├── course_id
│     └── course_name
│
└── teachers TABLE
      ├── teacher_id
      └── teacher_name
```

Your notes describe the relational model exactly this way: data is organized into tables, with rows representing records and columns representing attributes. 

### Interview answer 🎯

> "`college` is the database, while `students`, `courses`, and `teachers` are tables within that database."

---

# Q6. ⭐ Why do we need a DBMS? Why can't an application simply store everything in files?

This is the most interesting question.

Your notes establish that a DBMS is software used to **create, manage, and organize databases**. 

The key idea is that as data and application complexity grow, we need a system specifically designed to manage that data.

Imagine an application storing everything in:

```text
students.txt
orders.txt
payments.txt
employees.txt
```

Now suppose:

-  millions of records exist 
-  multiple users access the data simultaneously 
-  different applications need the same data 
-  data has relationships 
-  users need different permissions 
-  data must remain consistent 
-  you need efficient querying 

A DBMS gives us a structured system for managing these operations.

For example, instead of manually searching a huge file, we can ask:

```sql
SELECT *
FROM students
WHERE city = 'Delhi';
```

And the DBMS handles the query.

### Interview answer 🎯

> "A DBMS provides a structured way to store, organize, retrieve, and manipulate data. It becomes especially important when data is large, shared by multiple users or applications, and needs to be managed consistently rather than being handled as independent files."

---

# 🧠 The hierarchy you MUST understand

If an interviewer gives you:

```text
MySQL
College Database
Students Table
Rahul's Record
```

you should immediately understand:

```text
MySQL
  │
  │ is an
  ▼
RDBMS
  │
  │ manages
  ▼
College Database
  │
  │ contains
  ▼
Students Table
  │
  │ contains
  ▼
Rows / Records
```

And:

```text
SQL
 │
 │ communicates with
 ▼
MySQL
 │
 │ manages
 ▼
Database
```

This is the foundation for everything we're about to learn.

---

# 🔥 One final interview question

Suppose I ask you:

> **"You say MySQL is an RDBMS. Why is it called relational?"**

A strong answer would be:

> "Because data is organized into relations, represented as tables of rows and columns, and different tables can be related through common keys or columns."

For example:

```text
CUSTOMER
+-------------+-------+
| customer_id | name  |
+-------------+-------+
| 1           | Rahul |
| 2           | Priya |
+-------------+-------+

ORDERS
+----------+-------------+--------+
| order_id | customer_id | amount |
+----------+-------------+--------+
| 101      | 1           | 500    |
| 102      | 2           | 700    |
+----------+-------------+--------+
```

The relationship:

```text
CUSTOMER.customer_id
        │
        │
        ▼
ORDERS.customer_id
```

is what will eventually lead us to one of the **most important SQL interview topics: JOINs**.

And your notes later define joins as operations that combine rows from multiple tables using related columns. 

---

## 🧩 Your Database Basics cheat sheet

| TermMeaning  |                                                     |
| ------------ | --------------------------------------------------- |
| **Data**     | Individual pieces of information                    |
| **Database** | Collection of interrelated/organized data           |
| **DBMS**     | Software that manages databases                     |
| **RDBMS**    | DBMS based on the relational/table model            |
| **Table**    | Data organized into rows and columns                |
| **Row**      | A record                                            |
| **Column**   | An attribute                                        |
| **SQL**      | Language used to interact with relational databases |
| **MySQL**    | An RDBMS that uses SQL                              |
| **CRUD**     | Create, Read, Update, Delete                        |

Source basis: your uploaded Apna College SQL notes. 

### The one sentence I want permanently in your head:

> **SQL is the language, MySQL is the RDBMS, the database contains the data, and tables organize that data into rows and columns.**

Once this is solid, we can move to the next concept without any confusion.

---
Part 2 

# Database Basics — Part 2

We'll build this in this order:

```
```

```
1. Table
2. Row vs Column
3. Schema
4. Keys
5. Relationships
6. Cardinality
7. Why we split tables
8. Normalization
9. 1NF → 2NF → 3NF
10. How all of this connects to JOINs + LeetCode
```

---

# 1. Start with a real-world problem

Imagine you're building a college system.

You might initially think:

> "I'll create one table containing everything."

Something like:

| student\_idstudent\_namecitycourseteacherteacher\_phone |       |        |      |      |      |
| ------------------------------------------------------- | ----- | ------ | ---- | ---- | ---- |
| 1                                                       | Rahul | Delhi  | SQL  | Amit | 9999 |
| 2                                                       | Priya | Mumbai | SQL  | Amit | 9999 |
| 3                                                       | Aman  | Delhi  | Java | Neha | 8888 |
| 4                                                       | Riya  | Pune   | SQL  | Amit | 9999 |

At first glance, this looks fine.

But there's a problem.

Look at:

```
```

```
Amit | 9999
```

It's repeated.

Three students are taking SQL, so we're storing Amit's information three times.

And suppose Amit changes his phone number.

We now need to update:

```
```

```
row 1
row 2
row 4
```

What happens if we update only two?

Our database becomes inconsistent.

This is where **database design** begins.

---

# 2. Tables represent entities

Instead of one giant table, we can identify different **entities**.

For our college:

```
```

```
Student
Course
Teacher
```

Then create separate tables:

### Student

| student\_idstudent\_namecity |       |        |
| ---------------------------- | ----- | ------ |
| 1                            | Rahul | Delhi  |
| 2                            | Priya | Mumbai |
| 3                            | Aman  | Delhi  |
| 4                            | Riya  | Pune   |

### Course

| course\_idcourse\_nameteacher\_id |      |     |
| --------------------------------- | ---- | --- |
| 101                               | SQL  | 501 |
| 102                               | Java | 502 |

### Teacher

| teacher\_idteacher\_namephone |      |      |
| ----------------------------- | ---- | ---- |
| 501                           | Amit | 9999 |
| 502                           | Neha | 8888 |

Now we've separated different concepts.

This is the beginning of **relational database design**.

---

# 3. Row vs Column

Your notes call:

-  rows → **records** 
-  columns → **attributes**  

This distinction is extremely important.

Consider:

| student\_idnamecity |       |        |
| ------------------- | ----- | ------ |
| 1                   | Rahul | Delhi  |
| 2                   | Priya | Mumbai |

### Row

This:

```
```

```
1 | Rahul | Delhi
```

is one **record/row**.

It represents one student.

### Column

This:

```
```

```
student_id
```

is a **column/attribute**.

It describes one property of every student.

So:

```
```

```
                    TABLE
                      │
            ┌─────────┴─────────┐
            │                   │
         Columns              Rows
       (attributes)          (records)
            │                   │
       student_id            Student 1
       name                  Student 2
       city                  Student 3
```

### Interview question

**What is a row?**

> A row represents one record/instance in a table.

**What is a column?**

> A column represents an attribute/property of the records stored in the table.

---

# 4. What is a schema?

This is an important word that beginners often confuse with database.

A **schema** describes the structure of a database: its tables, columns, relationships, constraints, and other database objects.

Think:

```
```

```
Database
│
├── Structure
│   ├── tables
│   ├── columns
│   ├── relationships
│   └── constraints
│
└── Actual data
```

The structure is the **schema**.

For example:

```
```

```
students
-----------------------
student_id INT
name       VARCHAR(50)
city       VARCHAR(50)
```

That's part of the schema.

The actual:

```
```

```
1 | Rahul | Delhi
2 | Priya | Mumbai
```

is the data.

### Easy mental model

```
```

```
SCHEMA = blueprint
DATA   = actual contents
```

Think about a house.

```
```

```
Blueprint → Schema
Actual house → Data
```

---

# 5. Now the most important concept: Keys

Your notes specifically cover:

> **Primary Key**
>
> **Foreign Key**

A primary key uniquely identifies each row, while a foreign key references the primary key of another table. 

Let's understand them deeply.

---

# 6. Primary Key

Suppose:

### Students

| student\_idnamecity |       |        |
| ------------------- | ----- | ------ |
| 101                 | Rahul | Delhi  |
| 102                 | Priya | Mumbai |
| 103                 | Aman  | Pune   |

We need a way to uniquely identify each student.

That's:

```
```

```
student_id
```

So:

```
```

```
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);
```

A primary key provides the unique identity of a row.

Your notes emphasize that the primary key uniquely identifies each row and cannot be `NULL`. 

---

# 7. Why do we need a primary key?

Imagine:

| namecity |        |
| -------- | ------ |
| Rahul    | Delhi  |
| Rahul    | Delhi  |
| Rahul    | Mumbai |

If I say:

> "Update Rahul."

Which Rahul?

We don't know.

But if we have:

| student\_idnamecity |       |        |
| ------------------- | ----- | ------ |
| 101                 | Rahul | Delhi  |
| 102                 | Rahul | Delhi  |
| 103                 | Rahul | Mumbai |

Now:

```
```

```
WHERE student_id = 102
```

uniquely identifies one row.

That's the fundamental purpose of a primary key.

---

# 8. Primary Key ≠ necessarily one physical column

This is an important interview-level correction.

Your notes describe a primary key as a column **or set of columns** that uniquely identifies a row. 

So we can have:

```
```

```
student_id
```

as a primary key.

But sometimes we need multiple columns.

For example:

### Enrollment

| student\_idcourse\_idgrade |     |   |
| -------------------------- | --- | - |
| 101                        | 501 | A |
| 101                        | 502 | B |
| 102                        | 501 | A |

Here:

```
```

```
student_id alone ❌
course_id alone ❌
```

But:

```
```

```
(student_id, course_id) ✅
```

uniquely identifies an enrollment.

That's called a **composite primary key**.

---

# 9. Foreign Key

Now we reach the concept that makes tables **relational**.

Suppose:

### Customers

| customer\_idname |       |
| ---------------- | ----- |
| 1                | Rahul |
| 2                | Priya |
| 3                | Aman  |

### Orders

| order\_idcustomer\_idamount |   |     |
| --------------------------- | - | --- |
| 101                         | 1 | 500 |
| 102                         | 1 | 700 |
| 103                         | 2 | 300 |

Here:

```
```

```
Customers
customer_id
    │
    │ referenced by
    ▼
Orders
customer_id
```

`Orders.customer_id` is a **foreign key** referencing `Customers.customer_id`.

Your notes describe exactly this relationship. 

---

# 10. Primary Key vs Foreign Key

Memorize this table:

| Primary KeyForeign Key                |                                             |
| ------------------------------------- | ------------------------------------------- |
| Identifies a row                      | References another table's key              |
| Must be unique                        | Can contain duplicates                      |
| Cannot be NULL                        | Can be NULL, depending on design            |
| Identifies the row in its own table   | Establishes relationship with another table |
| Typically one PK constraint per table | A table can have multiple FKs               |

Your notes explicitly state that foreign keys can have duplicate and `NULL` values and that a table can have multiple foreign keys. 

### Mental picture

```
```

```
CUSTOMERS
┌─────────────┐
│ PK          │
│ customer_id │
└──────┬──────┘
       │
       │ relationship
       │
       ▼
ORDERS
┌─────────────┐
│ FK          │
│ customer_id │
└─────────────┘
```

---

# 11. Why can a foreign key have duplicates?

This is an **excellent interview question**.

Look at:

### Customers

```
```

```
customer_id
1
2
```

### Orders

```
```

```
order_id | customer_id
101      | 1
102      | 1
103      | 1
104      | 2
```

Customer `1` placed **three orders**.

Therefore:

```
```

```
Orders.customer_id
1
1
1
2
```

must be allowed to repeat.

So:

> **Primary key identifies one row. Foreign key identifies which parent row another row is related to.**

That's why FK values can repeat.

---

# 12. Relationships

Now we can describe relationships between tables.

There are three major cardinalities you should understand.

---

## One-to-One

One person has one passport.

```
```

```
Person
  1
  │
  │
  1
Passport
```

Example:

```
```

```
person_id → passport
```

---

## One-to-Many ⭐

One customer can have many orders.

```
```

```
Customer
    1
    │
    ├──────── Order
    ├──────── Order
    └──────── Order
```

This is extremely common.

Database representation:

```
```

```
customers
customer_id PK
```

and:

```
```

```
orders
order_id PK
customer_id FK
```

Notice something important:

**The foreign key normally lives on the "many" side.**

```
```

```
Customer 1 ────────< Orders
                      ↑
                     FK
```

This pattern will appear constantly in interviews.

---

# 13. Many-to-Many

Now imagine students and courses.

One student can take many courses.

One course can have many students.

```
```

```
Student
   ∞
   │
   │
   ∞
Course
```

We don't normally directly put a single FK in either table.

Instead, we introduce a **junction/association table**:

### Student

```
```

```
student_id
```

### Course

```
```

```
course_id
```

### Enrollment

```
```

```
student_id
course_id
```

So:

```
```

```
Students
    │
    │ 1
    ▼
Enrollment
    ▲
    │ 1
    │
Courses
```

Or conceptually:

```
```

```
Students
   ∞
   │
   ▼
Enrollment
   ▲
   │
   ∞
Courses
```

This is an extremely important database design pattern.

And it eventually leads directly to SQL JOIN problems.

---

# 14. Why don't we just put everything into one table?

This brings us to **normalization**.

Suppose we store:

| student\_idstudent\_namecourseteacherteacher\_phone |       |      |      |      |
| --------------------------------------------------- | ----- | ---- | ---- | ---- |
| 1                                                   | Rahul | SQL  | Amit | 9999 |
| 2                                                   | Priya | SQL  | Amit | 9999 |
| 3                                                   | Aman  | SQL  | Amit | 9999 |
| 4                                                   | Riya  | Java | Neha | 8888 |

We've introduced **redundancy**.

Amit's phone number appears three times.

That's dangerous.

---

# 15. The three classic anomalies

Normalization exists largely to reduce problematic redundancy and update anomalies.

These are important interview concepts.

## 1. Update anomaly

Amit changes his phone:

```
```

```
9999 → 7777
```

We need to update multiple rows.

If we forget one:

```
```

```
Amit | 9999
Amit | 7777
Amit | 7777
```

Our database is inconsistent.

---

## 2. Insert anomaly

Suppose a new teacher joins:

```
```

```
Teacher: Raj
Phone: 6666
```

But Raj hasn't been assigned any student yet.

If our only table requires:

```
```

```
student_id
course
teacher
```

how do we insert Raj?

We can't naturally represent the teacher independently.

That's an **insert anomaly**.

---

## 3. Delete anomaly

Suppose Aman is the only student taking Java.

If we delete Aman:

```
```

```
Aman
Java
Neha
8888
```

we might accidentally lose information about the Java course or Neha.

That's a **delete anomaly**.

---

# 16. Normalization

Now the big definition.

> **Normalization is the process of organizing relational data into well-structured tables to reduce unnecessary redundancy and prevent update, insert, and delete anomalies.**

This is **additional database knowledge**, not a definition present in the retrieved sections of your uploaded notes.

The core academic literature traces relational normalization to the relational model and functional-dependency-based normal forms; the scholarly search results also describe 2NF in terms of non-key attributes being fully functionally dependent on the entire key. 

For your interviews, focus first on:

```
```

```
1NF
2NF
3NF
```

---

# 17. 1NF — First Normal Form

The basic idea:

> **Each cell should contain a single/atomic value, rather than a list of values.**

Bad:

| student\_idnamecourses |       |                   |
| ---------------------- | ----- | ----------------- |
| 1                      | Rahul | SQL, Java, Python |

`courses` contains multiple values.

Better:

| student\_idcourse |        |
| ----------------- | ------ |
| 1                 | SQL    |
| 1                 | Java   |
| 1                 | Python |

Now each cell contains one value.

### Mental rule

```
```

```
❌ "SQL, Java, Python"

✅
SQL
Java
Python
```

That's the intuition behind 1NF.

---

# 18. 2NF

This is where things become more interesting.

2NF matters particularly when you have a **composite key**.

Suppose:

### Enrollment

| student\_idcourse\_idstudent\_namecourse\_name |     |       |      |
| ---------------------------------------------- | --- | ----- | ---- |
| 1                                              | 101 | Rahul | SQL  |
| 1                                              | 102 | Rahul | Java |
| 2                                              | 101 | Priya | SQL  |

Primary key:

```
```

```
(student_id, course_id)
```

But:

```
```

```
student_id → student_name
```

Student name depends only on part of the composite key.

And:

```
```

```
course_id → course_name
```

Course name depends only on another part.

So we have **partial dependency**.

That's what 2NF tries to eliminate.

Split it:

### Students

| student\_idstudent\_name |       |
| ------------------------ | ----- |
| 1                        | Rahul |
| 2                        | Priya |

### Courses

| course\_idcourse\_name |      |
| ---------------------- | ---- |
| 101                    | SQL  |
| 102                    | Java |

### Enrollment

| student\_idcourse\_id |     |
| --------------------- | --- |
| 1                     | 101 |
| 1                     | 102 |
| 2                     | 101 |

Now the attributes belong where they actually depend.

---

# 19. 3NF

Now imagine:

### Employees

| employee\_idemployee\_namedepartment\_iddepartment\_name |       |    |             |
| -------------------------------------------------------- | ----- | -- | ----------- |
| 1                                                        | Rahul | 10 | Engineering |
| 2                                                        | Priya | 10 | Engineering |
| 3                                                        | Aman  | 20 | HR          |

We have:

```
```

```
employee_id → department_id
department_id → department_name
```

Therefore:

```
```

```
employee_id → department_name
```

indirectly.

`department_name` really belongs to the **department**, not directly to the employee.

So split:

### Employees

| employee\_idemployee\_namedepartment\_id |       |    |
| ---------------------------------------- | ----- | -- |
| 1                                        | Rahul | 10 |
| 2                                        | Priya | 10 |
| 3                                        | Aman  | 20 |

### Departments

| department\_iddepartment\_name |             |
| ------------------------------ | ----------- |
| 10                             | Engineering |
| 20                             | HR          |

Now the relationship is cleaner.

This is the intuition behind **3NF**:

> Non-key attributes should depend on the key, the whole key, and nothing but the key.

That's a common interview mnemonic.

---

# 20. Don't memorize normalization yet

This is important.

Don't try to memorize:

```
```

```
1NF = ...
2NF = ...
3NF = ...
```

Instead remember the problem:

```
```

```
BAD DESIGN
     ↓
Repeated information
     ↓
Update anomaly
Insert anomaly
Delete anomaly
     ↓
NORMALIZATION
     ↓
Separate entities into appropriate tables
     ↓
Connect tables using keys
```

That's the actual reason normalization exists.

---

# 21. But wait — why not normalize EVERYTHING?

Excellent interview follow-up.

Because normalization isn't automatically "more tables = better."

More tables can mean more joins.

For example:

```
```

```
Orders
   ↓
Customers
   ↓
Addresses
   ↓
Countries
   ↓
Regions
```

Now a simple query may require many joins.

Sometimes production systems deliberately **denormalize** data for performance or reporting.

So the practical tradeoff is:

```
```

```
Normalization
    ↓
Less redundancy
Better consistency
More tables
Potentially more joins

Denormalization
    ↓
More redundancy
Fewer joins
Potentially faster reads
More difficult updates
```

This is a more advanced database-design topic; we don't need to master it yet.

---

# 22. The most important connection: Keys + Relationships + JOIN

Now look at this:

### Customers

| customer\_idname |       |
| ---------------- | ----- |
| 1                | Rahul |
| 2                | Priya |

### Orders

| order\_idcustomer\_idamount |   |     |
| --------------------------- | - | --- |
| 101                         | 1 | 500 |
| 102                         | 1 | 700 |
| 103                         | 2 | 300 |

Question:

> Find each customer's name and their order amount.

The information is split across tables.

We need to connect:

```
```

```
Customers.customer_id
          =
Orders.customer_id
```

That's a **JOIN**.

Eventually:

```
```

```
SELECT c.name, o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Don't worry about mastering JOIN syntax yet.

The important thing is:

> **JOIN is the SQL mechanism that lets us use the relationships we've designed between tables.**

Your uploaded notes later define joins in essentially these terms: combining rows from multiple tables using related/common columns or keys. 

---

# 23. This is why database design matters for LeetCode

Look at **LeetCode #1378 — Replace Employee ID With The Unique Identifier**.

Conceptually, you have:

```
```

```
Employees
employee_id
name

EmployeeUNI
id
unique_id
```

The problem isn't really about complicated SQL.

It's testing whether you recognize:

```
```

```
Employees.id
     │
     │ relationship
     ▼
EmployeeUNI.id
```

and retrieve information across the relationship.

Likewise:

### #1068 — Product Sales Analysis I

You have product information and sales information.

### #1581 — Customer Who Visited but Did Not Make Any Transactions

You have visits and transactions.

### #577 — Employee Bonus

You have employees and bonus information.

### #1280 — Students and Examinations

You have multiple related entities.

The underlying pattern is repeatedly:

```
```

```
Understand entities
       ↓
Understand keys
       ↓
Understand relationships
       ↓
JOIN tables
       ↓
Filter / aggregate
```

That's why we're spending time here **before SELECT**.

---

# 24. One subtle but VERY important distinction

Suppose:

```
```

```
Customers
customer_id PK
```

and:

```
```

```
Orders
customer_id FK
```

A foreign key **does not necessarily mean**:

> "This column must be unique."

No.

It means:

> "This value references a valid key in the parent table, subject to the FK constraint."

Therefore:

```
```

```
Orders.customer_id

1
1
1
2
2
3
```

is perfectly reasonable.

This represents:

```
```

```
Customer 1 → 3 orders
Customer 2 → 2 orders
Customer 3 → 1 order
```

This is the database representation of a **one-to-many relationship**.

---

# 25. Another subtle interview point: PK vs UNIQUE

You may encounter:

```
```

```
email VARCHAR(255) UNIQUE
```

and:

```
```

```
id INT PRIMARY KEY
```

Both enforce uniqueness, but they have different roles.

### Primary key

> The designated identifier for rows in the table.

### UNIQUE constraint

> Prevents duplicate values in the constrained column(s).

A table can have multiple `UNIQUE` constraints, but it has one primary-key constraint.

Your notes also distinguish `UNIQUE` from `PRIMARY KEY`, describing `UNIQUE` as requiring distinct values and the primary key as uniquely identifying rows and being non-null. 

---

# 26. Schema vs database — don't get trapped

Depending on the database system, terminology around **database** and **schema** differs.

For our MySQL learning, be careful not to blindly apply terminology from PostgreSQL or textbook definitions.

For now, use this mental model:

```
```

```
Database design/schema
        ↓
tables
        ↓
columns + types + constraints
        ↓
relationships
        ↓
actual rows
```

We'll revisit MySQL's exact treatment of databases/schemas when we study MySQL-specific database commands.

---

# 27. Our complete mental model

This is the big picture I want you to internalize:

```
```

```
                         DATABASE
                             │
                    ┌────────┴────────┐
                    │                 │
                 Schema            Data
                    │                 │
             ┌──────┼──────┐         │
             ▼      ▼      ▼         ▼
          Students Courses Teachers  Rows
             │      │      │
             │      │      │
             └──────┼──────┘
                    │
             relationships
                    │
              PK ↔ FK
                    │
                    ▼
                  JOIN
                    │
                    ▼
              Query results
```

And underneath the design:

```
```

```
Normalization
      ↓
Reduce unnecessary redundancy
      ↓
Avoid anomalies
      ↓
Separate entities
      ↓
Use PK/FK relationships
      ↓
JOIN when you need combined information
```

---

# 🎯 Interview Cheat Sheet

If the interviewer asks:

### "What is a primary key?"

> A column or set of columns that uniquely identifies each row in a table.

### "What is a foreign key?"

> A column or set of columns that references a key in another table and establishes a relationship between the tables.

### "Can a foreign key contain duplicates?"

> Yes. For example, many orders can belong to the same customer.

### "Can a foreign key be NULL?"

> Yes, if the relationship is optional and the column isn't constrained as `NOT NULL`.

### "What is a composite key?"

> A key made from multiple columns that together uniquely identify a row.

### "What is normalization?"

> Organizing relational data into appropriate tables to reduce redundancy and prevent insertion, update, and deletion anomalies.

### "Why normalize?"

> To improve data consistency and reduce unnecessary duplication.

### "What is a one-to-many relationship?"

> One record in a parent table can be associated with multiple records in a child table, typically represented by a foreign key on the many side.

---

# 🧠 The connection I REALLY want you to remember

Don't think of a database as:

```
```

```
"Some tables containing data."
```

Think of it as:

```
```

```
REAL WORLD
    ↓
Entities
    ↓
Tables
    ↓
Rows + Columns
    ↓
Keys
    ↓
Relationships
    ↓
Normalized structure
    ↓
SQL queries
    ↓
JOIN / FILTER / GROUP / AGGREGATE
```

**That's how you should mentally approach SQL interview problems.**

And this is exactly why the SQL 50 will become much easier: when you see two or three tables, you'll stop thinking *"Which SQL syntax do I remember?"* and start thinking:

> **"What does each table represent? What is the key? How are these entities related? What is the grain of each table? What result do I need?"**

That's the beginning of genuine SQL skill.

---

part 3 

# 🔥 Constraints + Keys + NULL in MySQL

The big picture:

```
```

```
                    CONSTRAINTS
                         │
        ┌────────────────┼────────────────┐
        │                │                │
     NOT NULL          UNIQUE          PRIMARY KEY
        │                │                │
   value required    no duplicates    row identity
                         │
        ┌────────────────┼────────────────┐
        │                │                │
     FOREIGN KEY       DEFAULT          CHECK
        │                │                │
   table relationship  fallback value   validation rule
```

The purpose is simple:

> **Constraints protect the integrity of your data.**

Instead of trusting every application developer to insert valid data, the database itself enforces important rules.

---

# 1. What is a constraint?

Your notes define SQL constraints as rules for data in a table. 

Imagine:

```
```

```
CREATE TABLE students (
    id INT,
    name VARCHAR(100),
    age INT
);
```

Nothing here says:

- `id` must be unique 
- `name` cannot be missing 
- `age` must be positive 

We can add constraints:

```
```

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT CHECK (age >= 0)
);
```

Now MySQL enforces those rules.

Think:

```
```

```
Without constraints:

Application → Database
                ↓
             "Anything?"

With constraints:

Application → Database
                ↓
          "Does this obey
           my rules?"
                ↓
          YES → accept
          NO  → reject
```

---

# 2. `NOT NULL`

This is the easiest one.

```
```

```
name VARCHAR(100) NOT NULL
```

means:

> `name` cannot contain `NULL`.

Your notes summarize `NOT NULL` as preventing a column from having a null value. 

Example:

```
```

```
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

This is valid:

```
```

```
INSERT INTO employees
VALUES (1, 'Rahul');
```

This is rejected:

```
```

```
INSERT INTO employees
VALUES (2, NULL);
```

Because:

```
```

```
name → NOT NULL
```

---

# 3. What exactly is `NULL`?

This is **extremely important for SQL interviews**.

`NULL` does **not** mean:

```
```

```
0
```

It does **not** mean:

```
```

```
''
```

It does **not** mean:

```
```

```
false
```

It means approximately:

> **The value is unknown, missing, or not applicable.**

Consider:

| idnamephone |       |      |
| ----------- | ----- | ---- |
| 1           | Rahul | 9876 |
| 2           | Priya | NULL |

For Priya, `phone = NULL` does not necessarily mean:

> "Priya has no phone."

It means:

> "We don't currently have a phone value / the value is unknown."

---

# 4. `NULL` is NOT zero

This:

```
```

```
salary = 0
```

means:

> salary is known to be zero.

Whereas:

```
```

```
salary = NULL
```

means:

> salary is unknown/missing/not provided.

Very different.

---

# 5. `NULL` is NOT an empty string

These are also different:

```
```

```
NULL
''
```

`''` is a string containing zero characters.

`NULL` represents absence/unknownness.

So:

```
```

```
INSERT INTO users (name)
VALUES ('Rahul');
```

might result in:

```
```

```
phone = NULL
```

whereas:

```
```

```
INSERT INTO users (name, phone)
VALUES ('Rahul', '');
```

explicitly stores an empty string.

---

# 6. The biggest `NULL` trap

You might instinctively write:

```
```

```
WHERE phone = NULL
```

❌ Wrong.

You use:

```
```

```
WHERE phone IS NULL
```

And:

```
```

```
WHERE phone IS NOT NULL
```

Your notes explicitly introduce `IS NULL` for checking NULL values. 

### Why?

Because `NULL` represents an unknown value, and SQL uses **three-valued logic**:

```
```

```
TRUE
FALSE
UNKNOWN
```

This is one of the reasons SQL behaves differently from ordinary programming languages.

We'll deep-dive into this when we reach `WHERE`.

---

# 7. `UNIQUE`

Your notes describe `UNIQUE` as requiring values in a column to be different. 

Example:

```
```

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

Now:

```
```

```
id    email
1     rahul@gmail.com
2     priya@gmail.com
```

is fine.

But:

```
```

```
3     rahul@gmail.com
```

violates the `UNIQUE` constraint.

---

# 8. `UNIQUE` vs `PRIMARY KEY`

This is a **very common interview question**.

| PRIMARY KEYUNIQUE                    |                                      |
| ------------------------------------ | ------------------------------------ |
| Identifies rows                      | Prevents duplicate values            |
| Cannot be `NULL`                     | Can allow `NULL`                     |
| One primary-key constraint per table | Multiple UNIQUE constraints possible |
| Main row identity                    | Candidate/alternate uniqueness rule  |

For example:

```
```

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    username VARCHAR(50) UNIQUE
);
```

Here:

```
```

```
id        → PRIMARY KEY
email     → UNIQUE
username  → UNIQUE
```

We have one primary key but multiple unique constraints.

### Important MySQL detail

In MySQL, a `UNIQUE` index generally permits multiple `NULL` values because `NULL` is not considered equal to another `NULL` for uniqueness purposes.

So:

```
```

```
email
----------------
a@gmail.com
b@gmail.com
NULL
NULL
```

can be valid with a normal MySQL `UNIQUE` constraint.

If you want an email to both exist and be unique:

```
```

```
email VARCHAR(255) NOT NULL UNIQUE
```

That's a very useful real-world pattern.

---

# 9. `PRIMARY KEY`

Your notes define a primary key as a column or set of columns that uniquely identifies each row. 

Example:

```
```

```
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Now:

```
```

```
employee_id
-----------
1
2
3
```

uniquely identifies each employee.

### Think of it as:

```
```

```
PRIMARY KEY
     ↓
"Who exactly is this row?"
```

---

# 10. Can a primary key have multiple columns?

YES.

This is called a **composite primary key**.

Example:

```
```

```
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

Now:

```
```

```
student_id | course_id
-----------+----------
1          | 101
1          | 102
2          | 101
```

But:

```
```

```
1 | 101
1 | 101
```

❌ duplicate primary-key combination.

The combination must be unique.

---

# 11. Primary Key vs Unique — deeper understanding

Imagine:

```
```

```
users
--------------------------------
id | email | username
```

You could have:

```
```

```
id INT PRIMARY KEY
email VARCHAR(255) UNIQUE
username VARCHAR(50) UNIQUE
```

Why?

Because:

```
```

```
id
↓
identity of row
```

while:

```
```

```
email
↓
must not be duplicated
```

and:

```
```

```
username
↓
must not be duplicated
```

The distinction is about **role**, not just uniqueness.

---

# 12. `DEFAULT`

Your notes say:

> `DEFAULT` sets the default value of a column. 

Example:

```
```

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    status VARCHAR(20) DEFAULT 'active'
);
```

Now:

```
```

```
INSERT INTO users (id, name)
VALUES (1, 'Rahul');
```

Since we didn't provide `status`:

```
```

```
status = 'active'
```

is automatically used.

---

# 13. `DEFAULT` does NOT mean `NULL`

This distinction matters.

```
```

```
status VARCHAR(20) DEFAULT 'active'
```

means:

> If no value is supplied, use `'active'`.

It doesn't mean:

> Every explicitly supplied `NULL` becomes `'active'`.

For example, depending on column nullability:

```
```

```
INSERT INTO users (id, name, status)
VALUES (1, 'Rahul', NULL);
```

can explicitly store `NULL`.

So:

```
```

```
DEFAULT
   ↓
What happens when value is omitted?
```

Whereas:

```
```

```
NOT NULL
   ↓
Is NULL allowed?
```

Different concepts.

---

# 14. Combining constraints

This is where things become powerful.

```
```

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    status VARCHAR(20) NOT NULL DEFAULT 'active',
    age INT CHECK (age >= 18)
);
```

Now:

```
```

```
id
↓
PRIMARY KEY
↓
unique + non-null
```

```
```

```
username
↓
NOT NULL + UNIQUE
```

```
```

```
status
↓
NOT NULL + DEFAULT
```

```
```

```
age
↓
CHECK age >= 18
```

We're effectively defining a **contract** for the table.

---

# 15. `CHECK`

Now we reach another useful constraint.

`CHECK` specifies a condition that values must satisfy.

Example:

```
```

```
age INT CHECK (age >= 18)
```

Then:

```
```

```
age = 25    ✅
age = 18    ✅
age = 17    ❌
```

Another example:

```
```

```
salary DECIMAL(10,2) CHECK (salary >= 0)
```

means negative salaries aren't accepted.

Your notes list `CHECK` among the constraints used to ensure data integrity. 

### MySQL-specific point

For modern MySQL, `CHECK` constraints are enforced in MySQL 8.0.16 and later. This is worth knowing for interviews because older tutorials sometimes say MySQL ignores `CHECK`.

---

# 16. Now the BIG one: FOREIGN KEY

Let's create two tables.

### Parent

```
```

```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

### Child

```
```

```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

Now:

```
```

```
customers
┌─────────────┐
│ customer_id │ ← PRIMARY KEY
└──────┬──────┘
       │
       │ referenced by
       ▼
orders
┌─────────────┐
│ customer_id │ ← FOREIGN KEY
└─────────────┘
```

This creates a relationship.

Your notes describe a foreign key as a column/set of columns referencing a primary key in another table. 

---

# 17. What does the foreign key actually protect?

Suppose:

```
```

```
customers

customer_id
-----------
1
2
3
```

Now:

```
```

```
INSERT INTO orders
VALUES (101, 999);
```

❌ The customer `999` doesn't exist.

The foreign key can prevent this because:

```
```

```
orders.customer_id = 999
```

must reference a valid parent key.

This protects **referential integrity**.

Think:

> **"Don't let a child point to a parent that doesn't exist."**

---

# 18. Why can Foreign Keys repeat?

Suppose customer 1 makes three orders:

```
```

```
order_id | customer_id
---------+------------
101      | 1
102      | 1
103      | 1
```

That's valid.

Because:

```
```

```
Customer 1
    │
    ├── Order 101
    ├── Order 102
    └── Order 103
```

Your notes explicitly state that foreign keys can have duplicates and `NULL`, and that a table can have multiple foreign keys. 

---

# 19. Can a Foreign Key be NULL?

Yes.

Suppose:

```
```

```
manager_id INT,
FOREIGN KEY (manager_id)
    REFERENCES employees(employee_id)
```

The CEO might have:

```
```

```
manager_id = NULL
```

because the CEO doesn't have a manager inside the organization.

That's perfectly legitimate if the column isn't `NOT NULL`.

So:

```
```

```
FK = 10
```

means:

> "This references parent 10."

Whereas:

```
```

```
FK = NULL
```

means:

> "There is currently no referenced value."

---

# 20. Foreign Key + NOT NULL

These two together are extremely useful.

```
```

```
customer_id INT NOT NULL,
FOREIGN KEY (customer_id)
    REFERENCES customers(customer_id)
```

Now every order **must** belong to a customer.

You cannot have:

```
```

```
customer_id = NULL
```

and you cannot have:

```
```

```
customer_id = 999
```

if customer 999 doesn't exist.

So we've enforced:

```
```

```
Every order
    ↓
must have a customer
    ↓
and that customer must exist
```

That's excellent database design.

---

# 21. Parent vs Child table

These terms are important.

```
```

```
customers
    ↓
parent table

orders
    ↓
child table
```

Why?

Because:

```
```

```
orders.customer_id
        ↓
references
        ↓
customers.customer_id
```

The table being referenced is the **parent**.

The table containing the foreign key is the **child**.

---

# 22. Now the interesting part: DELETE

Suppose:

### Customers

```
```

```
id
--
1
2
```

### Orders

```
```

```
order_id | customer_id
---------+------------
101      | 1
102      | 1
103      | 2
```

Now someone runs:

```
```

```
DELETE FROM customers
WHERE customer_id = 1;
```

What should happen to orders 101 and 102?

This is where foreign-key actions matter.

---

# 23. `ON DELETE CASCADE`

Your notes specifically cover this.

They explain that with `ON DELETE CASCADE`, deleting a referenced parent row causes the corresponding referencing rows in the child table to be deleted. 

Example:

```
```

```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    
    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
        ON DELETE CASCADE
);
```

Before:

```
```

```
customers

1 Rahul
2 Priya
```

```
```

```
orders

101 → customer 1
102 → customer 1
103 → customer 2
```

Delete:

```
```

```
DELETE FROM customers
WHERE customer_id = 1;
```

After:

```
```

```
customers

2 Priya
```

and:

```
```

```
orders

103 → customer 2
```

Orders 101 and 102 are automatically deleted.

### Mental model

```
```

```
DELETE parent
      ↓
CASCADE
      ↓
DELETE related children
```

---

# 24. `ON UPDATE CASCADE`

Your notes similarly state that `ON UPDATE CASCADE` updates the referencing rows in the child when the referenced parent key is updated. 

Example:

```
```

```
FOREIGN KEY (customer_id)
    REFERENCES customers(customer_id)
    ON UPDATE CASCADE
```

Suppose:

```
```

```
customers
customer_id
-----------
1
```

and:

```
```

```
orders
customer_id
-----------
1
1
1
```

If the parent key changes:

```
```

```
1 → 100
```

then with `ON UPDATE CASCADE`:

```
```

```
customers
customer_id
-----------
100
```

and:

```
```

```
orders
customer_id
-----------
100
100
100
```

The relationship stays intact.

---

# 25. But here's an important design insight

You might ask:

> "Why would we ever update a primary key?"

Usually, identifiers such as:

```
```

```
customer_id
employee_id
order_id
```

are designed to be stable.

So `ON UPDATE CASCADE` is less commonly needed in typical application designs than `ON DELETE CASCADE`.

But it exists for situations where referenced key values can change.

---

# 26. What if we DON'T use CASCADE?

Then the database can prevent deletion of a parent that still has dependent child rows.

For example:

```
```

```
Customer 1
   │
   ├── Order 101
   └── Order 102
```

If you attempt:

```
```

```
DELETE FROM customers
WHERE customer_id = 1;
```

the database can reject the operation because deleting the customer would leave orphaned orders.

This is the whole point of referential integrity.

---

# 27. Common foreign-key actions

For MySQL/InnoDB, the important actions to know are:

```
```

```
ON DELETE / ON UPDATE
│
├── RESTRICT
├── NO ACTION
├── CASCADE
└── SET NULL
```

### RESTRICT

Don't allow the operation if dependent rows exist.

### NO ACTION

For MySQL/InnoDB, effectively behaves like `RESTRICT` for this purpose.

### CASCADE

Propagate the change.

```
```

```
parent DELETE
     ↓
child DELETE
```

### SET NULL

Set the child FK to `NULL`.

Example:

```
```

```
FOREIGN KEY (manager_id)
    REFERENCES employees(employee_id)
    ON DELETE SET NULL
```

If manager 10 is deleted:

```
```

```
employee
manager_id
----------
10
```

can become:

```
```

```
employee
manager_id
----------
NULL
```

Of course, the child FK column must allow `NULL`.

---

# 28. CASCADE vs SET NULL

Imagine:

```
```

```
Department
    ↓
Employees
```

If department 10 is deleted:

### CASCADE

```
```

```
Delete department
       ↓
Delete employees
```

Potentially dangerous.

### SET NULL

```
```

```
Delete department
       ↓
employee.department_id = NULL
```

The employees remain.

Which one is correct depends on the business meaning.

This is **database design**, not just syntax.

---

# 29. A complete realistic example

Let's build a small system.

```
```

```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE
);
```

And:

```
```

```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    amount DECIMAL(10,2) CHECK (amount >= 0),
    status VARCHAR(20) NOT NULL DEFAULT 'pending',

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

Look at what we've accomplished.

### `customer_id`

```
```

```
PRIMARY KEY
```

→ uniquely identifies customer.

### `name`

```
```

```
NOT NULL
```

→ customer must have a name.

### `email`

```
```

```
NOT NULL + UNIQUE
```

→ email must exist and cannot be duplicated.

### `order_id`

```
```

```
PRIMARY KEY
```

→ uniquely identifies order.

### `customer_id` in orders

```
```

```
NOT NULL + FOREIGN KEY
```

→ every order must belong to an existing customer.

### `amount`

```
```

```
CHECK (amount >= 0)
```

→ no negative order amount.

### `status`

```
```

```
DEFAULT 'pending'
```

→ automatically starts as pending if omitted.

### Cascade

```
```

```
ON DELETE CASCADE
ON UPDATE CASCADE
```

→ relationship changes propagate according to the defined rules.

That's a **proper relational schema**.

---

# 30. One thing I want you to notice

Look at this:

```
```

```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    ...
    
    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

We now have a direct bridge from everything we've studied:

```
```

```
Database Basics
      ↓
Tables
      ↓
Rows + Columns
      ↓
Primary Key
      ↓
Foreign Key
      ↓
Relationships
      ↓
Constraints
      ↓
Data Integrity
      ↓
JOIN
```

And that last step is why we're doing all this **before SELECT**.

---

# 31. Constraint cheat sheet

Burn this into memory:

| ConstraintQuestion it answers |                                                     |
| ----------------------------- | --------------------------------------------------- |
| `NOT NULL`                    | **Must a value exist?**                             |
| `UNIQUE`                      | **Can values repeat?**                              |
| `PRIMARY KEY`                 | **How do I uniquely identify this row?**            |
| `FOREIGN KEY`                 | **Which row in another table does this relate to?** |
| `DEFAULT`                     | **What value should be used if none is supplied?**  |
| `CHECK`                       | **Does this value satisfy a rule?**                 |

That's a beautiful way to remember them.

---

# 32. The `NULL` cheat sheet

This is worth memorizing separately.

```
```

```
NULL
```

means:

> Unknown / missing / not applicable.

Not:

```
```

```
0
```

Not:

```
```

```
```

Not:

```
```

```
```

And:

```
```

```
WHERE column IS NULL
```

not:

```
```

```
WHERE column = NULL
```

And:

```
```

```
WHERE column IS NOT NULL
```

not:

```
```

```
WHERE column != NULL
```

This will become **very important in LeetCode**.

For example, **#584 Find Customer Referee** requires reasoning about `NULL`:

```
```

```
WHERE referee_id != 2
   OR referee_id IS NULL
```

If you don't understand SQL's `NULL` behavior, that problem can feel surprisingly confusing.

---

# 33. Interview traps 🚨

### Trap 1

**Can a foreign key contain duplicate values?**

✅ Yes.

---

### Trap 2

**Can a foreign key be NULL?**

✅ Yes, unless `NOT NULL` is also specified.

---

### Trap 3

**Can a primary key be NULL?**

❌ No.

---

### Trap 4

**Can a table have multiple primary keys?**

❌ It has one primary-key constraint.

But that primary key can contain **multiple columns**.

```
```

```
PRIMARY KEY (A, B)
```

---

### Trap 5

**Can a table have multiple UNIQUE constraints?**

✅ Yes.

---

### Trap 6

**Does** **`DEFAULT`** **mean the column cannot be NULL?**

❌ No.

`DEFAULT` and `NOT NULL` solve different problems.

---

### Trap 7

**Does** **`NULL = NULL`** **return TRUE?**

❌ No.

This is where SQL's three-valued logic enters.

---

### Trap 8

**What does** **`ON DELETE CASCADE`** **mean?**

> Deleting a referenced parent row automatically deletes matching child rows.

Your notes state this explicitly. 

---

# 34. Interview round — your first real database test

Imagine I'm interviewing you.

### Question 1

What's the difference between:

```
```

```
id INT PRIMARY KEY
```

and:

```
```

```
id INT UNIQUE
```

---

### Question 2

Can this table contain two rows with `email = NULL`?

```
```

```
CREATE TABLE users (
    email VARCHAR(255) UNIQUE
);
```

Think carefully.

---

### Question 3

What's the difference between:

```
```

```
WHERE manager_id = NULL
```

and:

```
```

```
WHERE manager_id IS NULL
```

---

### Question 4

Consider:

```
```

```
customers
-----------
id
1
2

orders
-----------
order_id | customer_id
101      | 1
102      | 1
103      | 2
```

Can `orders.customer_id` contain:

```
```

```
1
1
1
```

Why?

---

### Question 5

What happens here?

```
```

```
FOREIGN KEY (customer_id)
REFERENCES customers(id)
ON DELETE CASCADE
```

If customer `1` is deleted and customer `1` has five orders?

---

### Question 6 ⭐

Why would we use:

```
```

```
ON DELETE SET NULL
```

instead of:

```
```

```
ON DELETE CASCADE
```

---

### Question 7 ⭐⭐

Consider:

```
```

```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    amount DECIMAL(10,2) CHECK (amount >= 0),
    status VARCHAR(20) DEFAULT 'pending',

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

Tell me **what rule each constraint is enforcing**.

---

## 🧠 The entire concept in one picture

```
```

```
                         TABLE
                           │
             ┌─────────────┴─────────────┐
             │                           │
          COLUMNS                      ROWS
             │                           │
             ▼                           ▼
       ┌───────────────┐          ┌────────────┐
       │ id            │          │ Record 1   │
       │ name          │          │ Record 2   │
       │ email         │          │ Record 3   │
       │ customer_id   │          └────────────┘
       └───────────────┘
             │
             ▼
        CONSTRAINTS
             │
   ┌─────────┼──────────┬──────────┬──────────┐
   ▼         ▼          ▼          ▼          ▼
 NOT NULL  UNIQUE       PK         FK       CHECK
                                      │
                                      ▼
                               OTHER TABLE
                                      │
                                      ▼
                                  RELATIONSHIP
                                      │
                                      ▼
                                    JOIN
```

This is the foundation.

Your notes cover the core constraint definitions and cascade behavior, including the fact that primary keys uniquely identify rows, foreign keys reference another table's key, and foreign keys may contain duplicates/NULLs.

---

part 4 

# 🚀 SELECT Starts Now

This is a major milestone. From here, we're moving from **database design** to **actually interrogating the data**.

Your notes describe `SELECT` as the foundation of DQL for retrieving columns, and `WHERE` as the clause used to filter records. They also cover comparison operators and `AND`, `OR`, `NOT`.  

We'll learn this in an interview-oriented way:

```
```

```
SELECT
  ↓
FROM
  ↓
WHERE
  ↓
Comparison operators
  ↓
AND / OR / NOT
  ↓
NULL + 3-valued logic
  ↓
LeetCode
```

And I'm going to make one distinction throughout:

> **Your notes** = what your notes teach.
>
> **MySQL/interview additions** = extra knowledge we'll layer on top.

---

# 1. First: What is a SQL query?

Suppose we have:

### `Employees`

| idnamedepartmentsalary |       |       |       |
| ---------------------- | ----- | ----- | ----- |
| 1                      | Rahul | IT    | 70000 |
| 2                      | Priya | HR    | 50000 |
| 3                      | Aman  | IT    | 90000 |
| 4                      | Riya  | Sales | 60000 |

And I ask:

> Give me the names of employees who work in IT.

You're asking the database:

```
```

```
"Look at Employees,
find IT employees,
and give me their names."
```

SQL:

```
```

```
SELECT name
FROM Employees
WHERE department = 'IT';
```

This tiny query contains our first three fundamental concepts:

```
```

```
SELECT name
FROM Employees
WHERE department = 'IT';
```

### `SELECT`

> **What do I want?**

```
```

```
name
```

### `FROM`

> **Where do I want it from?**

```
```

```
Employees
```

### `WHERE`

> **Which rows do I want?**

```
```

```
department = 'IT'
```

---

# 2. The fundamental mental model

This is more useful than memorizing syntax:

```
```

```
SELECT → WHAT?
FROM   → WHERE FROM?
WHERE  → WHICH ROWS?
```

For:

```
```

```
SELECT name
FROM Employees
WHERE salary > 60000;
```

Think:

```
```

```
WHAT?
→ name

FROM?
→ Employees

WHICH ROWS?
→ salary > 60000
```

That mental translation will make SQL much easier.

---

# 3. `SELECT`

Your notes give the basic syntax:

```
```

```
SELECT column1, column2, ...
FROM table_name;
```

and:

```
```

```
SELECT *
FROM table_name;
```

to retrieve all columns. 

Let's practice.

Given:

| idnameagecity |       |    |        |
| ------------- | ----- | -- | ------ |
| 1             | Rahul | 22 | Delhi  |
| 2             | Priya | 24 | Mumbai |
| 3             | Aman  | 21 | Pune   |

### All columns

```
```

```
SELECT *
FROM students;
```

Result:

| idnameagecity |       |    |        |
| ------------- | ----- | -- | ------ |
| 1             | Rahul | 22 | Delhi  |
| 2             | Priya | 24 | Mumbai |
| 3             | Aman  | 21 | Pune   |

---

### Only names

```
```

```
SELECT name
FROM students;
```

Result:

| name  |
| ----- |
| Rahul |
| Priya |
| Aman  |

---

### Multiple columns

```
```

```
SELECT name, city
FROM students;
```

Result:

| namecity |        |
| -------- | ------ |
| Rahul    | Delhi  |
| Priya    | Mumbai |
| Aman     | Pune   |

---

# 4. `SELECT *` vs selecting columns

As a beginner, you'll frequently write:

```
```

```
SELECT *
FROM students;
```

That's perfectly useful while learning.

But in production/interview SQL, don't blindly use `*`.

If you only need:

```
```

```
name
city
```

write:

```
```

```
SELECT name, city
FROM students;
```

Why?

Because you're explicitly saying what data you need.

This becomes increasingly important when tables have dozens or hundreds of columns.

---

# 5. `FROM`

`FROM` tells SQL which table is the source.

```
```

```
SELECT name
FROM employees;
```

means:

```
```

```
Take the employees table
        ↓
look at its rows
        ↓
return name
```

So:

```
```

```
SELECT name
FROM employees;
```

is not asking:

> "Find a name somewhere in the database."

It says:

> "Look at the `employees` table and return its `name` column."

---

# 6. The hidden beauty of SELECT

Here's something I want you to notice.

Suppose the table has:

```
```

```
1 million rows
```

and:

```
```

```
SELECT name
FROM employees;
```

You didn't ask SQL to modify anything.

You're simply creating a **result set** from the existing data.

Conceptually:

```
```

```
TABLE
  ↓
SELECT / FROM / WHERE
  ↓
RESULT SET
```

The result set is what your application/client sees.

---

# 7. Now `WHERE`

Your notes:

> `WHERE` is used to filter records. 

Suppose:

| idnamesalary |       |       |
| ------------ | ----- | ----- |
| 1            | Rahul | 70000 |
| 2            | Priya | 50000 |
| 3            | Aman  | 90000 |

Query:

```
```

```
SELECT name
FROM employees
WHERE salary > 60000;
```

Let's mentally evaluate every row:

```
```

```
Rahul → 70000 > 60000 → TRUE  → keep
Priya → 50000 > 60000 → FALSE → discard
Aman  → 90000 > 60000 → TRUE  → keep
```

Result:

| name  |
| ----- |
| Rahul |
| Aman  |

This is the core idea of filtering.

---

# 8. WHERE is evaluated row by row

This is a very important mental model.

Suppose:

```
```

```
SELECT *
FROM employees
WHERE salary >= 60000;
```

Don't think:

> "WHERE somehow searches the table."

Think:

```
```

```
Row 1 → condition → TRUE/FALSE
Row 2 → condition → TRUE/FALSE
Row 3 → condition → TRUE/FALSE
Row 4 → condition → TRUE/FALSE
...
```

Only rows where the condition evaluates to **TRUE** survive the filter.

And this becomes VERY important when we discuss `NULL`.

---

# 9. Comparison operators

Your notes list:

```
```

```
=       equal
>       greater than
<       less than
>=      greater than or equal
<=      less than or equal
<>      not equal
```

and note that `!=` is also used in some SQL implementations. 

Let's make them concrete.

---

## `=`

```
```

```
SELECT *
FROM employees
WHERE department = 'IT';
```

Meaning:

> department must equal IT.

---

## `>`

```
```

```
SELECT *
FROM employees
WHERE salary > 60000;
```

Strictly greater.

`60000` itself doesn't qualify.

---

## `>=`

```
```

```
SELECT *
FROM employees
WHERE salary >= 60000;
```

Now `60000` qualifies.

---

## `<`

```
```

```
WHERE salary < 60000
```

---

## `<=`

```
```

```
WHERE salary <= 60000
```

---

## `<>`

```
```

```
WHERE department <> 'HR'
```

Meaning:

> department is not equal to HR.

MySQL also supports:

```
```

```
WHERE department != 'HR'
```

---

# 10. Strings require quotes

This:

```
```

```
WHERE department = 'IT'
```

is correct.

Don't write:

```
```

```
WHERE department = IT
```

because `IT` would be interpreted as an identifier rather than a string literal.

For strings:

```
```

```
'IT'
'India'
'Rahul'
```

For numeric values:

```
```

```
70000
22
100
```

typically without quotes.

---

# 11. `AND`

Your notes say `AND` requires all the conditions to be true. 

Example:

```
```

```
SELECT *
FROM employees
WHERE department = 'IT'
  AND salary > 60000;
```

We're asking:

```
```

```
department = IT
        AND
salary > 60000
```

Both must be true.

Suppose:

| namedepartmentsalary |    |       |
| -------------------- | -- | ----- |
| Rahul                | IT | 70000 |
| Aman                 | IT | 50000 |
| Priya                | HR | 80000 |

Evaluate:

```
```

```
Rahul:
IT = IT       → TRUE
70000 > 60000 → TRUE
                 ↓
               TRUE ✅

Aman:
IT = IT       → TRUE
50000 > 60000 → FALSE
                 ↓
               FALSE ❌

Priya:
HR = IT       → FALSE
80000 > 60000 → TRUE
                 ↓
               FALSE ❌
```

Result:

```
```

```
Rahul
```

---

# 12. `OR`

`OR` means:

> At least one condition must be TRUE.

Your notes explain that a row is selected if any condition separated by `OR` is true. 

Example:

```
```

```
SELECT *
FROM employees
WHERE department = 'IT'
   OR department = 'HR';
```

Meaning:

```
```

```
IT OR HR
```

So:

| departmentResult |   |
| ---------------- | - |
| IT               | ✅ |
| HR               | ✅ |
| Sales            | ❌ |
| Marketing        | ❌ |

---

# 13. `NOT`

`NOT` reverses the truth value of a condition.

```
```

```
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

Conceptually:

```
```

```
department = HR
       ↓
     NOT
       ↓
department ≠ HR
```

You could also write:

```
```

```
WHERE department <> 'HR'
```

Usually the latter is simpler.

---

# 14. The BIG `AND` + `OR` trap

This is where interview questions start getting interesting.

Suppose the requirement is:

> Employees who are in IT or HR, and whose salary is above 60000.

You might write:

```
```

```
WHERE department = 'IT'
   OR department = 'HR'
  AND salary > 60000;
```

⚠️ Dangerous.

SQL operator precedence matters.

`AND` is evaluated before `OR`.

So this behaves conceptually like:

```
```

```
WHERE department = 'IT'
   OR (
        department = 'HR'
        AND salary > 60000
      );
```

That is probably **not** what we intended.

---

# 15. Use parentheses

Correct:

```
```

```
SELECT *
FROM employees
WHERE (department = 'IT'
       OR department = 'HR')
  AND salary > 60000;
```

Now the logic is obvious:

```
```

```
        IT OR HR
           ↓
      salary > 60000
           ↓
          AND
```

### Interview rule

Whenever `AND` and `OR` are mixed:

> **Use parentheses unless you're deliberately relying on precedence.**

It makes your intention explicit and prevents bugs.

Your notes themselves demonstrate parenthesized combinations of `AND` and `OR`. 

---

# 16. Truth table

Let's make the logic concrete.

## AND

| ABA AND B |       |       |
| --------- | ----- | ----- |
| TRUE      | TRUE  | TRUE  |
| TRUE      | FALSE | FALSE |
| FALSE     | TRUE  | FALSE |
| FALSE     | FALSE | FALSE |

So:

> **AND = everything must pass.**

---

## OR

| ABA OR B |       |       |
| -------- | ----- | ----- |
| TRUE     | TRUE  | TRUE  |
| TRUE     | FALSE | TRUE  |
| FALSE    | TRUE  | TRUE  |
| FALSE    | FALSE | FALSE |

So:

> **OR = at least one must pass.**

---

## NOT

| ANOT A |       |
| ------ | ----- |
| TRUE   | FALSE |
| FALSE  | TRUE  |

---

# 17. NOW: NULL 😈

This is where SQL becomes different from ordinary programming.

Suppose:

| idnamemanager\_id |       |      |
| ----------------- | ----- | ---- |
| 1                 | Rahul | 10   |
| 2                 | Priya | NULL |
| 3                 | Aman  | 20   |

You want:

> Employees who don't have a manager.

Your first instinct might be:

```
```

```
WHERE manager_id = NULL
```

❌ Wrong.

Correct:

```
```

```
WHERE manager_id IS NULL;
```

Your notes specifically identify `IS NULL` as the way to check for NULL values. 

---

# 18. Why `= NULL` doesn't work

This is one of the most important SQL concepts.

SQL doesn't treat `NULL` as an ordinary value.

Instead:

```
```

```
5 = NULL
```

produces:

```
```

```
UNKNOWN
```

And:

```
```

```
NULL = NULL
```

also produces:

```
```

```
UNKNOWN
```

Not TRUE.

Not FALSE.

**UNKNOWN.**

That's SQL's **three-valued logic**.

```
```

```
TRUE
FALSE
UNKNOWN
```

Academic work on SQL semantics explicitly treats SQL's three-valued logic as a distinctive part of query processing. 

---

# 19. The WHERE rule that explains everything

Remember this:

> **WHERE keeps rows only when the condition evaluates to TRUE.**

What happens to:

```
```

```
FALSE
```

?

Discard.

What happens to:

```
```

```
UNKNOWN
```

?

Also discard.

Therefore:

```
```

```
WHERE manager_id = NULL
```

doesn't find NULLs.

The comparison evaluates to UNKNOWN.

So rows don't survive.

---

# 20. `IS NULL`

Instead:

```
```

```
WHERE manager_id IS NULL
```

asks specifically:

> Is this value NULL?

Now:

```
```

```
Rahul → 10     → FALSE
Priya → NULL   → TRUE
Aman  → 20     → FALSE
```

Result:

```
```

```
Priya
```

---

# 21. `IS NOT NULL`

Opposite:

```
```

```
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

Result:

```
```

```
Rahul
Aman
```

---

# 22. NULL + comparison operators

This is a HUGE interview concept.

Suppose:

```
```

```
salary
------
70000
NULL
50000
```

Query:

```
```

```
WHERE salary > 60000
```

Evaluation:

```
```

```
70000 > 60000 → TRUE
NULL > 60000  → UNKNOWN
50000 > 60000 → FALSE
```

Only:

```
```

```
TRUE
```

survives.

So the NULL row is excluded.

---

# 23. NULL + `<>`

Suppose:

```
```

```
WHERE department <> 'HR'
```

You might think:

```
```

```
IT  → TRUE
HR  → FALSE
NULL → TRUE?
```

No.

It's:

```
```

```
IT   → TRUE
HR   → FALSE
NULL → UNKNOWN
```

Therefore NULL is excluded.

This is why sometimes a query like:

```
```

```
WHERE referee_id != 2
```

doesn't return rows where `referee_id` is NULL.

And that's exactly why **LeetCode #584 — Find Customer Referee** is such a good first SQL problem.

---

# 24. LeetCode #1757 — Recyclable and Low Fat Products

Now let's apply everything.

The table conceptually contains:

```
```

```
Products
---------
product_id
low_fats
recyclable
```

Requirement:

> Find products that are both low fat and recyclable.

Translate English → SQL:

```
```

```
low_fats = 'Y'
AND
recyclable = 'Y'
```

Therefore:

```
```

```
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

### What concepts did we just use?

```
```

```
SELECT
FROM
WHERE
=
AND
```

That's it.

This is a perfect first problem because it tests whether you understand **AND as intersection of conditions**.

---

# 25. LeetCode #584 — Find Customer Referee

Now it gets more interesting.

Table:

```
```

```
Customer
---------
id
name
referee_id
```

Requirement:

> Find customers who were not referred by customer 2.

We might initially write:

```
```

```
SELECT name
FROM Customer
WHERE referee_id != 2;
```

But there's a problem.

What about:

```
```

```
referee_id = NULL
```

Because:

```
```

```
NULL != 2
```

is:

```
```

```
UNKNOWN
```

and UNKNOWN rows don't survive WHERE.

But the problem wants customers whose referee is **not 2**, including those with no referee.

So:

```
```

```
SELECT name
FROM Customer
WHERE referee_id <> 2
   OR referee_id IS NULL;
```

🔥 This is a **must-understand** SQL pattern.

```
```

```
not X
OR
NULL
```

---

# 26. LeetCode #595 — Big Countries

This one introduces another type of `WHERE`.

The table:

```
```

```
World
---------
name
continent
area
population
gdp
```

A country is considered big if:

```
```

```
area >= 3,000,000
OR
population >= 25,000,000
```

Translate directly:

```
```

```
SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
```

Notice the language:

> "condition A **or** condition B"

→ `OR`

This is why translating the English requirement into Boolean logic is such an important SQL skill.

---

# 27. LeetCode #1148 — Article Views I

Table:

```
```

```
Views
---------
article_id
author_id
viewer_id
view_date
```

Requirement:

> Find authors who viewed at least one of their own articles.

We need:

```
```

```
author_id = viewer_id
```

Query:

```
```

```
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

Now we've introduced something new:

```
```

```
DISTINCT
```

Your notes say `DISTINCT` removes duplicate rows from the query result. 

Suppose:

| author\_idviewer\_id |   |
| -------------------- | - |
| 1                    | 1 |
| 1                    | 1 |
| 2                    | 3 |
| 2                    | 2 |

After:

```
```

```
WHERE author_id = viewer_id
```

we get:

```
```

```
1
1
2
```

But we want:

```
```

```
1
2
```

So:

```
```

```
DISTINCT
```

removes the duplicate `1`.

---

# 28. LeetCode #1683 — Invalid Tweets

Table:

```
```

```
Tweets
---------
tweet_id
content
```

Requirement:

> Find tweets whose content length is greater than 15.

Now we need a **function**:

```
```

```
LENGTH(content)
```

Query:

```
```

```
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```

This is a great lesson:

```
```

```
WHERE
doesn't have to compare only raw columns.

It can compare:
        ↓
an expression/function
```

For example:

```
```

```
WHERE salary * 12 > 1000000
```

or:

```
```

```
WHERE LENGTH(content) > 15
```

We'll later study functions properly.

---

# 29. Your first five SQL 50 problems

Look at the progression:

| ProblemMain concept                   |                           |
| ------------------------------------- | ------------------------- |
| #1757 Recyclable and Low Fat Products | `WHERE` + `AND`           |
| #584 Find Customer Referee            | `NULL` + `IS NULL` + `OR` |
| #595 Big Countries                    | `OR` + comparison         |
| #1148 Article Views I                 | `WHERE` + `DISTINCT`      |
| #1683 Invalid Tweets                  | `WHERE` + function        |

This is **exactly** how I want us to learn the SQL 50.

Not:

```
```

```
Learn 50 syntax tricks
→ solve 50 problems
```

Instead:

```
```

```
Learn concept
    ↓
Understand why
    ↓
Solve relevant SQL 50 problems
    ↓
Extract pattern
    ↓
Interview question
    ↓
Next concept
```

---

# 30. A crucial distinction: SELECT vs WHERE

This is something interviewers love.

Suppose:

```
```

```
SELECT name
FROM employees
WHERE salary > 60000;
```

What does `SELECT` do?

> Determines which columns/expressions appear in the result.

What does `WHERE` do?

> Determines which rows are allowed into the result.

So:

```
```

```
SELECT → columns
WHERE  → rows
```

🔥 Memorize that.

---

# 31. Example

Table:

| idnamesalarydept |       |       |    |
| ---------------- | ----- | ----- | -- |
| 1                | Rahul | 70000 | IT |
| 2                | Priya | 50000 | HR |
| 3                | Aman  | 90000 | IT |

Query:

```
```

```
SELECT name, salary
FROM employees
WHERE dept = 'IT';
```

### `WHERE`

Filters:

```
```

```
Rahul → keep
Priya → remove
Aman  → keep
```

### `SELECT`

From the remaining rows, return:

```
```

```
name
salary
```

Result:

| namesalary |       |
| ---------- | ----- |
| Rahul      | 70000 |
| Aman       | 90000 |

---

# 32. SQL's logical thinking pattern

For every beginner query, I want you to mentally ask:

### Step 1

**What table?**

```
```

```
FROM ?
```

### Step 2

**Which rows?**

```
```

```
WHERE ?
```

### Step 3

**What information from those rows?**

```
```

```
SELECT ?
```

Example:

> Give me the names of IT employees earning more than 60k.

Think:

```
```

```
TABLE
→ employees

ROWS
→ department = IT
AND salary > 60000

OUTPUT
→ name
```

Then write:

```
```

```
SELECT name
FROM employees
WHERE department = 'IT'
  AND salary > 60000;
```

This approach is much more reliable than trying to remember SQL syntax mechanically.

---

# 33. Interview-level question: What happens if WHERE is omitted?

```
```

```
SELECT name
FROM employees;
```

All rows qualify.

Because there is no filtering condition.

Think:

```
```

```
FROM employees
     ↓
all rows
     ↓
SELECT name
```

---

# 34. Interview-level question: Can WHERE contain multiple conditions?

Absolutely.

```
```

```
WHERE salary > 60000
  AND department = 'IT'
  AND age >= 21
```

And:

```
```

```
WHERE department = 'IT'
   OR department = 'HR'
```

And:

```
```

```
WHERE NOT department = 'HR'
```

And combinations:

```
```

```
WHERE (department = 'IT' OR department = 'HR')
  AND salary > 60000
```

Your notes explicitly cover these logical combinations. 

---

# 35. One subtle correction to your notes

Your notes say:

> `NOT` displays a record if the condition is "NOT TRUE." 

For our interview preparation, be more precise:

SQL uses three-valued logic:

```
```

```
TRUE
FALSE
UNKNOWN
```

And:

```
```

```
NOT TRUE    → FALSE
NOT FALSE   → TRUE
NOT UNKNOWN → UNKNOWN
```

So don't think:

> `NOT` always turns a condition into its opposite boolean value in a simple TRUE/FALSE world.

`NULL` makes SQL more subtle.

---

# 36. Our first SQL pattern library

Start building this in your head.

### Pattern 1 — exact match

```
```

```
WHERE column = value
```

---

### Pattern 2 — numeric threshold

```
```

```
WHERE salary > 50000
```

---

### Pattern 3 — multiple requirements

```
```

```
WHERE condition1
  AND condition2
```

---

### Pattern 4 — alternatives

```
```

```
WHERE condition1
   OR condition2
```

---

### Pattern 5 — exclude a value

```
```

```
WHERE column <> value
```

---

### Pattern 6 — NULL

```
```

```
WHERE column IS NULL
```

---

### Pattern 7 — non-NULL

```
```

```
WHERE column IS NOT NULL
```

---

### Pattern 8 — duplicates in result

```
```

```
SELECT DISTINCT column
```

---

### Pattern 9 — function in filter

```
```

```
WHERE FUNCTION(column) > value
```

---

# 37. 🎯 The five problems we just learned

You should now be able to explain these **without looking at the SQL**:

### #1757

> Find products where **both** low\_fats and recyclable are Y.

```
```

```
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

### #584

> Find customers whose referee isn't 2 **or is NULL**.

```
```

```
SELECT name
FROM Customer
WHERE referee_id <> 2
   OR referee_id IS NULL;
```

### #595

> Find countries where area is huge **or** population is huge.

```
```

```
SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
```

### #1148

> Find authors who viewed their own articles and remove duplicates.

```
```

```
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

### #1683

> Find tweets whose content length exceeds 15.

```
```

```
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```

---

# 🧠 The most important takeaway today

Don't memorize:

```
```

```
SELECT ...
FROM ...
WHERE ...
```

as a template only.

Understand the **three questions**:

```
```

```
┌───────────────────────────────────┐
│ SELECT → WHAT do I want?          │
│ FROM   → WHERE is the data?       │
│ WHERE  → WHICH rows do I want?    │
└───────────────────────────────────┘
```

Then Boolean logic:

```
```

```
AND → both/all conditions
OR  → at least one
NOT → negation
```

And the SQL-specific monster:

```
```

```
NULL
 ↓
not an ordinary value
 ↓
comparisons with NULL → UNKNOWN
 ↓
WHERE keeps TRUE
 ↓
use IS NULL / IS NOT NULL
```

That last chain is the key to **#584**.

---

## 🔥 Your first interview challenge

Don't look at the answers yet. Solve these mentally/in SQL:

### Q1

Table:

```
```

```
Employees
id | name | salary | department
```

Write a query to find names of employees whose salary is greater than `50000`.

### Q2

Find employees who work in either `IT` or `HR`.

### Q3

Find employees who work in `IT` **and** earn at least `60000`.

### Q4

Find employees whose `manager_id` is NULL.

### Q5 — Interview trap

What is wrong with:

```
```

```
SELECT name
FROM Employees
WHERE manager_id = NULL;
```

### Q6 — SQL 50 style

A product is recyclable **and** low fat. Write the query.

### Q7 — harder

Find employees who are in **IT or HR** and whose salary is **greater than 60000**. Use parentheses correctly.

If you can solve those seven confidently, **you have actually learned** **`SELECT + FROM + WHERE + Boolean logic + NULL`** **rather than just read it.**

---

answers 

## Q1. Salary greater than 50,000

> Find names of employees whose salary is greater than `50000`.

```sql
SELECT name
FROM Employees
WHERE salary > 50000;
```

### Think:

```text
SELECT → what?       name
FROM   → where?      Employees
WHERE  → which rows? salary > 50000
```

---

# Q2. Employees in IT or HR

> Find employees who work in either `IT` or `HR`.

```sql
SELECT *
FROM Employees
WHERE department = 'IT'
   OR department = 'HR';
```

### Pattern

```text
A OR B
```

means **either condition can be true**.

Your notes define `OR` as returning a record when any of the conditions is true. 

---

# Q3. IT AND salary ≥ 60,000

```sql
SELECT *
FROM Employees
WHERE department = 'IT'
  AND salary >= 60000;
```

### Pattern

```text
A AND B
```

means **both conditions must be true**.

So an employee with:

```text
IT + 70000  → ✅
IT + 50000  → ❌
HR + 70000  → ❌
```

Your notes describe `AND` exactly this way. 

---

# Q4. Employees whose manager\_id is NULL

This is the important one.

```sql
SELECT *
FROM Employees
WHERE manager_id IS NULL;
```

### ❌ Don't write:

```sql
WHERE manager_id = NULL;
```

Use:

```sql
IS NULL
```

Your notes specifically give `IS NULL` for checking NULL values. 

---

# Q5. Interview trap

Given:

```sql
SELECT name
FROM Employees
WHERE manager_id = NULL;
```

### What's wrong?

`NULL` is **not an ordinary value that you compare using** **`=`**.

So:

```text
manager_id = NULL
```

doesn't correctly test for NULL.

Use:

```sql
SELECT name
FROM Employees
WHERE manager_id IS NULL;
```

### Interview answer 🎯

If the interviewer asks:

> "How do you check whether a column contains NULL?"

Say:

> **I use** **`IS NULL`****, not** **`= NULL`****. Similarly, I use** **`IS NOT NULL`** **to check for non-NULL values.**

---

# Q6. Recyclable AND low fat

This is **LeetCode #1757**.

Requirement:

> Product must be low fat **and** recyclable.

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

### Translation skill

English:

```text
low fat AND recyclable
```

SQL:

```sql
low_fats = 'Y'
AND recyclable = 'Y'
```

This is exactly the kind of direct Boolean translation you want to become automatic.

---

# Q7. IT or HR AND salary > 60,000

This is the most important one of the seven.

Requirement:

> Employees who are in **IT or HR** and whose salary is **greater than 60000**.

Correct:

```sql
SELECT *
FROM Employees
WHERE (department = 'IT'
       OR department = 'HR')
  AND salary > 60000;
```

### Read it as:

```text
          ┌── IT ──┐
Employee ─┤        ├── AND ── salary > 60000
          └── HR ──┘
```

Or mathematically:

```text
(IT OR HR) AND salary > 60000
```

---

# ⚠️ Why parentheses matter

Don't write this casually:

```sql
WHERE department = 'IT'
   OR department = 'HR'
  AND salary > 60000;
```

Because SQL evaluates `AND` before `OR`.

So it is effectively:

```sql
WHERE department = 'IT'
   OR (department = 'HR' AND salary > 60000);
```

That's a **different condition**.

The safe interview habit is:

```sql
WHERE (condition1 OR condition2)
  AND condition3;
```

---

# 🧠 Your 7 answers together

```sql
-- Q1
SELECT name
FROM Employees
WHERE salary > 50000;


-- Q2
SELECT *
FROM Employees
WHERE department = 'IT'
   OR department = 'HR';


-- Q3
SELECT *
FROM Employees
WHERE department = 'IT'
  AND salary >= 60000;


-- Q4
SELECT *
FROM Employees
WHERE manager_id IS NULL;


-- Q5
-- WRONG:
-- WHERE manager_id = NULL

-- CORRECT:
SELECT name
FROM Employees
WHERE manager_id IS NULL;


-- Q6 — LeetCode #1757
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';


-- Q7
SELECT *
FROM Employees
WHERE (department = 'IT'
       OR department = 'HR')
  AND salary > 60000;
```

---

# 🔥 The pattern you should now have in your brain

Whenever you see an SQL question, translate:

### "Give me..."

```text
↓
SELECT
```

### "from..."

```text
↓
FROM
```

### "where..."

```text
↓
WHERE
```

### "and..."

```text
↓
AND
```

### "or..."

```text
↓
OR
```

### "not equal..."

```text
↓
<> / !=
```

### "is missing / has no value..."

```text
↓
IS NULL
```

### "has a value..."

```text
↓
IS NOT NULL
```

Your notes establish `SELECT` as the foundation of DQL and `WHERE` as the filtering clause, followed by these comparison and logical operators.


---

Part 5 

One important thing: your notes **do not provide a dedicated section for MySQL string functions such as** **`LOWER()`****,** **`UPPER()`****,** **`CONCAT()`****, etc.** So I'll clearly mark those as **MySQL/interview additions**, rather than pretending they're from your notes.

# 🧠 Part 2 — Filtering Like an Interviewer

Our toolbox is now:

```
SELECT
FROM
WHERE
│
├── =
├── > < >= <= <>
├── AND / OR / NOT
├── IS NULL
├── DISTINCT
├── LIKE
├── IN
└── BETWEEN

AS → rename output
```

The notes place these directly in the DQL/`SELECT` material. 

---

# 1. `DISTINCT`

## What problem does it solve?

Imagine:

```
Employees

id   name    department
1    Rahul   IT
2    Aman    HR
3    Priya   IT
4    Riya    IT
5    John    HR
```

If you ask:

```
SELECT department
FROM Employees;
```

you could get:

```
IT
HR
IT
IT
HR
```

But maybe the interviewer asks:

> "What are the different departments?"

You don't want duplicates.

Use:

```
SELECT DISTINCT department
FROM Employees;
```

Result:

```
IT
HR
```

Your notes define `DISTINCT` as removing duplicate rows from the query result. 

---

## ⚠️ Important: DISTINCT applies to the combination

Consider:

```
SELECT DISTINCT department, city
FROM Employees;
```

`DISTINCT` doesn't mean:

> "Make department unique and city unique independently."

It means:

> Remove duplicate **combinations of** **`(department, city)`**.

Example:

| department | city |
| -------------- | ------ |
| IT             | Delhi  |
| IT             | Delhi  |
| IT             | Mumbai |
| HR             | Delhi  |

Result:

| department | city |
| -------------- | ------ |
| IT             | Delhi  |
| IT             | Mumbai |
| HR             | Delhi  |

### Interview question

**Q:** Does `DISTINCT` apply to one column or the entire selected row?

**A:** The duplicate check applies to the **combination of the selected expressions/columns**.

---

# 2. `AS` — Aliases

Now suppose:

```
SELECT first_name
FROM employees;
```

The output column is:

```
first_name
```

But maybe you want:

```
Employee Name
```

Use an alias:

```
SELECT first_name AS employee_name
FROM employees;
```

Result:

```
employee_name
-------------
Rahul
Priya
Aman
```

Your notes describe `AS` as renaming columns or expressions in the query result. 

---

## Alias doesn't rename the actual column

This is important.

```
SELECT first_name AS employee_name
FROM employees;
```

does **not** change the database schema.

It only changes the name displayed in the result.

Think:

```
Database column:
first_name

        ↓ AS

Query output:
employee_name
```

---

# 3. Alias with expressions

This becomes very useful later.

```
SELECT salary * 12 AS annual_salary
FROM Employees;
```

Suppose:

```
salary = 50000
```

Output:

```
annual_salary
-------------
600000
```

Your notes also describe aliases for expressions. 

---

# 4. `LIKE`

Now we're getting into **pattern matching**.

Your notes define `LIKE` as an operator used in `WHERE` to search for a specified pattern. 

Suppose:

```
Customers

name
--------
Rahul
Ramesh
Priya
Riya
Aman
```

Question:

> Find customers whose name starts with `R`.

```
SELECT *
FROM Customers
WHERE name LIKE 'R%';
```

Result:

```
Rahul
Ramesh
Riya
```

---

# 5. `%` — the wildcard

This is extremely important.

Your notes say:

> `%` represents zero, one, or multiple characters. 

So:

```
LIKE 'R%'
```

means:

```
R
R + anything
```

Examples:

```
R
Rahul
Ramesh
Riya
R12345
```

All potentially match.

---

# 6. `%` positions

## Starts with R

```
WHERE name LIKE 'R%'
```

```
Rahul       ✅
Riya        ✅
Aman        ❌
```

---

## Ends with a

```
WHERE name LIKE '%a'
```

Your notes explicitly give this pattern. 

```
Priya       ✅
Riya        ✅
Rahul       ❌
```

---

## Contains "or"

```
WHERE name LIKE '%or%'
```

Means:

```
anything
+
"or"
+
anything
```

Your notes give this exact pattern. 

---

# 7. `_` — exactly one character

This is different from `%`.

Your notes say:

> `_` represents one single character. 

Example:

```
WHERE name LIKE '_a%'
```

Break it down:

```
_   → exactly one character
a   → must be a
%   → anything afterward
```

So:

```
Rahul
```

doesn't necessarily match because second character is `a`? Actually:

```
R a h u l
↑ ↑
_ a
```

Yes → matches.

---

## Compare `%` and `_`

### `%`

```
zero or more characters
```

### `_`

```
exactly one character
```

This distinction is **interview gold**.

---

# 8. Pattern examples

Let's make this automatic.

| PatternMeaning |                            |
| -------------- | -------------------------- |
| `'A%'`         | starts with A              |
| `'%A'`         | ends with A                |
| `'%A%'`        | contains A                 |
| `'_A%'`        | A is second character      |
| `'A_%'`        | starts A, at least 2 chars |
| `'A__%'`       | starts A, at least 3 chars |
| `'A%O'`        | starts A and ends O        |

These patterns are directly reflected in your notes. 

---

# 9. `IN`

Suppose you want:

> Employees in IT, HR, or Sales.

You could write:

```
SELECT *
FROM Employees
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Sales';
```

That's valid.

But SQL gives us a cleaner way:

```
SELECT *
FROM Employees
WHERE department IN ('IT', 'HR', 'Sales');
```

Your notes describe `IN` as filtering results based on a list of values. 

---

# 10. IN = multiple OR conditions

This is a great mental transformation:

```
WHERE department IN ('IT', 'HR', 'Sales')
```

Think:

```
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Sales'
```

So:

```
IN
 ↓
"Does this value belong to this list?"
```

---

# 11. `NOT IN`

You can also exclude a list:

```
SELECT *
FROM Employees
WHERE department NOT IN ('HR', 'Sales');
```

Meaning:

```
department is neither HR nor Sales
```

### ⚠️ NULL warning

This is another place where `NULL` can create surprising behavior.

If `department` can be `NULL`, don't casually assume `NOT IN` will include those rows.

Remember our previous rule:

```
NULL + comparison
        ↓
UNKNOWN
        ↓
WHERE doesn't keep it
```

---

# 12. `BETWEEN`

Suppose:

```
salary
------
40000
50000
60000
70000
80000
```

Question:

> Find salaries from 50,000 to 70,000.

You can write:

```
WHERE salary >= 50000
  AND salary <= 70000
```

Or:

```
WHERE salary BETWEEN 50000 AND 70000;
```

Your notes describe `BETWEEN` as filtering within a specified range. 

---

# 🚨 VERY IMPORTANT: BETWEEN is inclusive

This:

```
WHERE salary BETWEEN 50000 AND 70000
```

means:

```
50000 ≤ salary ≤ 70000
```

Therefore:

```
50000 → ✅
60000 → ✅
70000 → ✅
70001 → ❌
49999 → ❌
```

Memorize:

> **BETWEEN includes both endpoints.**

---

# 13. BETWEEN with dates

Your notes give:

```
SELECT *
FROM orders
WHERE order_date BETWEEN '2023-01-01' AND '2023-06-30';
```

This means dates from the beginning of January 1 through June 30, with the comparison inclusive at the boundaries.

We'll go much deeper into date filtering later because it becomes extremely important in the SQL 50 problems.

---

# 14. `IS NULL` — quick reinforcement

We already learned:

```
WHERE email IS NULL
```

Your notes explicitly use this pattern. 

And:

```
WHERE email IS NOT NULL
```

means:

> Give me rows where email has a value.

Never:

```
WHERE email = NULL
```

---

# 15. Combining everything

Now we can write much more expressive queries.

Suppose:

```
Employees
---------------------------
name
department
salary
email
```

Question:

> Find IT or HR employees whose salary is between 50k and 80k.

```
SELECT name
FROM Employees
WHERE department IN ('IT', 'HR')
  AND salary BETWEEN 50000 AND 80000;
```

That's already a very realistic interview query.

Break it down:

```
department IN (...)
        ↓
     IT or HR

salary BETWEEN ...
        ↓
50k through 80k

        ↓
       AND

        ↓
     SELECT name
```

---

# 16. Another interview-style example

> Find employees whose name starts with `A`, work in IT or HR, and have an email.

```
SELECT name
FROM Employees
WHERE name LIKE 'A%'
  AND department IN ('IT', 'HR')
  AND email IS NOT NULL;
```

Look how naturally our concepts combine:

```
LIKE
+
IN
+
IS NOT NULL
+
AND
```

This is exactly why we're learning them together.

---

# 17. String functions — MySQL addition

Now let's distinguish this from your notes.

Your uploaded notes cover the `LIKE` pattern operator and its wildcards, but the retrieved material doesn't contain a dedicated section teaching functions such as `LOWER()`, `UPPER()`, `CONCAT()`, or `SUBSTRING()`. 

So from here, I'm adding **MySQL/interview knowledge**.

The first functions you should know are:

```
LOWER()
UPPER()
LENGTH()
CONCAT()
SUBSTRING()
```

---

# 18. `LOWER()`

Converts a string to lowercase.

```
SELECT LOWER(name)
FROM Employees;
```

Example:

```
RAHUL
```

becomes:

```
rahul
```

Useful when you need normalized text comparison/display.

---

# 19. `UPPER()`

Opposite:

```
SELECT UPPER(name)
FROM Employees;
```

```
rahul
```

→

```
RAHUL
```

---

# 20. `LENGTH()`

Returns the length of a string in bytes in MySQL.

For basic ASCII text, you'll commonly see it behave like character length:

```
SELECT LENGTH('Rahul');
```

Result:

```
5
```

And this is exactly the type of idea you'll need for:

### LeetCode #1683 — Invalid Tweets

```
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```

So we have already seen our first connection:

```
STRING FUNCTION
      ↓
  LENGTH()
      ↓
    WHERE
      ↓
LeetCode #1683
```

---

# 21. `CONCAT()`

Combines strings.

Suppose:

```
first_name | last_name
-----------|----------
Rahul      | Kumar
Priya      | Sharma
```

Query:

```
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM Employees;
```

Result:

```
full_name
------------
Rahul Kumar
Priya Sharma
```

This is very useful in real-world SQL.

---

# 22. `SUBSTRING()`

Extract part of a string.

For example:

```
SELECT SUBSTRING('ABCDEFG', 2, 3);
```

Conceptually:

```
A B C D E F G
  ↑-----↑
```

Result:

```
BCD
```

The exact syntax/details matter when we start solving the string-heavy SQL 50 problems, so we'll revisit this when we reach **Advanced String Functions / Regex / Clause**.

---

# 23. One VERY important distinction

Don't confuse:

```
LIKE
```

with:

```
=
```

### `=`

Exact comparison.

```
WHERE name = 'Rahul'
```

Means exactly Rahul.

### `LIKE`

Pattern comparison.

```
WHERE name LIKE 'Rah%'
```

Means the value matches the specified pattern.

---

# 24. `LIKE` + `NOT`

You can also write:

```
WHERE name NOT LIKE 'A%'
```

Meaning:

> name does not match the pattern beginning with A.

---

# 25. LeetCode connection: #1148

We already solved:

```
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

Now look at what we learned:

```
DISTINCT → remove duplicates
AS       → rename author_id to id
WHERE    → filter own views
```

So #1148 was secretly teaching **three concepts**.

That's exactly how I want you to approach SQL 50.

---

# 26. LeetCode #1517 — Find Users With Valid E-Mails

This is where `LIKE` becomes useful.

The requirement is essentially:

> Find users whose email matches the required pattern.

The important concept is:

```
WHERE mail LIKE ...
```

For example, pattern matching often looks like:

```
WHERE mail LIKE '%@leetcode.com'
```

But #1517 has additional requirements around the valid username characters, so the final solution involves more than simply memorizing one `LIKE` pattern.

We'll solve it properly when we reach **regex/string filtering**, because the problem belongs to that section of SQL 50.

The important lesson now:

```
LIKE
 ↓
pattern matching
 ↓
emails / names / text
 ↓
#1517
```

---

# 27. LeetCode #1527 — Patients With a Condition

This is another excellent `LIKE` problem.

Suppose the `conditions` column contains values such as:

```
"DIAB100 MYOP"
"ASTHMA DIAB100"
"MYOP"
```

Requirement:

> Find patients who have a condition beginning with `DIAB1`.

The tricky part is that `DIAB100` might appear:

```
at the beginning
```

or:

```
after a space
```

This is a beautiful example of why pattern thinking matters.

We'll solve it when we do the actual problem, but mentally you're looking for patterns such as:

```
'DIAB1%'
```

and:

```
'% DIAB1%'
```

That is a direct application of `%` and pattern matching from your notes. 

---

# 28. LeetCode #1667 — Fix Names in a Table

This one is particularly useful because it combines **string functions** with ordering.

The requirement is essentially to normalize names so the first character is uppercase and the remaining characters are lowercase.

Conceptually:

```
"alice"
```

becomes:

```
"Alice"
```

This will require functions such as:

```
UPPER()
LOWER()
SUBSTRING()
```

We'll treat #1667 as our first **string-function-focused SQL 50 problem**.

---

# 29. Your SQL mental dictionary

At this point, when an interviewer says:

> "different"

Think:

```
DISTINCT
```

---

> "starts with"

Think:

```
LIKE 'A%'
```

---

> "ends with"

Think:

```
LIKE '%A'
```

---

> "contains"

Think:

```
LIKE '%A%'
```

---

> "second character is A"

Think:

```
LIKE '_A%'
```

---

> "one of these values"

Think:

```
IN (...)
```

---

> "not one of these values"

Think:

```
NOT IN (...)
```

---

> "between X and Y"

Think:

```
BETWEEN X AND Y
```

Remember:

```
inclusive
```

---

> "missing / no value"

Think:

```
IS NULL
```

---

> "has a value"

Think:

```
IS NOT NULL
```

---

> "call this result something else"

Think:

```
AS
```

---

# 30. One combined interview problem

Let's put everything together.

### Table

```
Employees
------------------------------------------------
id | name | department | salary | email
```

### Requirement

> Find the names of employees whose name starts with `A`, who are in IT, HR, or Sales, whose salary is between 50,000 and 100,000, and whose email isn't NULL. Return the name as `employee_name`.

Don't panic.

Translate sentence by sentence:

```
names
 ↓
SELECT name

employees
 ↓
FROM Employees

starts with A
 ↓
name LIKE 'A%'

IT / HR / Sales
 ↓
department IN (...)

50k to 100k
 ↓
salary BETWEEN 50000 AND 100000

email isn't NULL
 ↓
email IS NOT NULL

rename output
 ↓
AS employee_name
```

Final:

```
SELECT name AS employee_name
FROM Employees
WHERE name LIKE 'A%'
  AND department IN ('IT', 'HR', 'Sales')
  AND salary BETWEEN 50000 AND 100000
  AND email IS NOT NULL;
```

🔥 **This is the skill we're building.**

Not memorizing SQL.

**English → logic → SQL.**

---

# 31. Quick interview traps

### Trap #1

```
WHERE name = 'A%'
```

❌ Not a pattern match.

Use:

```
WHERE name LIKE 'A%'
```

---

### Trap #2

```
WHERE salary BETWEEN 50000 AND 100000
```

Does `50000` qualify?

**Yes.**

Does `100000` qualify?

**Yes.**

`BETWEEN` is inclusive.

---

### Trap #3

```
WHERE email = NULL
```

❌

Use:

```
WHERE email IS NULL
```

---

### Trap #4

```
WHERE department = 'IT'
   OR 'HR'
```

❌ Don't write conditions like that.

Use:

```
WHERE department IN ('IT', 'HR')
```

or:

```
WHERE department = 'IT'
   OR department = 'HR'
```

---

### Trap #5

```
SELECT DISTINCT department, city
```

Does it make both columns independently unique?

**No.**

It removes duplicate **department + city combinations**.

---

# 🎯 What I want you to master from this lesson

You should now be able to see:

```
                    SQL FILTERING
                         │
       ┌─────────────────┼─────────────────┐
       │                 │                 │
   Exact match       Pattern            Lists
       │                 │                 │
       =               LIKE              IN
                         │
                    ┌────┴────┐
                    %         _
                many/zero   exactly 1


                  Ranges
                     │
                  BETWEEN
                     │
                 inclusive


                   NULL
                     │
              ┌──────┴──────┐
              │             │
          IS NULL      IS NOT NULL


                  Output
                     │
                    AS
                     │
                  alias


                Duplicates
                     │
                  DISTINCT
```

And then:

```
                 STRING FUNCTIONS
                       │
          ┌────────────┼────────────┐
          │            │            │
       LOWER        UPPER        LENGTH
          │            │            │
          └────────────┼────────────┘
                       │
                    CONCAT
                       │
                   SUBSTRING
```

The first group is directly supported by your notes; the second group is additional MySQL/interview knowledge because the retrieved notes don't have a dedicated string-functions section. 

---

## 🧪 Now let's test you

Don't solve these mentally only—actually write the SQL.

### Q1

Find unique departments from `Employees`.

### Q2

Find employees whose name starts with `S`.

### Q3

Find employees whose name contains `"an"` anywhere.

### Q4

Find employees from `IT`, `HR`, or `Finance`.

### Q5

Find employees with salary between `60000` and `90000`.

### Q6

Find employees who don't have an email.

### Q7

Return `first_name` as `employee_name`.

### Q8 🔥 Combined

Find unique cities of employees whose department is either `IT` or `HR`, whose name starts with `A`, and whose salary is between `50000` and `100000`.

### Q9 🔥 Interview trap

What's the difference between:

```
WHERE name LIKE 'A%'
```

and:

```
WHERE name LIKE 'A_'
```

### Q10 🔥 Think

What does this return?

```
SELECT DISTINCT department, city
FROM Employees;
```

---
Answers 
# Q1. Find unique departments

### Answer

```sql
SELECT DISTINCT department
FROM Employees;
```

### Why?

`DISTINCT` removes duplicate values from the result.

If the table contains:

```text
IT
HR
IT
Finance
HR
```

the result is:

```text
IT
HR
Finance
```

### Interview phrase

> "`DISTINCT` eliminates duplicate result rows."

---

# Q2. Employees whose name starts with `S`

### Answer

```sql
SELECT *
FROM Employees
WHERE name LIKE 'S%';
```

### Why?

`%` means **zero or more characters**.

So:

```text
'S%'
```

means:

```text
S
S + anything
```

Examples:

```text
Sam       ✅
Sarah     ✅
Steve     ✅
Rahul     ❌
```

---

# Q3. Employees whose name contains `"an"`

### Answer

```sql
SELECT *
FROM Employees
WHERE name LIKE '%an%';
```

### Breakdown

```text
%an%
│  │
│  └── "an"
└───── anything before/after
```

So `"an"` can occur anywhere.

Examples:

```text
Anand       ✅
Sanjay      ✅
Rohan       ✅
Rahul       ❌
```

---

# Q4. Employees from IT, HR, or Finance

### Answer

```sql
SELECT *
FROM Employees
WHERE department IN ('IT', 'HR', 'Finance');
```

### Equivalent version

```sql
SELECT *
FROM Employees
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Finance';
```

The `IN` version is cleaner.

### Mental model

```text
IN (...)
   ↓
"Does this value belong to this list?"
```

---

# Q5. Salary between 60,000 and 90,000

### Answer

```sql
SELECT *
FROM Employees
WHERE salary BETWEEN 60000 AND 90000;
```

### Very important

`BETWEEN` is **inclusive**.

Therefore:

```text
60000 → ✅
75000 → ✅
90000 → ✅
59999 → ❌
90001 → ❌
```

Equivalent:

```sql
WHERE salary >= 60000
  AND salary <= 90000
```

---

# Q6. Employees who don't have an email

### Answer

```sql
SELECT *
FROM Employees
WHERE email IS NULL;
```

### 🚨 Remember

NOT:

```sql
WHERE email = NULL;
```

Correct:

```sql
WHERE email IS NULL;
```

Because `NULL` represents an unknown/missing value, and SQL provides `IS NULL` specifically for testing it.

---

# Q7. Return `first_name` as `employee_name`

### Answer

```sql
SELECT first_name AS employee_name
FROM Employees;
```

You can also write:

```sql
SELECT first_name employee_name
FROM Employees;
```

But I recommend using `AS` while learning because it makes the intention explicit.

### Important

This:

```text
AS employee_name
```

does **not** rename the database column.

It only renames the column in the query result.

---

# Q8. 🔥 Combined

> Find unique cities of employees whose department is either IT or HR, whose name starts with A, and whose salary is between 50,000 and 100,000.

Let's translate the English piece by piece.

### "unique cities"

```text
DISTINCT city
```

### "IT or HR"

```text
department IN ('IT', 'HR')
```

### "name starts with A"

```text
name LIKE 'A%'
```

### "salary between 50k and 100k"

```text
salary BETWEEN 50000 AND 100000
```

### Combine with `AND`

```sql
SELECT DISTINCT city
FROM Employees
WHERE department IN ('IT', 'HR')
  AND name LIKE 'A%'
  AND salary BETWEEN 50000 AND 100000;
```

🔥 This is exactly the kind of translation skill you want for interviews.

---

# Q9. 🔥 `LIKE 'A%'` vs `LIKE 'A_'`

This is an important wildcard question.

## `LIKE 'A%'`

```sql
WHERE name LIKE 'A%'
```

Means:

> Starts with A, followed by **zero or more characters**.

Examples:

```text
A        ✅
Aman     ✅
Alice    ✅
Andrew   ✅
```

---

## `LIKE 'A_'`

```sql
WHERE name LIKE 'A_'
```

Means:

> Starts with A and has **exactly one additional character**.

Therefore:

```text
AB       ✅
AX       ✅
A        ❌
Aman     ❌
Alice    ❌
```

### Memorize this forever:

```text
%  → zero or more characters
_  → exactly one character
```

This distinction is directly covered in your notes. 

---

# Q10. 🔥 What does this return?

```sql
SELECT DISTINCT department, city
FROM Employees;
```

It returns **unique combinations of** **`department`** **and** **`city`**.

Suppose:

| department | city   |
| ---------- | ------ |
| IT         | Delhi  |
| IT         | Delhi  |
| IT         | Mumbai |
| HR         | Delhi  |
| HR         | Delhi  |
| HR         | Mumbai |

Query:

```sql
SELECT DISTINCT department, city
FROM Employees;
```

Result:

| department | city   |
| ---------- | ------ |
| IT         | Delhi  |
| IT         | Mumbai |
| HR         | Delhi  |
| HR         | Mumbai |

### 🚨 Important interview point

`DISTINCT` does **not** mean:

> Make `department` unique and `city` unique independently.

It means:

> Remove duplicate **rows/combinations of the selected expressions**.

---

# 🧠 The 10 answers together

```sql
-- Q1
SELECT DISTINCT department
FROM Employees;


-- Q2
SELECT *
FROM Employees
WHERE name LIKE 'S%';


-- Q3
SELECT *
FROM Employees
WHERE name LIKE '%an%';


-- Q4
SELECT *
FROM Employees
WHERE department IN ('IT', 'HR', 'Finance');


-- Q5
SELECT *
FROM Employees
WHERE salary BETWEEN 60000 AND 90000;


-- Q6
SELECT *
FROM Employees
WHERE email IS NULL;


-- Q7
SELECT first_name AS employee_name
FROM Employees;


-- Q8
SELECT DISTINCT city
FROM Employees
WHERE department IN ('IT', 'HR')
  AND name LIKE 'A%'
  AND salary BETWEEN 50000 AND 100000;


-- Q9
-- 'A%' → A followed by zero or more characters
-- 'A_' → A followed by exactly one character


-- Q10
SELECT DISTINCT department, city
FROM Employees;
-- Removes duplicate (department, city) combinations.
```

---

# 🎯 What you should now be able to translate instantly

| Interview wording | SQL                |
| ------------------ | ------------------ |
| unique/different   | `DISTINCT`         |
| starts with A      | `LIKE 'A%'`        |
| ends with A        | `LIKE '%A'`        |
| contains A         | `LIKE '%A%'`       |
| second character is A | `LIKE '_A%'`    |
| one of these       | `IN (...)`         |
| none of these      | `NOT IN (...)`     |
| between X and Y    | `BETWEEN X AND Y`  |
| missing value      | `IS NULL`          |
| has a value        | `IS NOT NULL`      |
| rename output      | `AS`               |

And the three wildcard rules:

```text
%       → 0 or more characters
_       → exactly 1 character
BETWEEN → inclusive
```

These are foundational for several of the SQL 50 problems we're going to hit, especially **#1517, #1527, #1667, #1683**, and later the more advanced string problems.

---

PART 6

# 🗺️ Our systematic path

We're currently here:

```
```

```
SELECT
  ↓
FROM
  ↓
WHERE
  ↓
DISTINCT / LIKE / IN / BETWEEN / NULL / AS
  ↓
👉 ORDER BY        ← WE ARE HERE
  ↓
LIMIT
  ↓
Aggregate Functions
  ↓
GROUP BY
  ↓
HAVING
  ↓
JOINS
  ↓
Subqueries
  ↓
String / Regex
  ↓
Advanced SQL
```

And this maps nicely onto your notes' general query structure:

```
```

```
SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...;
```

---

# PART 1 — `ORDER BY`

## 1. What does `ORDER BY` actually do?

Imagine:

```
```

```
Employees

name      salary
----------------
Rahul     70000
Aman      50000
Priya     90000
John      60000
```

If we write:

```
```

```
SELECT name, salary
FROM Employees;
```

**SQL does not promise that the rows will come back in a particular order.**

If the interviewer says:

> "Show employees sorted by salary."

That's when you use:

```
```

```
SELECT name, salary
FROM Employees
ORDER BY salary;
```

Result conceptually:

```
```

```
Aman      50000
John      60000
Rahul     70000
Priya     90000
```

Your notes describe `ORDER BY` as sorting the result set based on one or more columns. 

---

# 2. `ASC` — ascending

```
```

```
SELECT name, salary
FROM Employees
ORDER BY salary ASC;
```

Ascending means:

```
```

```
small → large
```

For numbers:

```
```

```
10
20
30
40
```

For text, generally:

```
```

```
A
B
C
D
```

For dates:

```
```

```
2024-01-01
2024-02-01
2024-03-01
```

---

# 3. `DESC` — descending

Now:

```
```

```
SELECT name, salary
FROM Employees
ORDER BY salary DESC;
```

means:

```
```

```
large → small
```

Result:

```
```

```
90000
70000
60000
50000
```

Your notes explicitly state that `ASC` sorts ascending and `DESC` descending. 

---

# 🚨 Interview fact: ASC is the default

These are equivalent:

```
```

```
ORDER BY salary;
```

and:

```
```

```
ORDER BY salary ASC;
```

Your notes state that ascending is the default. 

### My recommendation

Even though this works:

```
```

```
ORDER BY salary;
```

when you're learning, write:

```
```

```
ORDER BY salary ASC;
```

or:

```
```

```
ORDER BY salary DESC;
```

It makes your intention obvious.

---

# 4. Where does `ORDER BY` go?

This is extremely important.

Correct:

```
```

```
SELECT ...
FROM ...
WHERE ...
ORDER BY ...;
```

For example:

```
```

```
SELECT name, salary
FROM Employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

Read it:

> Give me names and salaries from Employees, only IT employees, sorted from highest salary to lowest.

---

# 5. The mental execution

For this:

```
```

```
SELECT name, salary
FROM Employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

Think:

```
```

```
Employees
    ↓
Filter IT
    ↓
Remaining employees
    ↓
Sort by salary
    ↓
Highest → Lowest
```

So:

> **WHERE decides which rows survive.**

> **ORDER BY decides the order of those surviving rows.**

That's a very useful interview distinction.

---

# 6. `WHERE` vs `ORDER BY`

Suppose:

```
```

```
Employees

name     department   salary
-----------------------------
Aman     IT           50000
Rahul    HR           90000
Priya    IT           80000
John     IT           60000
```

Query:

```
```

```
SELECT name, salary
FROM Employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

First:

```
```

```
WHERE department = 'IT'
```

removes Rahul.

Then:

```
```

```
ORDER BY salary DESC
```

sorts:

```
```

```
Priya   80000
John    60000
Aman    50000
```

---

# PART 2 — Sorting by multiple columns

This is where interview questions start becoming interesting.

Suppose:

```
```

```
Employees

name      department    salary
--------------------------------
Rahul     IT            80000
Aman      HR            70000
Priya     IT            80000
John      HR            90000
```

Question:

> Sort employees by department, and within each department sort by salary descending.

Answer:

```
```

```
SELECT name, department, salary
FROM Employees
ORDER BY department ASC,
         salary DESC;
```

Your notes explicitly explain this idea: rows are first sorted using the first column, and when values are equal, the next column is used. 

---

# 🧠 How to visualize multiple `ORDER BY`

Think of:

```
```

```
ORDER BY department ASC,
         salary DESC;
```

as:

```
```

```
PRIMARY SORT
department
    ↓
IT
HR
    ↓
Within each department...
    ↓
SECONDARY SORT
salary DESC
```

The **first expression has priority**.

---

# 7. Example

Input:

| namedepartmentsalary |    |       |
| -------------------- | -- | ----- |
| Rahul                | IT | 70000 |
| Priya                | IT | 90000 |
| Aman                 | HR | 50000 |
| John                 | HR | 80000 |

Query:

```
```

```
SELECT *
FROM Employees
ORDER BY department ASC,
         salary DESC;
```

Result:

| namedepartmentsalary |    |       |
| -------------------- | -- | ----- |
| John                 | HR | 80000 |
| Aman                 | HR | 50000 |
| Priya                | IT | 90000 |
| Rahul                | IT | 70000 |

First:

```
```

```
HR
IT
```

Then within HR:

```
```

```
80000
50000
```

Then within IT:

```
```

```
90000
70000
```

---

# 8. Very common interview pattern

> "Sort by X ascending and Y descending."

Immediately think:

```
```

```
ORDER BY X ASC, Y DESC;
```

For example:

> Sort products by category alphabetically, and within each category by price highest first.

```
```

```
SELECT product_name, category, price
FROM Products
ORDER BY category ASC,
         price DESC;
```

---

# PART 3 — Sorting by an expression

Your notes also cover sorting by calculated expressions. 

Suppose:

```
```

```
SELECT product_name,
       price,
       price * 1.1 AS new_price
FROM Products
ORDER BY new_price DESC;
```

We're not restricted to:

```
```

```
ORDER BY actual_column
```

We can sort based on a calculated result.

---

# 9. Alias + ORDER BY

This is a very useful combination.

```
```

```
SELECT price * 12 AS annual_cost
FROM Products
ORDER BY annual_cost DESC;
```

The alias gives the calculated column a name, and `ORDER BY` can use that result.

Your notes specifically provide this pattern with `discounted_price`. 

---

# PART 4 — Sorting by position

Your notes also mention this:

```
```

```
SELECT product_name, price
FROM products
ORDER BY 2 DESC, 1 ASC;
```

What does `2` mean?

It means:

```
```

```
SELECT product_name, price
       ↑            ↑
       1            2
```

Therefore:

```
```

```
ORDER BY 2 DESC
```

means:

> Sort by the second selected column → `price DESC`.

And:

```
```

```
ORDER BY 1 ASC
```

means:

> Then sort by the first selected column → `product_name ASC`.

---

# ⚠️ Should you use positional ORDER BY?

You should **understand it**, because interviewers may ask about it.

But in real code, I generally prefer:

```
```

```
ORDER BY price DESC,
         product_name ASC;
```

over:

```
```

```
ORDER BY 2 DESC, 1 ASC;
```

because column names are clearer and don't break conceptually when the `SELECT` list changes.

---

# PART 5 — NULL and ORDER BY

Your notes discuss NULL ordering too. 

Suppose:

| employeebonus |       |
| ------------- | ----- |
| Rahul         | 10000 |
| Aman          | NULL  |
| Priya         | 5000  |

If you do:

```
```

```
ORDER BY bonus ASC;
```

MySQL treats `NULL` as lower than non-NULL values, so it will generally appear first.

Conceptually:

```
```

```
NULL
5000
10000
```

For descending:

```
```

```
ORDER BY bonus DESC;
```

conceptually:

```
```

```
10000
5000
NULL
```

---

# ⚠️ Important source distinction

Your notes mention:

```
```

```
NULLS FIRST
NULLS LAST
```

as ways to control NULL ordering. 

However, **don't blindly memorize that syntax as MySQL syntax**. MySQL's handling differs from databases such as PostgreSQL.

For our interview preparation, we'll focus on **MySQL-compatible techniques** when the issue arises.

That's an important distinction because your goal is specifically **MySQL**.

---

# PART 6 — SQL 50 connection

Now we can connect `ORDER BY` to the problems you already listed.

## #595 — Big Countries

The basic problem is filtering countries based on:

```
```

```
area >= 3,000,000
OR
population >= 25,000,000
```

The core solution is:

```
```

```
SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
```

Notice:

```
```

```
SELECT
FROM
WHERE
```

No `ORDER BY` is required because the problem doesn't ask you to sort.

### Interview lesson

**Don't add clauses just because you know them.**

Use `ORDER BY` only when the question requires an ordering.

---

# #1148 — Article Views I

We previously had:

```
```

```
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

Now we can understand the entire query:

```
```

```
DISTINCT
   ↓
remove duplicate authors

AS
   ↓
rename author_id → id

WHERE
   ↓
author viewed their own article

ORDER BY
   ↓
sort resulting IDs
```

This is a perfect example of multiple concepts working together.

---

# #620 — Not Boring Movies

Now `ORDER BY` becomes directly relevant.

The problem asks for movies satisfying conditions and then requires ordering by `rating` in descending order.

The pattern is:

```
```

```
SELECT *
FROM Cinema
WHERE id % 2 = 1
  AND description <> 'boring'
ORDER BY rating DESC;
```

Look at the structure:

```
```

```
SELECT
  ↓
FROM
  ↓
WHERE
  ↓
ORDER BY
```

This is exactly the progression we're building.

---

# 🔥 Important pattern from #620

Notice:

```
```

```
id % 2 = 1
```

This means:

> ID is odd.

Because `%` is the modulo operator.

So:

```
```

```
5 % 2 = 1
7 % 2 = 1
9 % 2 = 1
```

Those are odd.

And:

```
```

```
description <> 'boring'
```

means:

> Description is not boring.

Then:

```
```

```
ORDER BY rating DESC
```

means:

> Highest rating first.

This one problem combines several things you've already learned.

---

# 🧠 SQL 50 strategy

This is how I want us to study each problem.

Instead of memorizing:

```
```

```
SELECT *
FROM Cinema
WHERE ...
ORDER BY ...;
```

we'll ask:

### Step 1 — What columns?

```
```

```
SELECT
```

### Step 2 — Which table?

```
```

```
FROM
```

### Step 3 — Which rows?

```
```

```
WHERE
```

### Step 4 — How should the result be arranged?

```
```

```
ORDER BY
```

This gives you a repeatable interview process.

---

# 🧩 Our current SQL grammar

You've now built:

```
```

```
SELECT columns
FROM table
WHERE conditions
ORDER BY columns;
```

And the `WHERE` toolbox is:

```
```

```
=  <>  >  <  >=  <=
AND
OR
NOT
IS NULL
IS NOT NULL
LIKE
IN
NOT IN
BETWEEN
```

Plus:

```
```

```
DISTINCT
AS
```

Your notes support this progression and give the general clause order as `SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY`. 

---

# 🎯 Interview rules to memorize

### Rule 1

```
```

```
ORDER BY salary ASC
```

→ smallest to largest.

### Rule 2

```
```

```
ORDER BY salary DESC
```

→ largest to smallest.

### Rule 3

```
```

```
ORDER BY salary
```

→ ascending by default.

### Rule 4

```
```

```
ORDER BY department, salary DESC
```

→ department is the primary sort; salary breaks ties.

### Rule 5

```
```

```
ORDER BY alias
```

can sort using a selected expression's alias.

### Rule 6

`WHERE` **filters**.

`ORDER BY` **sorts**.

Don't confuse their jobs.

---

# 🧪 Your first ORDER BY drill

Before we move to `LIMIT`, I want these to become automatic.

### Q1

Return all employees sorted by salary from highest to lowest.

### Q2

Return employees sorted alphabetically by name.

### Q3

Return employees sorted by department alphabetically, and within each department by salary highest first.

### Q4

Return the three columns `name`, `salary`, and `salary * 12 AS annual_salary`, sorted by annual salary descending.

### Q5

What is the difference between:

```
```

```
ORDER BY salary ASC
```

and

```
```

```
ORDER BY salary DESC
```

### Q6 🔥

What does this do?

```
```

```
SELECT name, department, salary
FROM Employees
ORDER BY department ASC, salary DESC;
```

### Q7 — SQL 50

For **#620 Not Boring Movies**, explain in English what each part of this does:

```
```

```
SELECT *
FROM Cinema
WHERE id % 2 = 1
  AND description <> 'boring'
ORDER BY rating DESC;
```

Don't worry about solving harder problems yet. **Master this layer first.** Then we'll do `LIMIT`, and after that we'll enter the really important **aggregate + GROUP BY** world, where a large chunk of SQL 50 starts becoming much more interesting.

---

PART 7

We have finished:

SELECT
FROM
WHERE
DISTINCT
AS
LIKE
IN
BETWEEN
IS NULL
ORDER BY

The next natural step from your notes is LIMIT, and then we'll move into the major SQL milestone: aggregate functions → GROUP BY → HAVING. Your notes explicitly introduce LIMIT, and then introduce grouping and aggregate functions such as COUNT, SUM, AVG, MAX, and MIN.

🚀 Part 3 — LIMIT
1. What problem does LIMIT solve?

Imagine we have:

Employees

name     salary
---------------
Aman     50000
Rahul    90000
Priya    80000
John     70000
Riya     60000

Question:

Give me only the first 3 rows.

Use:

SELECT *
FROM Employees
LIMIT 3;

Your notes define LIMIT as setting an upper limit on the number of rows returned.

2. ORDER BY + LIMIT = 🚨 very important

This combination is much more useful than LIMIT alone.

Suppose the interviewer asks:

Find the employee with the highest salary.

Think:

highest salary
      ↓
ORDER BY salary DESC
      ↓
only one row
      ↓
LIMIT 1

Therefore:

SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 1;

This pattern should become automatic:

"highest"
     ↓
DESC
     ↓
LIMIT 1
3. Lowest value

Question:

Find the employee with the lowest salary.

SELECT *
FROM Employees
ORDER BY salary ASC
LIMIT 1;

Mental translation:

lowest
  ↓
ASC
  ↓
LIMIT 1
4. Top 3 salaries

Question:

Find the three highest-paid employees.

SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 3;

This is one of the most common beginner/intermediate SQL interview patterns.

5. Top 5 products by price
SELECT product_name, price
FROM Products
ORDER BY price DESC
LIMIT 5;

Notice the order:

SELECT
  ↓
FROM
  ↓
ORDER BY
  ↓
LIMIT
🧠 Critical concept: LIMIT without ORDER BY

Consider:

SELECT *
FROM Employees
LIMIT 3;

This means:

Give me up to 3 rows.

It does not mean:

Give me the 3 highest-paid employees.

For that, you need:

SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 3;
Interview rule

LIMIT controls how many rows; ORDER BY controls which rows appear first.

6. WHERE + ORDER BY + LIMIT

Now combine everything we've learned.

Question:

Find the highest-paid employee in the IT department.

Translate:

IT employee
    ↓
WHERE department = 'IT'

highest salary
    ↓
ORDER BY salary DESC

one employee
    ↓
LIMIT 1

Answer:

SELECT *
FROM Employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 1;

🔥 This is exactly the type of incremental reasoning I want you to develop.

7. DISTINCT + ORDER BY + LIMIT

Question:

Find the three highest distinct salaries.

SELECT DISTINCT salary
FROM Employees
ORDER BY salary DESC
LIMIT 3;

Suppose salaries are:

90000
90000
80000
70000
70000
60000

Result:

90000
80000
70000

This is a very important stepping stone toward Second Highest Salary, which is SQL 50 #176.

🔥 SQL 50 #176 — Second Highest Salary

This is our first really useful connection.

The problem asks:

Find the second highest distinct salary.

Think:

DISTINCT
   ↓
remove duplicate salaries

ORDER BY DESC
   ↓
highest → lowest

LIMIT/OFFSET
   ↓
get second one

A MySQL solution can be:

SELECT (
    SELECT DISTINCT salary
    FROM Employee
    ORDER BY salary DESC
    LIMIT 1 OFFSET 1
) AS SecondHighestSalary;

Don't worry if OFFSET looks new—we'll learn it properly now.

8. OFFSET

Suppose:

SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 3 OFFSET 1;

Think:

OFFSET 1
   ↓
skip first 1 row

LIMIT 3
   ↓
then take 3 rows

If sorted data is:

90000
80000
70000
60000
50000

then:

OFFSET 1

skips:

90000

and:

LIMIT 3

returns:

80000
70000
60000
9. LIMIT offset, count

MySQL also supports:

SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 1, 3;

This means:

1 → offset
3 → number of rows

Equivalent to:

LIMIT 3 OFFSET 1

For learning/interviews, I recommend the clearer form:

LIMIT 3 OFFSET 1

because you can immediately understand which number means what.

10. LIMIT 1 OFFSET 1

This is particularly important.

ORDER BY salary DESC
LIMIT 1 OFFSET 1;

means:

Sort highest → lowest

90000  ← skip
80000  ← take

Therefore:

second highest row

This becomes useful for:

second highest salary
second latest order
second oldest employee
second highest score
🚨 But there's a catch

Suppose:

salary
------
90000
90000
80000
70000

If you do:

ORDER BY salary DESC
LIMIT 1 OFFSET 1;

you get:

90000

That's not the second-highest distinct salary.

That's why #176 is teaching us an important distinction:

second row
      ≠
second distinct value

To get the second distinct salary:

SELECT DISTINCT salary
FROM Employee
ORDER BY salary DESC
LIMIT 1 OFFSET 1;

Result:

80000

🔥 This is an excellent interview concept.

🧠 Our query pipeline so far

You should now mentally see:

FROM
  ↓
WHERE
  ↓
SELECT
  ↓
DISTINCT
  ↓
ORDER BY
  ↓
LIMIT

There is a more precise SQL logical-processing model that we'll discuss later, but for writing queries, this gives you a useful mental structure.

And now we're ready for the biggest conceptual jump.

🚀 Part 4 — Aggregate Functions

Your notes identify these five core aggregate functions:

COUNT()
SUM()
AVG()
MAX()
MIN()

These are fundamentally different from what we've done so far.

Until now we've mostly been asking:

Which rows do I want?

Now we'll start asking:

What can I calculate from these rows?

11. COUNT()

Suppose:

Employees

id
--
1
2
3
4
5

Question:

How many employees are there?

SELECT COUNT(*)
FROM Employees;

Result:

5

COUNT(*) counts rows.

12. COUNT(column)

Now:

Employees

id   email
---------
1    a@gmail.com
2    NULL
3    b@gmail.com
4    c@gmail.com

Compare:

SELECT COUNT(*)
FROM Employees;

with:

SELECT COUNT(email)
FROM Employees;

Results:

COUNT(*)     → 4
COUNT(email) → 3

Why?

Because:

COUNT(*)

counts rows.

While:

COUNT(email)

counts non-NULL values in email.

🔥 This is an extremely common interview question.

13. SUM()

Suppose:

salary
------
50000
60000
70000

Question:

What is the total salary?

SELECT SUM(salary)
FROM Employees;

Result:

180000

Think:

SUM → total
14. AVG()

Question:

What is the average salary?

SELECT AVG(salary)
FROM Employees;

Think:

AVG → average

Your notes explicitly define AVG() as computing the average of numeric values.

15. MAX()

Question:

What is the highest salary?

SELECT MAX(salary)
FROM Employees;

Think:

MAX → largest
16. MIN()

Question:

What is the lowest salary?

SELECT MIN(salary)
FROM Employees;

Think:

MIN → smallest
🧠 The five functions

Memorize this table:

Question	Function
How many?	COUNT()
Total?	SUM()
Average?	AVG()
Highest?	MAX()
Lowest?	MIN()

Your notes list exactly these five as the common aggregate functions.

17. Aggregation without GROUP BY

This is important.

You can simply do:

SELECT AVG(salary)
FROM Employees;

This produces one overall result.

If there are 1,000 employees:

1,000 rows
    ↓
AVG()
    ↓
1 result

Similarly:

SELECT MAX(salary)
FROM Employees;

produces one value.

18. Now the big question: "per department"

Suppose interviewer asks:

Find the average salary for each department.

You cannot just write:

SELECT AVG(salary)
FROM Employees;

because that gives the overall average.

You need:

SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department;

🔥 This is the moment GROUP BY becomes necessary.

Your notes define GROUP BY as grouping rows based on one or more columns, commonly together with aggregate functions.

19. What does GROUP BY actually do?

Suppose:

name	department	salary
Rahul	IT	80000
Priya	IT	60000
Aman	HR	50000
John	HR	70000
Riya	Sales	90000

When we write:

SELECT department, AVG(salary)
FROM Employees
GROUP BY department;

Think:

                 Employees
                     ↓
          ┌──────────┼──────────┐
          ↓          ↓          ↓
         IT          HR        Sales
          ↓          ↓          ↓
       80k,60k     50k,70k      90k
          ↓          ↓          ↓
        AVG        AVG         AVG
          ↓          ↓          ↓
        70k        60k         90k

Result:

department	AVG(salary)
HR	60000
IT	70000
Sales	90000
20. The most important GROUP BY mental model

Whenever you see:

"for each X"

immediately think:

GROUP BY X

Examples:

Average salary for each department

GROUP BY department

Number of students in each class

GROUP BY class

Total sales for each product

GROUP BY product

Number of customers per country

GROUP BY country

🔥 This phrase recognition will make SQL interview questions much easier.

21. COUNT + GROUP BY

Question:

How many employees are in each department?

SELECT department,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department;

Result:

department	employee_count
HR	2
IT	2
Sales	1

This exact pattern becomes extremely important in SQL 50.

22. GROUP BY + ORDER BY

Your notes explicitly show that these can be combined.

Question:

Show departments ordered by employee count, highest first.

SELECT department,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
ORDER BY employee_count DESC;

Now we're combining:

GROUP BY
    ↓
calculate each group
    ↓
ORDER BY
    ↓
rank the groups
23. GROUP BY + ORDER BY + LIMIT

Now we're approaching real interview territory.

Question:

Find the department with the most employees.

SELECT department,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
ORDER BY employee_count DESC
LIMIT 1;

Read it:

group employees by department
        ↓
count each department
        ↓
highest count first
        ↓
take first department

🔥 That's a very powerful pattern.

24. HAVING — the next big concept

Your notes introduce HAVING as a way to filter groups based on aggregate results, analogous to how WHERE filters rows.

Suppose:

Find departments whose average salary is greater than 50,000.

We need:

SELECT department,
       AVG(salary) AS avg_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 50000;
🚨 WHERE vs HAVING

This distinction is essential for interviews.

WHERE

Filters individual rows:

WHERE salary > 50000

Think:

ROW → filter
HAVING

Filters groups:

HAVING AVG(salary) > 50000

Think:

GROUP → filter
Memorize:

WHERE filters rows before grouping.

HAVING filters groups after grouping.

25. Example showing the difference

Question:

Find departments whose employees have an average salary greater than 60,000.

Correct:

SELECT department,
       AVG(salary) AS avg_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 60000;

Incorrect idea:

WHERE AVG(salary) > 60000

Why?

Because AVG(salary) is an aggregate over a group. WHERE operates before that grouping/aggregation step.

🧠 The new SQL structure

We're expanding our grammar:

SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...
LIMIT ...;

Your notes explicitly give the concepts of GROUP BY, aggregate functions, HAVING, and combining GROUP BY with ORDER BY.

This is a huge milestone.

🎯 SQL 50 connection

This next section unlocks a large number of the problems you listed.

For example:

#1729 — Find Followers Count

Concepts:

GROUP BY
COUNT
ORDER BY

The basic pattern is:

SELECT user_id,
       COUNT(*) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;
#596 — Classes With at Least 5 Students

Concepts:

GROUP BY
COUNT
HAVING

Pattern:

SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(*) >= 5;

🔥 This is almost a pure GROUP BY + HAVING problem.

#2356 — Number of Unique Subjects Taught by Each Teacher

Concepts:

GROUP BY
COUNT(DISTINCT ...)

Pattern:

SELECT teacher_id,
       COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id;

Now you can see why we needed DISTINCT before reaching aggregation.

#619 — Biggest Single Number

This introduces another important pattern involving:

GROUP BY
COUNT
HAVING
MAX

We'll solve it carefully once we've mastered the fundamentals.

🧭 Where we are now

You've gone from:

SELECT

to:

SELECT
FROM
WHERE
DISTINCT
LIKE
IN
BETWEEN
IS NULL
AS
ORDER BY
LIMIT

and we're now entering:

             AGGREGATION
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      COUNT      SUM       AVG
        ↓         ↓         ↓
       MAX       MIN
                  │
                  ↓
              GROUP BY
                  │
                  ↓
               HAVING
                  │
                  ↓
              ORDER BY
                  │
                  ↓
               LIMIT

This is the point where SQL starts becoming much more powerful.

🔥 Your next practice set

Before we move into JOIN, I want you to master these.

Q1

Find the total number of employees.

Q2

Find the highest salary.

Q3

Find the average salary.

Q4

Find the number of employees in each department.

Q5

Find the average salary in each department.

Q6

Find departments having more than 5 employees.

Q7

Find the department with the highest average salary.

Q8 🔥

Find the top 3 departments by employee count.

Q9 🔥

What is the difference between:

WHERE salary > 50000

and:

HAVING AVG(salary) > 50000
Q10 — SQL 50

Explain why #596 Classes With at Least 5 Students naturally requires:

GROUP BY
+
COUNT
+
HAVING


---

PART 8
We have finished:

```
```

```
SELECT
FROM
WHERE
DISTINCT
AS
LIKE
IN
BETWEEN
IS NULL
ORDER BY
```

The next natural step from your notes is **`LIMIT`**, and then we'll move into the major SQL milestone: **aggregate functions →** **`GROUP BY`** **→** **`HAVING`**. Your notes explicitly introduce `LIMIT`, and then introduce grouping and aggregate functions such as `COUNT`, `SUM`, `AVG`, `MAX`, and `MIN`.  

# 🚀 Part 3 — `LIMIT`

## 1. What problem does `LIMIT` solve?

Imagine we have:

```
```

```
Employees

name     salary
---------------
Aman     50000
Rahul    90000
Priya    80000
John     70000
Riya     60000
```

Question:

> Give me only the first 3 rows.

Use:

```
```

```
SELECT *
FROM Employees
LIMIT 3;
```

Your notes define `LIMIT` as setting an upper limit on the number of rows returned. 

---

# 2. `ORDER BY` + `LIMIT` = 🚨 very important

This combination is **much more useful** than `LIMIT` alone.

Suppose the interviewer asks:

> Find the employee with the highest salary.

Think:

```
```

```
highest salary
      ↓
ORDER BY salary DESC
      ↓
only one row
      ↓
LIMIT 1
```

Therefore:

```
```

```
SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 1;
```

This pattern should become automatic:

```
```

```
"highest"
     ↓
DESC
     ↓
LIMIT 1
```

---

# 3. Lowest value

Question:

> Find the employee with the lowest salary.

```
```

```
SELECT *
FROM Employees
ORDER BY salary ASC
LIMIT 1;
```

Mental translation:

```
```

```
lowest
  ↓
ASC
  ↓
LIMIT 1
```

---

# 4. Top 3 salaries

Question:

> Find the three highest-paid employees.

```
```

```
SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 3;
```

This is one of the most common beginner/intermediate SQL interview patterns.

---

# 5. Top 5 products by price

```
```

```
SELECT product_name, price
FROM Products
ORDER BY price DESC
LIMIT 5;
```

Notice the order:

```
```

```
SELECT
  ↓
FROM
  ↓
ORDER BY
  ↓
LIMIT
```

---

# 🧠 Critical concept: LIMIT without ORDER BY

Consider:

```
```

```
SELECT *
FROM Employees
LIMIT 3;
```

This means:

> Give me up to 3 rows.

It does **not** mean:

> Give me the 3 highest-paid employees.

For that, you need:

```
```

```
SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 3;
```

### Interview rule

> **`LIMIT`** **controls how many rows;** **`ORDER BY`** **controls which rows appear first.**

---

# 6. `WHERE` + `ORDER BY` + `LIMIT`

Now combine everything we've learned.

Question:

> Find the highest-paid employee in the IT department.

Translate:

```
```

```
IT employee
    ↓
WHERE department = 'IT'

highest salary
    ↓
ORDER BY salary DESC

one employee
    ↓
LIMIT 1
```

Answer:

```
```

```
SELECT *
FROM Employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 1;
```

🔥 This is exactly the type of incremental reasoning I want you to develop.

---

# 7. `DISTINCT` + `ORDER BY` + `LIMIT`

Question:

> Find the three highest distinct salaries.

```
```

```
SELECT DISTINCT salary
FROM Employees
ORDER BY salary DESC
LIMIT 3;
```

Suppose salaries are:

```
```

```
90000
90000
80000
70000
70000
60000
```

Result:

```
```

```
90000
80000
70000
```

This is a very important stepping stone toward **Second Highest Salary**, which is SQL 50 #176.

---

# 🔥 SQL 50 #176 — Second Highest Salary

This is our first really useful connection.

The problem asks:

> Find the second highest **distinct** salary.

Think:

```
```

```
DISTINCT
   ↓
remove duplicate salaries

ORDER BY DESC
   ↓
highest → lowest

LIMIT/OFFSET
   ↓
get second one
```

A MySQL solution can be:

```
```

```
SELECT (
    SELECT DISTINCT salary
    FROM Employee
    ORDER BY salary DESC
    LIMIT 1 OFFSET 1
) AS SecondHighestSalary;
```

Don't worry if `OFFSET` looks new—we'll learn it properly now.

---

# 8. `OFFSET`

Suppose:

```
```

```
SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 3 OFFSET 1;
```

Think:

```
```

```
OFFSET 1
   ↓
skip first 1 row

LIMIT 3
   ↓
then take 3 rows
```

If sorted data is:

```
```

```
90000
80000
70000
60000
50000
```

then:

```
```

```
OFFSET 1
```

skips:

```
```

```
90000
```

and:

```
```

```
LIMIT 3
```

returns:

```
```

```
80000
70000
60000
```

---

# 9. `LIMIT offset, count`

MySQL also supports:

```
```

```
SELECT *
FROM Employees
ORDER BY salary DESC
LIMIT 1, 3;
```

This means:

```
```

```
1 → offset
3 → number of rows
```

Equivalent to:

```
```

```
LIMIT 3 OFFSET 1
```

For learning/interviews, I recommend the clearer form:

```
```

```
LIMIT 3 OFFSET 1
```

because you can immediately understand which number means what.

---

# 10. `LIMIT 1 OFFSET 1`

This is particularly important.

```
```

```
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

means:

```
```

```
Sort highest → lowest

90000  ← skip
80000  ← take
```

Therefore:

> **second highest row**

This becomes useful for:

-  second highest salary 
-  second latest order 
-  second oldest employee 
-  second highest score 

---

# 🚨 But there's a catch

Suppose:

```
```

```
salary
------
90000
90000
80000
70000
```

If you do:

```
```

```
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

you get:

```
```

```
90000
```

That's **not** the second-highest distinct salary.

That's why #176 is teaching us an important distinction:

```
```

```
second row
      ≠
second distinct value
```

To get the second distinct salary:

```
```

```
SELECT DISTINCT salary
FROM Employee
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

Result:

```
```

```
80000
```

🔥 This is an excellent interview concept.

---

# 🧠 Our query pipeline so far

You should now mentally see:

```
```

```
FROM
  ↓
WHERE
  ↓
SELECT
  ↓
DISTINCT
  ↓
ORDER BY
  ↓
LIMIT
```

There is a more precise SQL logical-processing model that we'll discuss later, but for **writing queries**, this gives you a useful mental structure.

And now we're ready for the biggest conceptual jump.

---

# 🚀 Part 4 — Aggregate Functions

Your notes identify these five core aggregate functions: 

```
```

```
COUNT()
SUM()
AVG()
MAX()
MIN()
```

These are fundamentally different from what we've done so far.

Until now we've mostly been asking:

> **Which rows do I want?**

Now we'll start asking:

> **What can I calculate from these rows?**

---

# 11. `COUNT()`

Suppose:

```
```

```
Employees

id
--
1
2
3
4
5
```

Question:

> How many employees are there?

```
```

```
SELECT COUNT(*)
FROM Employees;
```

Result:

```
```

```
5
```

`COUNT(*)` counts rows.

---

# 12. `COUNT(column)`

Now:

```
```

```
Employees

id   email
---------
1    a@gmail.com
2    NULL
3    b@gmail.com
4    c@gmail.com
```

Compare:

```
```

```
SELECT COUNT(*)
FROM Employees;
```

with:

```
```

```
SELECT COUNT(email)
FROM Employees;
```

Results:

```
```

```
COUNT(*)     → 4
COUNT(email) → 3
```

Why?

Because:

```
```

```
COUNT(*)
```

counts rows.

While:

```
```

```
COUNT(email)
```

counts **non-NULL values** in `email`.

🔥 This is an extremely common interview question.

---

# 13. `SUM()`

Suppose:

```
```

```
salary
------
50000
60000
70000
```

Question:

> What is the total salary?

```
```

```
SELECT SUM(salary)
FROM Employees;
```

Result:

```
```

```
180000
```

Think:

```
```

```
SUM → total
```

---

# 14. `AVG()`

Question:

> What is the average salary?

```
```

```
SELECT AVG(salary)
FROM Employees;
```

Think:

```
```

```
AVG → average
```

Your notes explicitly define `AVG()` as computing the average of numeric values. 

---

# 15. `MAX()`

Question:

> What is the highest salary?

```
```

```
SELECT MAX(salary)
FROM Employees;
```

Think:

```
```

```
MAX → largest
```

---

# 16. `MIN()`

Question:

> What is the lowest salary?

```
```

```
SELECT MIN(salary)
FROM Employees;
```

Think:

```
```

```
MIN → smallest
```

---

# 🧠 The five functions

Memorize this table:

| QuestionFunction |           |
| ---------------- | --------- |
| How many?        | `COUNT()` |
| Total?           | `SUM()`   |
| Average?         | `AVG()`   |
| Highest?         | `MAX()`   |
| Lowest?          | `MIN()`   |

Your notes list exactly these five as the common aggregate functions. 

---

# 17. Aggregation without GROUP BY

This is important.

You can simply do:

```
```

```
SELECT AVG(salary)
FROM Employees;
```

This produces **one overall result**.

If there are 1,000 employees:

```
```

```
1,000 rows
    ↓
AVG()
    ↓
1 result
```

Similarly:

```
```

```
SELECT MAX(salary)
FROM Employees;
```

produces one value.

---

# 18. Now the big question: "per department"

Suppose interviewer asks:

> Find the average salary **for each department**.

You cannot just write:

```
```

```
SELECT AVG(salary)
FROM Employees;
```

because that gives the overall average.

You need:

```
```

```
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department;
```

🔥 **This is the moment** **`GROUP BY`** **becomes necessary.**

Your notes define `GROUP BY` as grouping rows based on one or more columns, commonly together with aggregate functions. 

---

# 19. What does GROUP BY actually do?

Suppose:

| namedepartmentsalary |       |       |
| -------------------- | ----- | ----- |
| Rahul                | IT    | 80000 |
| Priya                | IT    | 60000 |
| Aman                 | HR    | 50000 |
| John                 | HR    | 70000 |
| Riya                 | Sales | 90000 |

When we write:

```
```

```
SELECT department, AVG(salary)
FROM Employees
GROUP BY department;
```

Think:

```
```

```
                 Employees
                     ↓
          ┌──────────┼──────────┐
          ↓          ↓          ↓
         IT          HR        Sales
          ↓          ↓          ↓
       80k,60k     50k,70k      90k
          ↓          ↓          ↓
        AVG        AVG         AVG
          ↓          ↓          ↓
        70k        60k         90k
```

Result:

| departmentAVG(salary) |       |
| --------------------- | ----- |
| HR                    | 60000 |
| IT                    | 70000 |
| Sales                 | 90000 |

---

# 20. The most important GROUP BY mental model

Whenever you see:

> **"for each X"**

immediately think:

```
```

```
GROUP BY X
```

Examples:

> Average salary **for each department**

```
```

```
GROUP BY department
```

> Number of students **in each class**

```
```

```
GROUP BY class
```

> Total sales **for each product**

```
```

```
GROUP BY product
```

> Number of customers **per country**

```
```

```
GROUP BY country
```

🔥 This phrase recognition will make SQL interview questions much easier.

---

# 21. `COUNT` + GROUP BY

Question:

> How many employees are in each department?

```
```

```
SELECT department,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department;
```

Result:

| departmentemployee\_count |   |
| ------------------------- | - |
| HR                        | 2 |
| IT                        | 2 |
| Sales                     | 1 |

This exact pattern becomes extremely important in SQL 50.

---

# 22. `GROUP BY` + `ORDER BY`

Your notes explicitly show that these can be combined. 

Question:

> Show departments ordered by employee count, highest first.

```
```

```
SELECT department,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
ORDER BY employee_count DESC;
```

Now we're combining:

```
```

```
GROUP BY
    ↓
calculate each group
    ↓
ORDER BY
    ↓
rank the groups
```

---

# 23. `GROUP BY` + `ORDER BY` + `LIMIT`

Now we're approaching real interview territory.

Question:

> Find the department with the most employees.

```
```

```
SELECT department,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
ORDER BY employee_count DESC
LIMIT 1;
```

Read it:

```
```

```
group employees by department
        ↓
count each department
        ↓
highest count first
        ↓
take first department
```

🔥 That's a very powerful pattern.

---

# 24. `HAVING` — the next big concept

Your notes introduce `HAVING` as a way to filter **groups based on aggregate results**, analogous to how `WHERE` filters rows. 

Suppose:

> Find departments whose average salary is greater than 50,000.

We need:

```
```

```
SELECT department,
       AVG(salary) AS avg_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

# 🚨 WHERE vs HAVING

This distinction is **essential for interviews**.

## WHERE

Filters individual rows:

```
```

```
WHERE salary > 50000
```

Think:

```
```

```
ROW → filter
```

---

## HAVING

Filters groups:

```
```

```
HAVING AVG(salary) > 50000
```

Think:

```
```

```
GROUP → filter
```

### Memorize:

> **WHERE filters rows before grouping.**

> **HAVING filters groups after grouping.**

---

# 25. Example showing the difference

Question:

> Find departments whose employees have an average salary greater than 60,000.

Correct:

```
```

```
SELECT department,
       AVG(salary) AS avg_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Incorrect idea:

```
```

```
WHERE AVG(salary) > 60000
```

Why?

Because `AVG(salary)` is an aggregate over a group. `WHERE` operates before that grouping/aggregation step.

---

# 🧠 The new SQL structure

We're expanding our grammar:

```
```

```
SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...
LIMIT ...;
```

Your notes explicitly give the concepts of `GROUP BY`, aggregate functions, `HAVING`, and combining `GROUP BY` with `ORDER BY`. 

This is a **huge milestone**.

---

# 🎯 SQL 50 connection

This next section unlocks a large number of the problems you listed.

For example:

### #1729 — Find Followers Count

Concepts:

```
```

```
GROUP BY
COUNT
ORDER BY
```

The basic pattern is:

```
```

```
SELECT user_id,
       COUNT(*) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;
```

---

### #596 — Classes With at Least 5 Students

Concepts:

```
```

```
GROUP BY
COUNT
HAVING
```

Pattern:

```
```

```
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(*) >= 5;
```

🔥 This is almost a pure `GROUP BY + HAVING` problem.

---

### #2356 — Number of Unique Subjects Taught by Each Teacher

Concepts:

```
```

```
GROUP BY
COUNT(DISTINCT ...)
```

Pattern:

```
```

```
SELECT teacher_id,
       COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id;
```

Now you can see why we needed `DISTINCT` before reaching aggregation.

---

### #619 — Biggest Single Number

This introduces another important pattern involving:

```
```

```
GROUP BY
COUNT
HAVING
MAX
```

We'll solve it carefully once we've mastered the fundamentals.

---

# 🧭 Where we are now

You've gone from:

```
```

```
SELECT
```

to:

```
```

```
SELECT
FROM
WHERE
DISTINCT
LIKE
IN
BETWEEN
IS NULL
AS
ORDER BY
LIMIT
```

and we're now entering:

```
```

```
             AGGREGATION
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      COUNT      SUM       AVG
        ↓         ↓         ↓
       MAX       MIN
                  │
                  ↓
              GROUP BY
                  │
                  ↓
               HAVING
                  │
                  ↓
              ORDER BY
                  │
                  ↓
               LIMIT
```

This is the point where SQL starts becoming **much more powerful**.

---

# 🔥 Your next practice set

Before we move into `JOIN`, I want you to master these.

### Q1

Find the total number of employees.

### Q2

Find the highest salary.

### Q3

Find the average salary.

### Q4

Find the number of employees in each department.

### Q5

Find the average salary in each department.

### Q6

Find departments having more than 5 employees.

### Q7

Find the department with the highest average salary.

### Q8 🔥

Find the top 3 departments by employee count.

### Q9 🔥

What is the difference between:

```
```

```
WHERE salary > 50000
```

and:

```
```

```
HAVING AVG(salary) > 50000
```

### Q10 — SQL 50

Explain why **#596 Classes With at Least 5 Students** naturally requires:

```
```

```
GROUP BY
+
COUNT
+
HAVING
```


---

PART 9
Absolutely. 🔥 We’re now entering the **most important SQL interview section so far: JOINs**.

Your notes define a join as combining rows from two or more tables based on a related column/common key. They cover `INNER JOIN`, outer joins including `LEFT JOIN`/`RIGHT JOIN`, `CROSS JOIN`, and `SELF JOIN`. 

We'll go **slowly and visually** first. Then we'll attack:

**#1378 → #1581 → #197 → #1661 → #577 → #1280**

---

# 🧠 1. Why do JOINs exist?

So far we've mostly worked with one table:

```
```

```
Employees
```

But real databases don't usually put everything into one giant table.

For example:

### Employees

| employee\_idnamedepartment\_id |       |    |
| ------------------------------ | ----- | -- |
| 1                              | Alice | 10 |
| 2                              | Bob   | 20 |
| 3                              | Carol | 10 |
| 4                              | David | 30 |

### Departments

| department\_iddepartment\_name |             |
| ------------------------------ | ----------- |
| 10                             | Engineering |
| 20                             | HR          |
| 30                             | Finance     |

Now imagine the interviewer asks:

> Give me each employee's name and department name.

`Employees` has:

```
```

```
employee_id
name
department_id
```

`Departments` has:

```
```

```
department_id
department_name
```

The common column is:

```
```

```
department_id
```

So we connect the tables.

That's a **JOIN**.

---

# 2. The fundamental JOIN pattern

```
```

```
SELECT ...
FROM table1
JOIN table2
    ON table1.common_column = table2.common_column;
```

Your notes give this exact structure for an inner join. 

For our example:

```
```

```
SELECT e.name,
       d.department_name
FROM Employees AS e
JOIN Departments AS d
    ON e.department_id = d.department_id;
```

That's it.

But understanding **what happens to the rows** is much more important than memorizing syntax.

---

# 3. Think of JOIN as a matching operation

We have:

```
```

```
Employees                  Departments

Alice → department 10      10 → Engineering
Bob   → department 20      20 → HR
Carol → department 10      30 → Finance
David → department 30
```

JOIN condition:

```
```

```
e.department_id = d.department_id
```

SQL matches:

```
```

```
Alice → 10 → Engineering
Bob   → 20 → HR
Carol → 10 → Engineering
David → 30 → Finance
```

Result:

| namedepartment\_name |             |
| -------------------- | ----------- |
| Alice                | Engineering |
| Bob                  | HR          |
| Carol                | Engineering |
| David                | Finance     |

---

# 🚨 4. `ON` is incredibly important

Don't confuse:

```
```

```
JOIN ...
ON ...
```

with:

```
```

```
WHERE ...
```

### `ON`

Defines **how the tables are related/matched**.

```
```

```
ON e.department_id = d.department_id
```

### `WHERE`

Filters the resulting rows.

```
```

```
WHERE d.department_name = 'Engineering'
```

So:

```
```

```
SELECT e.name,
       d.department_name
FROM Employees e
JOIN Departments d
    ON e.department_id = d.department_id
WHERE d.department_name = 'Engineering';
```

means:

> Join employees with their departments, then keep only Engineering employees.

---

# 5. INNER JOIN

This is our first JOIN type.

Your notes define `INNER JOIN` as returning records where the join condition is satisfied in both tables. 

Think:

```
```

```
LEFT TABLE          RIGHT TABLE

A ──────────────── A     ✅
B ──────────────── B     ✅
C                   X     ❌
```

Only matches survive.

---

# 6. Example with an unmatched row

Employees:

| employee\_idnamedepartment\_id |       |    |
| ------------------------------ | ----- | -- |
| 1                              | Alice | 10 |
| 2                              | Bob   | 20 |
| 3                              | Carol | 40 |

Departments:

| department\_iddepartment\_name |             |
| ------------------------------ | ----------- |
| 10                             | Engineering |
| 20                             | HR          |
| 30                             | Finance     |

Notice:

```
```

```
Carol → department 40
```

but department `40` doesn't exist.

With:

```
```

```
SELECT e.name,
       d.department_name
FROM Employees e
INNER JOIN Departments d
    ON e.department_id = d.department_id;
```

Carol disappears.

Result:

| namedepartment\_name |             |
| -------------------- | ----------- |
| Alice                | Engineering |
| Bob                  | HR          |

That's the defining behavior:

> **INNER JOIN keeps only matching rows.**

---

# 7. `JOIN` vs `INNER JOIN`

In MySQL:

```
```

```
JOIN
```

is commonly used as shorthand for:

```
```

```
INNER JOIN
```

So these are equivalent:

```
```

```
FROM Employees e
INNER JOIN Departments d
ON e.department_id = d.department_id
```

and:

```
```

```
FROM Employees e
JOIN Departments d
ON e.department_id = d.department_id
```

During learning, I'll often write `INNER JOIN` so you can see the join type explicitly.

---

# 8. Now the important one: LEFT JOIN

Your notes define `LEFT JOIN` as returning **all records from the left table**, along with matching records from the right table. 

This is fundamentally different from INNER JOIN.

Think:

```
```

```
LEFT JOIN

LEFT TABLE              RIGHT TABLE

Alice ──────────────── Engineering
Bob   ──────────────── HR
Carol ──────────────── NULL
```

Carol stays.

Why?

Because the **left table is protected**.

---

# 9. LEFT JOIN example

```
```

```
SELECT e.name,
       d.department_name
FROM Employees e
LEFT JOIN Departments d
    ON e.department_id = d.department_id;
```

Result:

| namedepartment\_name |             |
| -------------------- | ----------- |
| Alice                | Engineering |
| Bob                  | HR          |
| Carol                | NULL        |

🔥 That `NULL` is extremely important.

It means:

> There was no matching row in the right table.

---

# 10. INNER vs LEFT JOIN

Memorize this table:

| JOINWhat survives? |                                           |
| ------------------ | ----------------------------------------- |
| `INNER JOIN`       | Only matches                              |
| `LEFT JOIN`        | Everything from left + matches from right |

Visual:

```
```

```
INNER JOIN

LEFT      RIGHT
  ○──────○
     ↓
   matches
```

```
```

```
LEFT JOIN

LEFT      RIGHT
  ○──────○
  ○──────○
  ○
  ↓
all left rows survive
```

---

# 11. This is the key interview question

Interviewer:

> "What's the difference between INNER JOIN and LEFT JOIN?"

Strong answer:

> **INNER JOIN returns only rows having a match in both tables. LEFT JOIN returns every row from the left table and the matching rows from the right table; when there is no match, columns from the right table are NULL.**

That's your interview answer.

---

# 12. Why LEFT JOIN + IS NULL is so powerful

This pattern is going to appear **everywhere**.

Suppose:

### Customers

| customer\_idname |       |
| ---------------- | ----- |
| 1                | Alice |
| 2                | Bob   |
| 3                | Carol |

### Orders

| order\_idcustomer\_id |   |
| --------------------- | - |
| 101                   | 1 |
| 102                   | 2 |

Question:

> Find customers who have never placed an order.

Think:

```
```

```
Customers
   ↓
LEFT JOIN Orders
   ↓
Alice → order
Bob   → order
Carol → NULL
   ↓
WHERE order is NULL
```

SQL:

```
```

```
SELECT c.customer_id,
       c.name
FROM Customers c
LEFT JOIN Orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

Result:

```
```

```
Carol
```

🔥 This pattern is **extremely important**.

---

# 13. Memorize this pattern

When you see:

> Find X who **didn't** have Y.

Think:

```
```

```
FROM X
LEFT JOIN Y
    ON ...
WHERE Y.some_column IS NULL
```

Examples:

> Customers who didn't make transactions

→ `LEFT JOIN` + `IS NULL`

> Employees without departments

→ `LEFT JOIN` + `IS NULL`

> Students who didn't attend exams

→ `LEFT JOIN` + `IS NULL`

This is why **#1581** is coming soon.

---

# 14. SQL 50 #1378 — Replace Employee ID With The Unique Identifier

Now let's apply JOINs immediately.

The problem has two tables conceptually:

### Employees

```
```

```
id
name
```

### EmployeeUNI

```
```

```
id
unique_id
```

We want:

```
```

```
unique_id | name
```

But not every employee necessarily has a corresponding `unique_id`.

What JOIN preserves all employees?

```
```

```
LEFT JOIN
```

So:

```
```

```
SELECT eu.unique_id,
       e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu
    ON e.id = eu.id;
```

### Why LEFT JOIN?

Because the question wants employees even when they don't have a unique ID.

If an employee has no match:

```
```

```
unique_id = NULL
```

That's exactly the behavior we just learned.

---

# 15. #1378 interview thought process

Don't memorize the query.

Think:

```
```

```
Need employee names
        ↓
Employees is main table
        ↓
Need unique ID
        ↓
EmployeeUNI
        ↓
Match using id
        ↓
Must preserve employees
        ↓
LEFT JOIN
```

This is the type of reasoning we're building.

---

# 16. SQL 50 #1581 — Customer Who Visited but Did Not Make Any Transactions

This is **the perfect LEFT JOIN problem**.

Tables:

### Visits

```
```

```
visit_id
customer_id
```

### Transactions

```
```

```
transaction_id
visit_id
```

Question:

> Find customers who visited but didn't make any transactions.

Translate:

```
```

```
Visits
  ↓
LEFT JOIN Transactions
  ↓
keep visits without matching transaction
  ↓
IS NULL
```

Query:

```
```

```
SELECT v.customer_id,
       COUNT(*) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t
    ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

🔥 Look at how many concepts are now coming together:

```
```

```
LEFT JOIN
+
ON
+
IS NULL
+
WHERE
+
GROUP BY
+
COUNT
```

This is exactly why we learned these concepts in sequence.

---

# 17. Why `COUNT(*)` works here

Suppose:

```
```

```
customer_id = 1
```

has two visits without transactions.

After:

```
```

```
LEFT JOIN
```

we get:

```
```

```
1 | NULL
1 | NULL
```

Then:

```
```

```
WHERE t.transaction_id IS NULL
```

keeps both.

Then:

```
```

```
GROUP BY customer_id
```

creates:

```
```

```
customer 1 → 2 rows
```

Then:

```
```

```
COUNT(*)
```

gives:

```
```

```
2
```

---

# 18. SQL 50 #197 — Rising Temperature

This is where JOINs get more interesting.

The table is essentially:

```
```

```
Weather

id
recordDate
temperature
```

Question:

> Find dates where today's temperature is higher than the previous day.

The previous day is **another row in the same table**.

This means:

```
```

```
Weather
   ↕
Weather
```

That's a **SELF JOIN**.

Your notes specifically describe self joins as treating one table as if it were two separate tables using aliases. 

---

# 19. SELF JOIN

Imagine:

```
```

```
Weather w1
Weather w2
```

They're actually the same table.

But SQL sees them as two references.

```
```

```
SELECT ...
FROM Weather w1
JOIN Weather w2
    ON ...
```

Now we can compare:

```
```

```
w1 = today's row
w2 = yesterday's row
```

---

# 20. #197 solution

```
```

```
SELECT w1.id
FROM Weather w1
JOIN Weather w2
    ON DATEDIFF(w1.recordDate, w2.recordDate) = 1
WHERE w1.temperature > w2.temperature;
```

Read it in English:

> Take one Weather row as today's row (`w1`), find another Weather row (`w2`) exactly one day before it, and keep today's row if its temperature is higher.

🔥 That's a genuine interview-level SQL thought process.

---

# 21. Why aliases are essential here

Without aliases:

```
```

```
Weather
Weather
```

would be ambiguous.

We need:

```
```

```
Weather w1
Weather w2
```

so we can say:

```
```

```
w1.temperature
```

versus:

```
```

```
w2.temperature
```

Your notes demonstrate exactly this technique with employee-manager relationships. 

---

# 22. SQL 50 #1661 — Average Time of Process per Machine

This one combines:

```
```

```
JOIN
GROUP BY
AVG
```

The table contains process events such as:

```
```

```
machine_id
process_id
activity_type
timestamp
```

There are two rows per process:

```
```

```
start
end
```

We need:

```
```

```
end_time - start_time
```

and then average the processing times per machine.

The important pattern is:

```
```

```
SELECT machine_id,
       AVG(end_timestamp - start_timestamp)
FROM ...
GROUP BY machine_id;
```

The exact implementation requires matching the start and end activity rows, which is another self-join pattern.

We'll solve it carefully when we drill #1661.

---

# 23. SQL 50 #577 — Employee Bonus

This is another **LEFT JOIN** problem.

Conceptually:

### Employee

```
```

```
empId
name
```

### Bonus

```
```

```
empId
bonus
```

Question:

> Find employees whose bonus is less than 1000 or who don't have a bonus.

Think:

```
```

```
Employee
   ↓
LEFT JOIN Bonus
   ↓
bonus < 1000
OR
bonus IS NULL
```

Pattern:

```
```

```
SELECT e.name,
       b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus < 1000
   OR b.bonus IS NULL;
```

Again:

```
```

```
LEFT JOIN
+
NULL
```

---

# 24. SQL 50 #1280 — Students and Examinations

This is a fantastic problem because it combines multiple concepts.

We have:

```
```

```
Students
Subjects
Examinations
```

The question asks us to report the number of exams each student attended for each subject.

The important insight is:

> We need **every student × every subject combination**, even if the student took zero exams.

That means we first need:

```
```

```
Students
   ×
Subjects
```

That's a **CROSS JOIN**.

Your notes define `CROSS JOIN` as producing every possible combination of rows from the two tables. 

Then:

```
```

```
Students × Subjects
        ↓
LEFT JOIN Examinations
        ↓
COUNT
        ↓
GROUP BY
```

🔥 This is an excellent progression problem.

---

# 25. The JOIN map you should memorize

```
```

```
                    JOIN
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    INNER          LEFT         SELF
       │             │             │
       ↓             ↓             ↓
  only matches   all left      same table
                 + matches     twice
                     │
                     ↓
                  NULL
                     │
                     ↓
                 IS NULL
```

And then:

```
```

```
CROSS JOIN
    ↓
every possible combination
```

Your notes cover these join types and their behavior.  

---

# 🚨 The most important JOIN interview patterns

## Pattern 1 — Only matching records

```
```

```
SELECT ...
FROM A
INNER JOIN B
    ON A.id = B.id;
```

Use when:

> "Find records that exist in both..."

---

## Pattern 2 — Everything from A

```
```

```
SELECT ...
FROM A
LEFT JOIN B
    ON A.id = B.id;
```

Use when:

> "Show all A, even if B doesn't exist."

---

## Pattern 3 — Find missing matches

```
```

```
SELECT ...
FROM A
LEFT JOIN B
    ON A.id = B.id
WHERE B.id IS NULL;
```

Use when:

> "Find A that doesn't have B."

🔥 Memorize this.

---

## Pattern 4 — Same table compared with itself

```
```

```
SELECT ...
FROM A x
JOIN A y
    ON ...;
```

Use when:

> "Compare one row with another row in the same table."

Examples:

-  employee → manager 
-  today's weather → yesterday's weather 
-  start event → end event 

---

## Pattern 5 — Every combination

```
```

```
SELECT ...
FROM A
CROSS JOIN B;
```

Use when:

> "Every possible combination of A and B."

---

# 🧠 Your JOIN decision tree

When an interviewer gives you a JOIN problem, ask:

### Question 1

> Am I using two different tables?

If yes:

```
```

```
JOIN
```

### Question 2

> Do I want only matching rows?

```
```

```
INNER JOIN
```

### Question 3

> Do I want ALL rows from my main table?

```
```

```
LEFT JOIN
```

### Question 4

> Do I specifically want records with no match?

```
```

```
LEFT JOIN
+
IS NULL
```

### Question 5

> Am I comparing rows within the same table?

```
```

```
SELF JOIN
```

### Question 6

> Do I need every possible combination?

```
```

```
CROSS JOIN
```

---

# 🎯 Now your SQL 50 JOIN roadmap

We're going to solve them **in this exact order**:

| ProblemMain concept |                                     |
| ------------------- | ----------------------------------- |
| **#1378**           | `LEFT JOIN`                         |
| **#1581**           | `LEFT JOIN + IS NULL + GROUP BY`    |
| **#197**            | `SELF JOIN + DATEDIFF`              |
| **#1661**           | `SELF JOIN + AVG + GROUP BY`        |
| **#577**            | `LEFT JOIN + NULL`                  |
| **#1280**           | `CROSS JOIN + LEFT JOIN + GROUP BY` |

This is a very deliberate progression: **simple join → missing rows → same-table comparison → aggregation after join → Cartesian product**.

---

# 🧪 Before we solve them

Don't memorize the six queries yet.

I want you to be able to answer these **without SQL first**:

### Q1

You have `Employees` and `Departments`. You want **only employees whose department exists**.

Which JOIN?

### Q2

You want **all employees**, including employees whose department doesn't exist.

Which JOIN?

### Q3

You want employees **without a department**.

Which JOIN + condition?

### Q4

You need to compare today's weather with yesterday's weather.

What kind of JOIN?

### Q5

You need every possible `Student × Subject` combination.

What JOIN?

### Q6 🔥

Explain in plain English what this does:

```
```

```
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus IS NULL;
```

If these six become intuitive, you've crossed a **major SQL interview milestone**. Then we'll solve **#1378 → #1581 → #197 → #1661 → #577 → #1280 line-by-line**, including why each wrong-looking alternative fails.

---

PART 10

Absolutely. 🔥 We’re now entering the **most important SQL interview section so far: JOINs**.

Your notes define a join as combining rows from two or more tables based on a related column/common key. They cover `INNER JOIN`, outer joins including `LEFT JOIN`/`RIGHT JOIN`, `CROSS JOIN`, and `SELF JOIN`. 

We'll go **slowly and visually** first. Then we'll attack:

**#1378 → #1581 → #197 → #1661 → #577 → #1280**

---

# 🧠 1. Why do JOINs exist?

So far we've mostly worked with one table:

```
```

```
Employees
```

But real databases don't usually put everything into one giant table.

For example:

### Employees

| employee\_idnamedepartment\_id |       |    |
| ------------------------------ | ----- | -- |
| 1                              | Alice | 10 |
| 2                              | Bob   | 20 |
| 3                              | Carol | 10 |
| 4                              | David | 30 |

### Departments

| department\_iddepartment\_name |             |
| ------------------------------ | ----------- |
| 10                             | Engineering |
| 20                             | HR          |
| 30                             | Finance     |

Now imagine the interviewer asks:

> Give me each employee's name and department name.

`Employees` has:

```
```

```
employee_id
name
department_id
```

`Departments` has:

```
```

```
department_id
department_name
```

The common column is:

```
```

```
department_id
```

So we connect the tables.

That's a **JOIN**.

---

# 2. The fundamental JOIN pattern

```
```

```
SELECT ...
FROM table1
JOIN table2
    ON table1.common_column = table2.common_column;
```

Your notes give this exact structure for an inner join. 

For our example:

```
```

```
SELECT e.name,
       d.department_name
FROM Employees AS e
JOIN Departments AS d
    ON e.department_id = d.department_id;
```

That's it.

But understanding **what happens to the rows** is much more important than memorizing syntax.

---

# 3. Think of JOIN as a matching operation

We have:

```
```

```
Employees                  Departments

Alice → department 10      10 → Engineering
Bob   → department 20      20 → HR
Carol → department 10      30 → Finance
David → department 30
```

JOIN condition:

```
```

```
e.department_id = d.department_id
```

SQL matches:

```
```

```
Alice → 10 → Engineering
Bob   → 20 → HR
Carol → 10 → Engineering
David → 30 → Finance
```

Result:

| namedepartment\_name |             |
| -------------------- | ----------- |
| Alice                | Engineering |
| Bob                  | HR          |
| Carol                | Engineering |
| David                | Finance     |

---

# 🚨 4. `ON` is incredibly important

Don't confuse:

```
```

```
JOIN ...
ON ...
```

with:

```
```

```
WHERE ...
```

### `ON`

Defines **how the tables are related/matched**.

```
```

```
ON e.department_id = d.department_id
```

### `WHERE`

Filters the resulting rows.

```
```

```
WHERE d.department_name = 'Engineering'
```

So:

```
```

```
SELECT e.name,
       d.department_name
FROM Employees e
JOIN Departments d
    ON e.department_id = d.department_id
WHERE d.department_name = 'Engineering';
```

means:

> Join employees with their departments, then keep only Engineering employees.

---

# 5. INNER JOIN

This is our first JOIN type.

Your notes define `INNER JOIN` as returning records where the join condition is satisfied in both tables. 

Think:

```
```

```
LEFT TABLE          RIGHT TABLE

A ──────────────── A     ✅
B ──────────────── B     ✅
C                   X     ❌
```

Only matches survive.

---

# 6. Example with an unmatched row

Employees:

| employee\_idnamedepartment\_id |       |    |
| ------------------------------ | ----- | -- |
| 1                              | Alice | 10 |
| 2                              | Bob   | 20 |
| 3                              | Carol | 40 |

Departments:

| department\_iddepartment\_name |             |
| ------------------------------ | ----------- |
| 10                             | Engineering |
| 20                             | HR          |
| 30                             | Finance     |

Notice:

```
```

```
Carol → department 40
```

but department `40` doesn't exist.

With:

```
```

```
SELECT e.name,
       d.department_name
FROM Employees e
INNER JOIN Departments d
    ON e.department_id = d.department_id;
```

Carol disappears.

Result:

| namedepartment\_name |             |
| -------------------- | ----------- |
| Alice                | Engineering |
| Bob                  | HR          |

That's the defining behavior:

> **INNER JOIN keeps only matching rows.**

---

# 7. `JOIN` vs `INNER JOIN`

In MySQL:

```
```

```
JOIN
```

is commonly used as shorthand for:

```
```

```
INNER JOIN
```

So these are equivalent:

```
```

```
FROM Employees e
INNER JOIN Departments d
ON e.department_id = d.department_id
```

and:

```
```

```
FROM Employees e
JOIN Departments d
ON e.department_id = d.department_id
```

During learning, I'll often write `INNER JOIN` so you can see the join type explicitly.

---

# 8. Now the important one: LEFT JOIN

Your notes define `LEFT JOIN` as returning **all records from the left table**, along with matching records from the right table. 

This is fundamentally different from INNER JOIN.

Think:

```
```

```
LEFT JOIN

LEFT TABLE              RIGHT TABLE

Alice ──────────────── Engineering
Bob   ──────────────── HR
Carol ──────────────── NULL
```

Carol stays.

Why?

Because the **left table is protected**.

---

# 9. LEFT JOIN example

```
```

```
SELECT e.name,
       d.department_name
FROM Employees e
LEFT JOIN Departments d
    ON e.department_id = d.department_id;
```

Result:

| namedepartment\_name |             |
| -------------------- | ----------- |
| Alice                | Engineering |
| Bob                  | HR          |
| Carol                | NULL        |

🔥 That `NULL` is extremely important.

It means:

> There was no matching row in the right table.

---

# 10. INNER vs LEFT JOIN

Memorize this table:

| JOINWhat survives? |                                           |
| ------------------ | ----------------------------------------- |
| `INNER JOIN`       | Only matches                              |
| `LEFT JOIN`        | Everything from left + matches from right |

Visual:

```
```

```
INNER JOIN

LEFT      RIGHT
  ○──────○
     ↓
   matches
```

```
```

```
LEFT JOIN

LEFT      RIGHT
  ○──────○
  ○──────○
  ○
  ↓
all left rows survive
```

---

# 11. This is the key interview question

Interviewer:

> "What's the difference between INNER JOIN and LEFT JOIN?"

Strong answer:

> **INNER JOIN returns only rows having a match in both tables. LEFT JOIN returns every row from the left table and the matching rows from the right table; when there is no match, columns from the right table are NULL.**

That's your interview answer.

---

# 12. Why LEFT JOIN + IS NULL is so powerful

This pattern is going to appear **everywhere**.

Suppose:

### Customers

| customer\_idname |       |
| ---------------- | ----- |
| 1                | Alice |
| 2                | Bob   |
| 3                | Carol |

### Orders

| order\_idcustomer\_id |   |
| --------------------- | - |
| 101                   | 1 |
| 102                   | 2 |

Question:

> Find customers who have never placed an order.

Think:

```
```

```
Customers
   ↓
LEFT JOIN Orders
   ↓
Alice → order
Bob   → order
Carol → NULL
   ↓
WHERE order is NULL
```

SQL:

```
```

```
SELECT c.customer_id,
       c.name
FROM Customers c
LEFT JOIN Orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

Result:

```
```

```
Carol
```

🔥 This pattern is **extremely important**.

---

# 13. Memorize this pattern

When you see:

> Find X who **didn't** have Y.

Think:

```
```

```
FROM X
LEFT JOIN Y
    ON ...
WHERE Y.some_column IS NULL
```

Examples:

> Customers who didn't make transactions

→ `LEFT JOIN` + `IS NULL`

> Employees without departments

→ `LEFT JOIN` + `IS NULL`

> Students who didn't attend exams

→ `LEFT JOIN` + `IS NULL`

This is why **#1581** is coming soon.

---

# 14. SQL 50 #1378 — Replace Employee ID With The Unique Identifier

Now let's apply JOINs immediately.

The problem has two tables conceptually:

### Employees

```
```

```
id
name
```

### EmployeeUNI

```
```

```
id
unique_id
```

We want:

```
```

```
unique_id | name
```

But not every employee necessarily has a corresponding `unique_id`.

What JOIN preserves all employees?

```
```

```
LEFT JOIN
```

So:

```
```

```
SELECT eu.unique_id,
       e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu
    ON e.id = eu.id;
```

### Why LEFT JOIN?

Because the question wants employees even when they don't have a unique ID.

If an employee has no match:

```
```

```
unique_id = NULL
```

That's exactly the behavior we just learned.

---

# 15. #1378 interview thought process

Don't memorize the query.

Think:

```
```

```
Need employee names
        ↓
Employees is main table
        ↓
Need unique ID
        ↓
EmployeeUNI
        ↓
Match using id
        ↓
Must preserve employees
        ↓
LEFT JOIN
```

This is the type of reasoning we're building.

---

# 16. SQL 50 #1581 — Customer Who Visited but Did Not Make Any Transactions

This is **the perfect LEFT JOIN problem**.

Tables:

### Visits

```
```

```
visit_id
customer_id
```

### Transactions

```
```

```
transaction_id
visit_id
```

Question:

> Find customers who visited but didn't make any transactions.

Translate:

```
```

```
Visits
  ↓
LEFT JOIN Transactions
  ↓
keep visits without matching transaction
  ↓
IS NULL
```

Query:

```
```

```
SELECT v.customer_id,
       COUNT(*) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t
    ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

🔥 Look at how many concepts are now coming together:

```
```

```
LEFT JOIN
+
ON
+
IS NULL
+
WHERE
+
GROUP BY
+
COUNT
```

This is exactly why we learned these concepts in sequence.

---

# 17. Why `COUNT(*)` works here

Suppose:

```
```

```
customer_id = 1
```

has two visits without transactions.

After:

```
```

```
LEFT JOIN
```

we get:

```
```

```
1 | NULL
1 | NULL
```

Then:

```
```

```
WHERE t.transaction_id IS NULL
```

keeps both.

Then:

```
```

```
GROUP BY customer_id
```

creates:

```
```

```
customer 1 → 2 rows
```

Then:

```
```

```
COUNT(*)
```

gives:

```
```

```
2
```

---

# 18. SQL 50 #197 — Rising Temperature

This is where JOINs get more interesting.

The table is essentially:

```
```

```
Weather

id
recordDate
temperature
```

Question:

> Find dates where today's temperature is higher than the previous day.

The previous day is **another row in the same table**.

This means:

```
```

```
Weather
   ↕
Weather
```

That's a **SELF JOIN**.

Your notes specifically describe self joins as treating one table as if it were two separate tables using aliases. 

---

# 19. SELF JOIN

Imagine:

```
```

```
Weather w1
Weather w2
```

They're actually the same table.

But SQL sees them as two references.

```
```

```
SELECT ...
FROM Weather w1
JOIN Weather w2
    ON ...
```

Now we can compare:

```
```

```
w1 = today's row
w2 = yesterday's row
```

---

# 20. #197 solution

```
```

```
SELECT w1.id
FROM Weather w1
JOIN Weather w2
    ON DATEDIFF(w1.recordDate, w2.recordDate) = 1
WHERE w1.temperature > w2.temperature;
```

Read it in English:

> Take one Weather row as today's row (`w1`), find another Weather row (`w2`) exactly one day before it, and keep today's row if its temperature is higher.

🔥 That's a genuine interview-level SQL thought process.

---

# 21. Why aliases are essential here

Without aliases:

```
```

```
Weather
Weather
```

would be ambiguous.

We need:

```
```

```
Weather w1
Weather w2
```

so we can say:

```
```

```
w1.temperature
```

versus:

```
```

```
w2.temperature
```

Your notes demonstrate exactly this technique with employee-manager relationships. 

---

# 22. SQL 50 #1661 — Average Time of Process per Machine

This one combines:

```
```

```
JOIN
GROUP BY
AVG
```

The table contains process events such as:

```
```

```
machine_id
process_id
activity_type
timestamp
```

There are two rows per process:

```
```

```
start
end
```

We need:

```
```

```
end_time - start_time
```

and then average the processing times per machine.

The important pattern is:

```
```

```
SELECT machine_id,
       AVG(end_timestamp - start_timestamp)
FROM ...
GROUP BY machine_id;
```

The exact implementation requires matching the start and end activity rows, which is another self-join pattern.

We'll solve it carefully when we drill #1661.

---

# 23. SQL 50 #577 — Employee Bonus

This is another **LEFT JOIN** problem.

Conceptually:

### Employee

```
```

```
empId
name
```

### Bonus

```
```

```
empId
bonus
```

Question:

> Find employees whose bonus is less than 1000 or who don't have a bonus.

Think:

```
```

```
Employee
   ↓
LEFT JOIN Bonus
   ↓
bonus < 1000
OR
bonus IS NULL
```

Pattern:

```
```

```
SELECT e.name,
       b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus < 1000
   OR b.bonus IS NULL;
```

Again:

```
```

```
LEFT JOIN
+
NULL
```

---

# 24. SQL 50 #1280 — Students and Examinations

This is a fantastic problem because it combines multiple concepts.

We have:

```
```

```
Students
Subjects
Examinations
```

The question asks us to report the number of exams each student attended for each subject.

The important insight is:

> We need **every student × every subject combination**, even if the student took zero exams.

That means we first need:

```
```

```
Students
   ×
Subjects
```

That's a **CROSS JOIN**.

Your notes define `CROSS JOIN` as producing every possible combination of rows from the two tables. 

Then:

```
```

```
Students × Subjects
        ↓
LEFT JOIN Examinations
        ↓
COUNT
        ↓
GROUP BY
```

🔥 This is an excellent progression problem.

---

# 25. The JOIN map you should memorize

```
```

```
                    JOIN
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    INNER          LEFT         SELF
       │             │             │
       ↓             ↓             ↓
  only matches   all left      same table
                 + matches     twice
                     │
                     ↓
                  NULL
                     │
                     ↓
                 IS NULL
```

And then:

```
```

```
CROSS JOIN
    ↓
every possible combination
```

Your notes cover these join types and their behavior.  

---

# 🚨 The most important JOIN interview patterns

## Pattern 1 — Only matching records

```
```

```
SELECT ...
FROM A
INNER JOIN B
    ON A.id = B.id;
```

Use when:

> "Find records that exist in both..."

---

## Pattern 2 — Everything from A

```
```

```
SELECT ...
FROM A
LEFT JOIN B
    ON A.id = B.id;
```

Use when:

> "Show all A, even if B doesn't exist."

---

## Pattern 3 — Find missing matches

```
```

```
SELECT ...
FROM A
LEFT JOIN B
    ON A.id = B.id
WHERE B.id IS NULL;
```

Use when:

> "Find A that doesn't have B."

🔥 Memorize this.

---

## Pattern 4 — Same table compared with itself

```
```

```
SELECT ...
FROM A x
JOIN A y
    ON ...;
```

Use when:

> "Compare one row with another row in the same table."

Examples:

-  employee → manager 
-  today's weather → yesterday's weather 
-  start event → end event 

---

## Pattern 5 — Every combination

```
```

```
SELECT ...
FROM A
CROSS JOIN B;
```

Use when:

> "Every possible combination of A and B."

---

# 🧠 Your JOIN decision tree

When an interviewer gives you a JOIN problem, ask:

### Question 1

> Am I using two different tables?

If yes:

```
```

```
JOIN
```

### Question 2

> Do I want only matching rows?

```
```

```
INNER JOIN
```

### Question 3

> Do I want ALL rows from my main table?

```
```

```
LEFT JOIN
```

### Question 4

> Do I specifically want records with no match?

```
```

```
LEFT JOIN
+
IS NULL
```

### Question 5

> Am I comparing rows within the same table?

```
```

```
SELF JOIN
```

### Question 6

> Do I need every possible combination?

```
```

```
CROSS JOIN
```

---

# 🎯 Now your SQL 50 JOIN roadmap

We're going to solve them **in this exact order**:

| ProblemMain concept |                                     |
| ------------------- | ----------------------------------- |
| **#1378**           | `LEFT JOIN`                         |
| **#1581**           | `LEFT JOIN + IS NULL + GROUP BY`    |
| **#197**            | `SELF JOIN + DATEDIFF`              |
| **#1661**           | `SELF JOIN + AVG + GROUP BY`        |
| **#577**            | `LEFT JOIN + NULL`                  |
| **#1280**           | `CROSS JOIN + LEFT JOIN + GROUP BY` |

This is a very deliberate progression: **simple join → missing rows → same-table comparison → aggregation after join → Cartesian product**.

---

# 🧪 Before we solve them

Don't memorize the six queries yet.

I want you to be able to answer these **without SQL first**:

### Q1

You have `Employees` and `Departments`. You want **only employees whose department exists**.

Which JOIN?

### Q2

You want **all employees**, including employees whose department doesn't exist.

Which JOIN?

### Q3

You want employees **without a department**.

Which JOIN + condition?

### Q4

You need to compare today's weather with yesterday's weather.

What kind of JOIN?

### Q5

You need every possible `Student × Subject` combination.

What JOIN?

### Q6 🔥

Explain in plain English what this does:

```
```

```
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus IS NULL;
```

If these six become intuitive, you've crossed a **major SQL interview milestone**. Then we'll solve **#1378 → #1581 → #197 → #1661 → #577 → #1280 line-by-line**, including why each wrong-looking alternative fails.


---
PART 11

Absolutely. This is the point where SQL starts feeling like **problem solving rather than syntax**.

We’ll build this chapter around one central idea:

> **Advanced SQL questions usually hide a smaller query inside the bigger question.**

We'll learn to recognize that hidden query, then connect it to the outer query.

Our roadmap:

```
```

```
Advanced Aggregation
        ↓
HAVING
        ↓
Subqueries
        ↓
IN / EXISTS
        ↓
Correlated subqueries
        ↓
Multi-step interview problems
        ↓
SQL 50 Medium problems
```

Research on text-to-SQL also consistently treats aggregation, `GROUP BY`/`HAVING`, joins, and nested subqueries as key components of complex SQL reasoning.

---

# 1. First: WHERE vs HAVING — permanently settle this

This is one of the most common interview questions.

Suppose:

```
```

```
Employees

name    department    salary
----------------------------
A       IT             80000
B       IT             60000
C       HR             40000
D       HR             50000
E       Sales           90000
```

## `WHERE`

Filters **individual rows**.

```
```

```
SELECT *
FROM Employees
WHERE salary > 50000;
```

Think:

```
```

```
ROWS
 ↓
WHERE
 ↓
remaining rows
```

---

## `HAVING`

Filters **groups**.

```
```

```
SELECT department,
       AVG(salary) AS avg_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

Think:

```
```

```
ROWS
 ↓
GROUP BY
 ↓
GROUPS
 ↓
HAVING
 ↓
remaining groups
```

### Memorize this:

> **WHERE asks: "Which rows?"**
>
> **HAVING asks: "Which groups?"**

---

# 2. Why can't we use WHERE with AVG?

This is wrong:

```
```

```
SELECT department,
       AVG(salary)
FROM Employees
WHERE AVG(salary) > 50000
GROUP BY department;
```

Because when `WHERE` is operating, the group average hasn't been calculated yet.

The correct version:

```
```

```
SELECT department,
       AVG(salary)
FROM Employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

# 3. A powerful interview translation trick

Look for these words.

### "where"

Usually:

```
```

```
WHERE
```

### "for each"

Usually:

```
```

```
GROUP BY
```

### "how many"

Usually:

```
```

```
COUNT()
```

### "total"

Usually:

```
```

```
SUM()
```

### "average"

Usually:

```
```

```
AVG()
```

### "at least N"

Often:

```
```

```
HAVING COUNT(...) >= N
```

### "greater than the average"

🚨 **Potential subquery.**

For example:

> Find employees whose salary is greater than the average salary.

There is a hidden question:

```
```

```
What is the average salary?
```

That becomes a subquery.

---

# 4. What is a subquery?

A **subquery** is simply a query inside another query.

Example:

```
```

```
SELECT *
FROM Employee
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
);
```

Look at the structure:

```
```

```
OUTER QUERY
    │
    │ salary >
    ↓
┌─────────────────────┐
│   INNER QUERY       │
│                     │
│ SELECT AVG(salary)  │
│ FROM Employee       │
└─────────────────────┘
```

The inner query answers:

> What is the average salary?

Then the outer query asks:

> Which employees have salary greater than that?

---

# 5. This is the fundamental subquery mental model

Don't think:

> "Oh no, nested SQL."

Think:

```
```

```
Question A
   ↓
solve A first
   ↓
use A's answer
   ↓
solve Question B
```

For:

> Find employees earning more than average.

Break it down:

### Question A

```
```

```
What is average salary?
```

```
```

```
SELECT AVG(salary)
FROM Employee;
```

### Question B

```
```

```
Who earns more than that?
```

```
```

```
SELECT *
FROM Employee
WHERE salary > average_salary;
```

Combine them:

```
```

```
SELECT *
FROM Employee
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
);
```

🔥 This decomposition is the skill we want.

---

# 6. Scalar subquery

The previous example returns **one value**:

```
```

```
SELECT AVG(salary)
FROM Employee;
```

For example:

```
```

```
65000
```

So we can compare:

```
```

```
WHERE salary > (65000)
```

A subquery that produces one value is commonly called a **scalar subquery**.

---

# 7. Subquery returning multiple rows

Now suppose:

> Find employees who work in departments located in New York.

Imagine:

```
```

```
Departments

department_id    location
-------------------------
10               New York
20               London
30               New York
```

The inner query:

```
```

```
SELECT department_id
FROM Departments
WHERE location = 'New York';
```

returns:

```
```

```
10
30
```

That's **multiple values**.

We can't do:

```
```

```
WHERE department_id = (
    SELECT department_id
    ...
)
```

because the subquery returns multiple rows.

Instead:

```
```

```
WHERE department_id IN (
    SELECT department_id
    FROM Departments
    WHERE location = 'New York'
);
```

---

# 8. `IN` + subquery

This is a huge pattern.

```
```

```
SELECT *
FROM Employee
WHERE department_id IN (
    SELECT department_id
    FROM Departments
    WHERE location = 'New York'
);
```

Think:

```
```

```
Inner query
     ↓
10, 30
     ↓
IN
     ↓
Employee.department_id
     ↓
keep 10 and 30
```

So:

> `IN` is useful when the subquery returns multiple possible values.

---

# 9. `EXISTS`

Another major subquery tool is:

```
```

```
EXISTS
```

`EXISTS` asks:

> Does at least one matching row exist?

Example:

> Find customers who have placed at least one order.

```
```

```
SELECT c.customer_id,
       c.name
FROM Customers c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
);
```

Read it in English:

> For each customer, check whether at least one order exists for that customer.

---

# 10. `EXISTS` vs `IN`

Conceptually:

### `IN`

> Is this value among these values?

```
```

```
WHERE department_id IN (...)
```

### `EXISTS`

> Does a matching row exist?

```
```

```
WHERE EXISTS (...)
```

For interviews, this distinction matters more than memorizing performance claims.

---

# 11. Correlated subquery 🚨

Now we reach a more advanced concept.

Look at:

```
```

```
SELECT e.name,
       e.salary
FROM Employee e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM Employee e2
    WHERE e2.department_id = e.department_id
);
```

Question:

> Find employees earning more than the average salary of **their own department**.

Notice:

```
```

```
e2.department_id = e.department_id
```

The inner query refers to the outer query.

That's a **correlated subquery**.

---

# 12. Understand it row by row

Suppose:

```
```

```
Alice | IT | 80000
Bob   | IT | 60000
Carol | HR | 50000
Dave  | HR | 40000
```

For Alice:

```
```

```
Alice's department = IT

average IT salary
= (80000 + 60000) / 2
= 70000

Alice salary = 80000
```

Therefore:

```
```

```
Alice qualifies.
```

For Bob:

```
```

```
IT average = 70000
Bob = 60000

Bob doesn't qualify.
```

For Carol:

```
```

```
HR average = 45000
Carol = 50000

Carol qualifies.
```

Result:

```
```

```
Alice
Carol
```

---

# 13. Why is it called "correlated"?

Because the inner query depends on the current outer row.

Visualize:

```
```

```
Outer employee Alice
        ↓
inner query calculates IT average

Outer employee Bob
        ↓
inner query calculates IT average

Outer employee Carol
        ↓
inner query calculates HR average
```

The inner query is **correlated with the outer query**.

---

# 14. Compare normal vs correlated subquery

## Non-correlated

```
```

```
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
)
```

The inner query doesn't care which employee the outer query is currently examining.

It calculates:

```
```

```
one global average
```

---

## Correlated

```
```

```
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM Employee e2
    WHERE e2.department_id = e.department_id
)
```

The inner query depends on:

```
```

```
current employee's department
```

So it calculates:

```
```

```
department-specific average
```

---

# 15. This gives us a powerful interview distinction

### Question:

> Salary greater than company average?

Use:

```
```

```
non-correlated subquery
```

### Question:

> Salary greater than department average?

Potentially:

```
```

```
correlated subquery
```

or later, a window function.

---

# 16. SQL 50 #570 — Managers with at Least 5 Direct Reports

Now let's apply aggregation + self-reference.

Suppose:

```
```

```
Employee

id    name       managerId
-------------------------
1     CEO        NULL
2     A          1
3     B          1
4     C          1
5     D          1
6     E          1
```

Question:

> Find managers with at least 5 direct reports.

The hidden question is:

> How many employees report to each manager?

That's:

```
```

```
GROUP BY managerId
COUNT(*)
```

Conceptually:

```
```

```
SELECT managerId,
       COUNT(*) AS reports
FROM Employee
WHERE managerId IS NOT NULL
GROUP BY managerId
HAVING COUNT(*) >= 5;
```

Then we need the manager's name.

So:

```
```

```
SELECT m.name
FROM Employee m
JOIN (
    SELECT managerId
    FROM Employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
    HAVING COUNT(*) >= 5
) x
ON m.id = x.managerId;
```

### 🚨 Important idea

The inner query produces:

```
```

```
manager IDs
```

The outer query converts those IDs into:

```
```

```
manager names
```

This is a **subquery producing a derived result set**.

---

# 17. #1075 — Project Employees I

Question:

> Find the average experience of employees working on each project.

Phrase:

```
```

```
for each project
```

→ `GROUP BY project_id`

Need:

```
```

```
average experience
```

→ `AVG(experience_years)`

We also need employee information from another table.

So:

```
```

```
SELECT p.project_id,
       AVG(e.experience_years) AS average_years
FROM Project p
JOIN Employee e
    ON p.employee_id = e.employee_id
GROUP BY p.project_id;
```

Notice the progression:

```
```

```
JOIN
 ↓
GROUP BY
 ↓
AVG
```

---

# 18. #1633 — Percentage of Users Attended a Contest

Now we encounter a very common interview pattern:

```
```

```
numerator
---------
denominator
```

Question:

> What percentage of users registered for each contest?

Think:

```
```

```
users who attended contest
--------------------------
total users
```

That's:

```
```

```
COUNT(DISTINCT user_id)
```

divided by:

```
```

```
SELECT COUNT(*)
FROM Users
```

So a subquery becomes useful for the denominator.

Conceptually:

```
```

```
SELECT
    contest_id,
    ROUND(
        COUNT(DISTINCT user_id) * 100.0 /
        (SELECT COUNT(*) FROM Users),
        2
    ) AS percentage
FROM Register
GROUP BY contest_id;
```

### Interview pattern

Whenever you see:

> "percentage of X out of all Y"

think:

```
```

```
numerator
---------
total
```

and the total is often a subquery.

---

# 19. #1211 — Queries Quality and Percentage

This one is a beautiful aggregation problem.

Suppose queries have:

```
```

```
query_name
rating
position
```

Quality is:

```
```

```
rating / position
```

Average quality:

```
```

```
AVG(rating / position)
```

Then poor-query percentage is based on:

```
```

```
rating < 3
```

So you're simultaneously calculating:

```
```

```
AVG(...)
```

and:

```
```

```
percentage(...)
```

This introduces a powerful idea:

> **One GROUP BY can produce multiple aggregate metrics.**

For example:

```
```

```
SELECT query_name,
       AVG(rating / position) AS quality,
       AVG(CASE WHEN rating < 3 THEN 1.0 ELSE 0 END) * 100
           AS poor_query_percentage
FROM Queries
GROUP BY query_name;
```

We'll later study `CASE` properly because it becomes extremely important for interview SQL.

---

# 20. #1193 — Monthly Transactions I

Now we're adding **conditional aggregation**.

The problem asks for transaction statistics per month and country.

We need concepts like:

```
```

```
GROUP BY month, country
```

and conditional counts/sums.

For example:

```
```

```
SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END)
```

This means:

> Count only approved transactions.

This is the beginning of a very important interview technique:

# Conditional aggregation

---

# 21. Conditional aggregation

Suppose:

```
```

```
Transactions

country   state
---------------
US        approved
US        declined
US        approved
UK        approved
```

Question:

> How many approved transactions per country?

Instead of filtering rows away with:

```
```

```
WHERE state = 'approved'
```

we can calculate conditionally:

```
```

```
SELECT country,
       SUM(
           CASE
               WHEN state = 'approved' THEN 1
               ELSE 0
           END
       ) AS approved_count
FROM Transactions
GROUP BY country;
```

Why is this powerful?

Because you can calculate:

```
```

```
approved
declined
total
percentage
```

all in the **same grouped result**.

---

# 22. #1174 — Immediate Food Delivery II

This introduces another important interview pattern:

> Find the percentage of customers whose first order was delivered immediately.

The hidden problem is:

```
```

```
What is each customer's first order?
```

That's an aggregation problem:

```
```

```
MIN(order_date)
```

grouped by customer.

Conceptually:

```
```

```
SELECT customer_id,
       MIN(order_date)
FROM Delivery
GROUP BY customer_id;
```

Then compare that first order's date with the preferred delivery date.

This is exactly the kind of problem where we build:

```
```

```
Step 1 → find first row/value
Step 2 → attach additional information
Step 3 → calculate percentage
```

---

# 23. #550 — Game Play Analysis IV

This is another **"first event"** problem.

Question conceptually:

> What percentage of players returned the day after their first login?

Break it apart.

### Step 1

Find each player's first login:

```
```

```
SELECT player_id,
       MIN(event_date) AS first_date
FROM Activity
GROUP BY player_id;
```

### Step 2

Check whether the player has activity on:

```
```

```
first_date + 1 day
```

### Step 3

Calculate:

```
```

```
players who returned next day
-----------------------------
total players
```

🔥 Notice how we're beginning to recognize the hidden structure instead of immediately writing SQL.

---

# 24. #1070 — Product Sales Analysis III

Question:

> Find products that were sold in their first year.

Hidden question:

> What is each product's first year?

That's:

```
```

```
MIN(year)
```

per product.

Then we need to retrieve sales corresponding to that year.

This can be approached using a subquery/aggregation pattern:

```
```

```
product
   ↓
MIN(year)
   ↓
first year
   ↓
match original rows
```

Again:

> **Find the important value first, then use it to filter the original data.**

That pattern is everywhere.

---

# 25. #1045 — Customers Who Bought All Products

This is a fantastic interview problem.

Question:

> Find customers who bought **every product**.

Suppose there are:

```
```

```
3 products total
```

Customer purchases:

```
```

```
Alice → Product A
Alice → Product B
Alice → Product C

Bob → Product A
Bob → Product B
```

We need Alice.

Think:

```
```

```
How many distinct products did Alice buy?
```

```
```

```
COUNT(DISTINCT product_key)
```

And:

```
```

```
How many products exist?
```

```
```

```
SELECT COUNT(*)
FROM Product
```

Then compare:

```
```

```
customer's distinct product count
=
total product count
```

A clean solution:

```
```

```
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (
    SELECT COUNT(*)
    FROM Product
);
```

🔥 This is one of the most important subquery patterns in the SQL 50.

---

# 26. The hidden structure of #1045

Don't memorize the query.

Translate:

> "Bought all products"

into:

```
```

```
For each customer:
        ↓
count distinct products purchased
        ↓
compare with total number of products
```

Which becomes:

```
```

```
GROUP BY customer
        +
COUNT(DISTINCT product)
        +
HAVING
        +
subquery COUNT(products)
```

That's the real skill.

---

# 🧠 The Medium SQL pattern library

At this point, start recognizing these phrases.

| Interview wordingLikely SQL |                                |
| --------------------------- | ------------------------------ |
| "for each..."               | `GROUP BY`                     |
| "at least N"                | `HAVING ... >= N`              |
| "more than average"         | subquery with `AVG()`          |
| "all products"              | `COUNT(DISTINCT ...)` vs total |
| "first order"               | `MIN(date)`                    |
| "latest order"              | `MAX(date)`                    |
| "percentage"                | numerator / denominator        |
| "conditional count"         | `SUM(CASE WHEN...)`            |
| "doesn't have"              | `LEFT JOIN ... IS NULL`        |
| "same table"                | self join                      |
| "every combination"         | `CROSS JOIN`                   |

This is the point where you should stop seeing SQL as individual commands.

Start seeing it as **patterns**.

---

# 🔥 One extremely important progression

Look at how far we've come:

### Beginner

```
```

```
SELECT *
FROM Employee
WHERE salary > 50000;
```

### Aggregation

```
```

```
SELECT department,
       AVG(salary)
FROM Employee
GROUP BY department;
```

### Filter groups

```
```

```
SELECT department,
       AVG(salary)
FROM Employee
GROUP BY department
HAVING AVG(salary) > 50000;
```

### Subquery

```
```

```
SELECT *
FROM Employee
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
);
```

### Correlated subquery

```
```

```
SELECT *
FROM Employee e
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM Employee e2
    WHERE e2.department_id = e.department_id
);
```

### Multi-stage query

```
```

```
JOIN
 ↓
GROUP BY
 ↓
aggregate
 ↓
subquery
 ↓
compare
 ↓
HAVING
 ↓
final result
```

🔥 **That is the transition from beginner SQL to interview SQL.**

---

# 🧪 Your challenge before the next chapter

Don't write SQL yet. Just identify the pattern.

### Q1

> Find employees whose salary is greater than the company's average salary.

What kind of subquery?

---

### Q2

> Find employees whose salary is greater than their department's average salary.

What kind of subquery?

---

### Q3

> Find departments with at least 10 employees.

What three SQL concepts?

---

### Q4

> Find customers who bought every product.

What aggregation + subquery idea?

---

### Q5

> Find each customer's first order.

What aggregate?

---

### Q6

> Find the percentage of users who performed an action out of all users.

What mathematical/query structure?

---

### Q7 🔥

Explain this without looking anything up:

```
```

```
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (
    SELECT COUNT(*)
    FROM Product
);
```

If you can explain **Q7 line-by-line in plain English**, you've genuinely understood the core of this chapter.


---
PART 12

Absolutely. 🔥 Now we enter one of the **highest-value SQL interview chapters**:

# `CASE WHEN` + Conditional Aggregation + Date Functions

These three ideas unlock a large portion of SQL 50 because they let you turn a sentence like:

> "For each month and country, calculate total transactions, approved transactions, and their amounts."

into a structured SQL solution.

---

# 1. `CASE WHEN` — SQL's IF/ELSE

The basic structure is:

```
```

```
CASE
    WHEN condition THEN result
    ELSE result
END
```

Think:

```
```

```
IF condition
    THEN this
ELSE
    that
```

Example:

```
```

```
SELECT name,
       salary,
       CASE
           WHEN salary >= 100000 THEN 'High'
           WHEN salary >= 50000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_level
FROM Employee;
```

Result:

| namesalarysalary\_level |        |        |
| ----------------------- | ------ | ------ |
| Alice                   | 120000 | High   |
| Bob                     | 70000  | Medium |
| Carol                   | 30000  | Low    |

---

# 2. `CASE` doesn't filter rows

This distinction is **very important**.

### `WHERE`

Removes rows:

```
```

```
WHERE salary >= 50000
```

### `CASE`

Changes/calculates a value:

```
```

```
CASE
    WHEN salary >= 50000 THEN 'Qualified'
    ELSE 'Not Qualified'
END
```

Think:

```
```

```
WHERE
→ "Should this row survive?"

CASE
→ "What value should this row produce?"
```

---

# 3. Simple CASE vs searched CASE

You'll mostly use **searched CASE** in interview problems.

### Searched CASE

```
```

```
CASE
    WHEN salary > 100000 THEN 'A'
    WHEN salary > 50000 THEN 'B'
    ELSE 'C'
END
```

Conditions can be anything.

---

### Simple CASE

```
```

```
CASE department
    WHEN 'IT' THEN 'Technology'
    WHEN 'HR' THEN 'Human Resources'
    ELSE 'Other'
END
```

Here SQL compares one expression against values.

For LeetCode, **searched CASE** is generally the one you should become extremely comfortable with.

---

# 4. The magic trick: `CASE` + `SUM`

This is one of the most important SQL interview patterns.

Suppose:

| countrystate |          |
| ------------ | -------- |
| US           | approved |
| US           | declined |
| US           | approved |

We want:

> Number of approved transactions.

We can write:

```
```

```
SUM(
    CASE
        WHEN state = 'approved' THEN 1
        ELSE 0
    END
)
```

Let's see what happens.

Original:

```
```

```
approved
declined
approved
```

CASE produces:

```
```

```
1
0
1
```

Then:

```
```

```
SUM(1 + 0 + 1)
= 2
```

Therefore:

```
```

```
SELECT
    SUM(
        CASE
            WHEN state = 'approved' THEN 1
            ELSE 0
        END
    ) AS approved_count
FROM Transactions;
```

🔥 This is **conditional aggregation**.

---

# 5. Why not just use WHERE?

You might ask:

```
```

```
SELECT COUNT(*)
FROM Transactions
WHERE state = 'approved';
```

That works if you only need approved transactions.

But imagine we want:

| countrytotalapproveddeclined |
| ---------------------------- |

Now `WHERE state = 'approved'` destroys the declined rows.

Instead:

```
```

```
SELECT
    country,

    COUNT(*) AS total,

    SUM(
        CASE
            WHEN state = 'approved' THEN 1
            ELSE 0
        END
    ) AS approved,

    SUM(
        CASE
            WHEN state = 'declined' THEN 1
            ELSE 0
        END
    ) AS declined

FROM Transactions
GROUP BY country;
```

One query gives us **multiple metrics**.

That's why conditional aggregation is so powerful.

---

# 6. Another trick: `COUNT(CASE WHEN...)`

You will also see:

```
```

```
COUNT(
    CASE
        WHEN state = 'approved' THEN 1
    END
)
```

Why does this work?

Remember:

```
```

```
COUNT(column)
→ counts non-NULL values
```

The CASE produces:

```
```

```
approved → 1
declined → NULL
approved → 1
```

COUNT ignores NULL:

```
```

```
COUNT(1, NULL, 1) = 2
```

So these two patterns are common:

### Pattern A

```
```

```
SUM(CASE WHEN condition THEN 1 ELSE 0 END)
```

### Pattern B

```
```

```
COUNT(CASE WHEN condition THEN 1 END)
```

For interviews, I recommend becoming very comfortable with **Pattern A** first because it makes the logic visually obvious.

---

# 7. Conditional SUM

`CASE` isn't limited to counting.

Suppose:

> Calculate total approved transaction amount.

```
```

```
SUM(
    CASE
        WHEN state = 'approved' THEN amount
        ELSE 0
    END
)
```

So:

```
```

```
state       amount
------------------
approved      100
declined       50
approved      200
```

CASE:

```
```

```
100
0
200
```

SUM:

```
```

```
300
```

---

# 8. Conditional AVG

You can even conditionally calculate averages.

```
```

```
AVG(
    CASE
        WHEN state = 'approved' THEN amount
    END
)
```

The declined rows produce NULL, and `AVG()` ignores NULL.

---

# 9. Conditional percentage

This pattern is **extremely important**.

Suppose:

> What percentage of transactions are approved?

We need:

```
```

```
approved transactions
--------------------- × 100
total transactions
```

SQL:

```
```

```
100.0 *
SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END)
/
COUNT(*)
```

Why `100.0` instead of `100`?

To make sure we're doing decimal arithmetic rather than accidentally getting integer division in contexts where integer types would truncate.

---

# 10. SQL 50 #1193 — Monthly Transactions I

Now let's attack a real problem.

The question asks for statistics by:

```
```

```
month + country
```

We need:

-  total transaction count 
-  approved transaction count 
-  total amount 
-  approved amount 

This is practically a textbook conditional aggregation problem.

---

## Step 1 — Extract month

The transaction has a date such as:

```
```

```
2019-01-15
```

We need:

```
```

```
2019-01
```

MySQL provides:

```
```

```
DATE_FORMAT(trans_date, '%Y-%m')
```

So:

```
```

```
DATE_FORMAT(trans_date, '%Y-%m') AS month
```

---

## Step 2 — Group

Question says:

> for each month and country

Therefore:

```
```

```
GROUP BY month, country
```

---

## Step 3 — Total transactions

```
```

```
COUNT(*) AS trans_count
```

---

## Step 4 — Approved transactions

```
```

```
SUM(
    CASE
        WHEN state = 'approved' THEN 1
        ELSE 0
    END
) AS approved_count
```

---

## Step 5 — Total amount

```
```

```
SUM(amount) AS trans_total_amount
```

---

## Step 6 — Approved amount

```
```

```
SUM(
    CASE
        WHEN state = 'approved' THEN amount
        ELSE 0
    END
) AS approved_total_amount
```

---

## Full solution

```
```

```
SELECT
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,

    COUNT(*) AS trans_count,

    SUM(
        CASE
            WHEN state = 'approved' THEN 1
            ELSE 0
        END
    ) AS approved_count,

    SUM(amount) AS trans_total_amount,

    SUM(
        CASE
            WHEN state = 'approved' THEN amount
            ELSE 0
        END
    ) AS approved_total_amount

FROM Transactions

GROUP BY
    DATE_FORMAT(trans_date, '%Y-%m'),
    country;
```

---

# 🧠 Recognize the structure

When you see:

> "For each X and Y, calculate several different statistics depending on conditions."

Think:

```
```

```
SELECT
    grouping columns,

    COUNT(...),

    SUM(CASE WHEN ...),

    SUM(CASE WHEN ...)

FROM table

GROUP BY
    grouping columns;
```

This pattern is **everywhere**.

---

# 11. Date functions — the essentials

For SQL interviews, don't try to memorize 50 date functions.

Master these first.

### Extract year

```
```

```
YEAR(order_date)
```

### Extract month number

```
```

```
MONTH(order_date)
```

### Extract day

```
```

```
DAY(order_date)
```

### Extract date portion

```
```

```
DATE(timestamp_column)
```

### Format a date

```
```

```
DATE_FORMAT(date_column, '%Y-%m')
```

### Difference between dates

```
```

```
DATEDIFF(date1, date2)
```

### Add/subtract time

```
```

```
DATE_ADD(date, INTERVAL 1 DAY)
```

```
```

```
DATE_SUB(date, INTERVAL 1 DAY)
```

These will take you very far.

---

# 12. `DATEDIFF`

Suppose:

```
```

```
2024-01-10
2024-01-07
```

Then:

```
```

```
DATEDIFF('2024-01-10', '2024-01-07')
```

returns:

```
```

```
3
```

Important:

```
```

```
DATEDIFF(A, B)
= number of days from B to A
```

It doesn't calculate hours/minutes; it returns the difference in calendar days.

---

# 13. `DATE_ADD`

Suppose:

```
```

```
first_login = 2024-01-10
```

Tomorrow:

```
```

```
DATE_ADD(first_login, INTERVAL 1 DAY)
```

gives:

```
```

```
2024-01-11
```

This becomes extremely useful in **#550 Game Play Analysis IV**.

---

# 14. #550 — Game Play Analysis IV

Question:

> What fraction of players logged in again the day after their first login?

Break it down.

### Part 1

Find each player's first login:

```
```

```
SELECT
    player_id,
    MIN(event_date) AS first_date
FROM Activity
GROUP BY player_id;
```

Suppose:

| player\_idfirst\_date |            |
| --------------------- | ---------- |
| 1                     | 2020-01-01 |
| 2                     | 2020-01-03 |
| 3                     | 2020-01-05 |

Now we ask:

> Did player 1 have activity on 2020-01-02?

> Did player 2 have activity on 2020-01-04?

etc.

---

# 15. The crucial pattern

We can build the first-login result as a derived table:

```
```

```
(
    SELECT
        player_id,
        MIN(event_date) AS first_date
    FROM Activity
    GROUP BY player_id
)
```

Then join back to Activity.

Conceptually:

```
```

```
Activity
   ↓
find first date per player
   ↓
join back to Activity
   ↓
look for first_date + 1 day
   ↓
count players
   ↓
divide by total players
```

This is **multi-stage SQL thinking**.

---

# 16. #1174 — Immediate Food Delivery II

Same underlying idea.

Question:

> For each customer, identify their first order.

That means:

```
```

```
MIN(order_date)
```

Then determine whether that first order was delivered on the customer's preferred date.

So we're again doing:

```
```

```
customer
   ↓
MIN(order_date)
   ↓
identify first order
   ↓
CASE WHEN immediate
   ↓
percentage
```

This is a recurring pattern:

> **FIRST/LATEST event problems = MIN/MAX + another step.**

---

# 17. #1321 — Restaurant Growth

This problem introduces another major date concept:

> rolling / consecutive time periods.

Instead of looking at a single day, we may need:

```
```

```
current day
+
previous 6 days
```

That leads toward **window functions**, which we'll learn later.

But before window functions, understand the underlying problem:

```
```

```
date
↓
aggregate revenue for date
↓
combine nearby dates
↓
calculate average
```

The important lesson is that **date-based grouping isn't always just** **`GROUP BY YEAR/MONTH`**.

Sometimes the question is about:

```
```

```
first day
previous day
next day
last 7 days
same month
same year
```

These require different date strategies.

---

# 18. #585 — Investments in 2016

This problem is particularly valuable because it combines:

```
```

```
aggregation
+
conditions
+
uniqueness
```

The idea is roughly:

> Find investments in 2016 where the investment value is shared by multiple people, while the location is unique.

This is a classic:

> **"Find values occurring multiple times / exactly once."**

pattern.

You may use:

```
```

```
COUNT(...)
```

with grouping or subqueries.

For example, conceptually:

```
```

```
tiv_2015
↓
must occur multiple times

location
↓
must occur exactly once
```

So you need to think separately about the two constraints.

That's an important interview habit:

> Don't treat a long English sentence as one condition. Break it into independent logical requirements.

---

# 19. #185 — Department Top Three Salaries

🚨 This is where things become significantly harder.

Question:

> Find employees who are among the top three **unique salaries** in each department.

Notice two hidden requirements:

### Requirement 1

**Within each department**

```
```

```
GROUP/PARTITION BY department
```

### Requirement 2

**Top three unique salaries**

Not simply:

```
```

```
ORDER BY salary DESC
LIMIT 3
```

because `LIMIT` would apply to the entire result rather than independently within every department.

And duplicate salaries matter.

Example:

```
```

```
IT:
100k
100k
90k
80k
70k
```

Top three unique salaries:

```
```

```
100k
90k
80k
```

Not:

```
```

```
100k
100k
90k
```

This problem is the perfect motivation for our next major chapter:

# Window Functions

Especially:

```
```

```
DENSE_RANK()
```

We'll get there.

---

# 20. The mental model you should now have

Let's connect everything.

Suppose an interviewer says:

> "For each country and month, calculate total transactions, approved transactions, total amount, approved amount."

Your brain should immediately produce:

```
```

```
"For each"
      ↓
GROUP BY

"month"
      ↓
DATE_FORMAT

"total transactions"
      ↓
COUNT(*)

"approved transactions"
      ↓
SUM(CASE WHEN...)

"total amount"
      ↓
SUM(amount)

"approved amount"
      ↓
SUM(CASE WHEN...)
```

That is **SQL translation skill**.

---

# 21. Another interview translation example

> "Find the percentage of players who logged in the day after their first login."

Your brain:

```
```

```
"first login"
      ↓
MIN(date)

"day after"
      ↓
DATE_ADD(date, INTERVAL 1 DAY)

"did they login?"
      ↓
JOIN / EXISTS

"percentage"
      ↓
qualifying / total
```

This is exactly how I want you to approach SQL 50.

Not:

> "What syntax do I remember?"

Instead:

> **"What operations does the English sentence imply?"**

---

# 🔥 Your current SQL toolkit

You now have:

```
```

```
SELECT
FROM
WHERE
DISTINCT
LIKE
IN
BETWEEN
IS NULL
AS
ORDER BY

JOIN
LEFT JOIN
SELF JOIN
CROSS JOIN

GROUP BY
COUNT
SUM
AVG
MIN
MAX

HAVING

Subqueries
IN subqueries
EXISTS
Correlated subqueries

CASE WHEN
Conditional aggregation

YEAR
MONTH
DAY
DATE
DATE_FORMAT
DATEDIFF
DATE_ADD
DATE_SUB
```

That's already a **serious SQL foundation**.

---

# 🎯 Mini interview drill

Before we move to window functions, try to mentally solve these.

### Q1

What does this produce?

```
```

```
SUM(
    CASE
        WHEN salary >= 50000 THEN 1
        ELSE 0
    END
)
```

---

### Q2

What's the difference between:

```
```

```
COUNT(*)
```

and:

```
```

```
COUNT(
    CASE WHEN state = 'approved' THEN 1 END
)
```

---

### Q3

Translate:

> "Find the number of approved transactions per country."

---

### Q4

Translate:

> "Find the average salary for each department, but only show departments whose average salary exceeds 80,000."

---

### Q5 🔥

Translate:

> "Find customers whose first order was delivered immediately."

Break the English into **at least 3 SQL operations**.

---

### Q6 🔥🔥

Why doesn't this solve #185?

```
```

```
SELECT *
FROM Employee
ORDER BY salary DESC
LIMIT 3;
```

And what does **"top 3 unique salaries per department"** tell you that this query is missing?

---

## Next major chapter

After this, I strongly recommend:

# 🚀 Window Functions

Starting with:

```
```

```
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
```

because they unlock the hardest and most interview-relevant SQL 50 problems:

- **#185 — Department Top Three Salaries** 
- **#1070 — Product Sales Analysis III** 
- **#1204 — Last Person to Fit in the Bus** 
- **#626 — Exchange Seats** 
-  and several of the "first/latest/consecutive" patterns. 

The big conceptual leap will be:

```
```

```
GROUP BY
→ collapses rows into groups

WINDOW FUNCTIONS
→ calculate across related rows WITHOUT collapsing them
```

That distinction is **absolutely fundamental** for interview SQL.


---
PART 13

# 🚀 Next: Window Functions

This is the next major jump in your SQL interview preparation.

The key distinction:

> **`GROUP BY`** **collapses rows. Window functions calculate across rows while keeping the individual rows.**

This single idea unlocks problems like **#185 Department Top Three Salaries**, and later makes many "first/latest/previous/next/top N per group" questions much easier.

---

# 1. Why do we need window functions?

Suppose we have:

| employeedepartmentsalary |    |        |
| ------------------------ | -- | ------ |
| Alice                    | IT | 100000 |
| Bob                      | IT | 80000  |
| Carol                    | IT | 80000  |
| David                    | IT | 60000  |
| Emma                     | HR | 90000  |
| Frank                    | HR | 70000  |

If we do:

```
```

```
SELECT department, MAX(salary)
FROM Employee
GROUP BY department;
```

we get:

| departmentmax\_salary |        |
| --------------------- | ------ |
| IT                    | 100000 |
| HR                    | 90000  |

The individual employee rows are gone.

That's what `GROUP BY` does.

---

# 2. Window functions don't collapse rows

Now:

```
```

```
SELECT
    name,
    department,
    salary,
    MAX(salary) OVER (
        PARTITION BY department
    ) AS department_max
FROM Employee;
```

Result:

| namedepartmentsalarydepartment\_max |    |        |        |
| ----------------------------------- | -- | ------ | ------ |
| Alice                               | IT | 100000 | 100000 |
| Bob                                 | IT | 80000  | 100000 |
| Carol                               | IT | 80000  | 100000 |
| David                               | IT | 60000  | 100000 |
| Emma                                | HR | 90000  | 90000  |
| Frank                               | HR | 70000  | 90000  |

🔥 **Rows remain.**

That's the magic.

---

# 3. The basic window syntax

You'll see:

```
```

```
FUNCTION(...) OVER (
    PARTITION BY ...
    ORDER BY ...
)
```

There are three important pieces.

### Function

For example:

```
```

```
ROW_NUMBER()
```

or:

```
```

```
RANK()
```

or:

```
```

```
SUM(salary)
```

### `PARTITION BY`

Defines the group/window.

```
```

```
PARTITION BY department
```

means:

> Treat each department separately.

### `ORDER BY`

Defines the order inside the window.

```
```

```
ORDER BY salary DESC
```

means:

> Highest salary first.

---

# 4. `ROW_NUMBER()`

Let's rank employees within each department:

```
```

```
SELECT
    name,
    department,
    salary,
    ROW_NUMBER() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS rn
FROM Employee;
```

Result:

| namedeptsalaryrn |    |        |   |
| ---------------- | -- | ------ | - |
| Alice            | IT | 100000 | 1 |
| Bob              | IT | 80000  | 2 |
| Carol            | IT | 80000  | 3 |
| David            | IT | 60000  | 4 |
| Emma             | HR | 90000  | 1 |
| Frank            | HR | 70000  | 2 |

Notice something important:

Bob and Carol have the same salary, but they receive different row numbers.

```
```

```
Bob   → 2
Carol → 3
```

That's exactly what `ROW_NUMBER()` means:

> **Every row gets a unique sequential number.**

---

# 5. `RANK()`

Now:

```
```

```
RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

Result:

| namesalaryrank |        |   |
| -------------- | ------ | - |
| Alice          | 100000 | 1 |
| Bob            | 80000  | 2 |
| Carol          | 80000  | 2 |
| David          | 60000  | 4 |

Bob and Carol tie.

Both receive:

```
```

```
2
```

But notice the next rank:

```
```

```
4
```

There is a gap.

That's the defining behavior of `RANK()`.

---

# 6. `DENSE_RANK()`

Now:

```
```

```
DENSE_RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

Result:

| namesalarydense\_rank |        |   |
| --------------------- | ------ | - |
| Alice                 | 100000 | 1 |
| Bob                   | 80000  | 2 |
| Carol                 | 80000  | 2 |
| David                 | 60000  | 3 |

No gap.

So:

```
```

```
ROW_NUMBER
→ unique number per row

RANK
→ ties share rank, gaps appear

DENSE_RANK
→ ties share rank, no gaps
```

---

# 7. Memorize this table

Suppose salaries are:

```
```

```
100
80
80
60
```

Then:

| salaryROW\_NUMBERRANKDENSE\_RANK |   |   |   |
| -------------------------------- | - | - | - |
| 100                              | 1 | 1 | 1 |
| 80                               | 2 | 2 | 2 |
| 80                               | 3 | 2 | 2 |
| 60                               | 4 | 4 | 3 |

This distinction is **critical** for SQL interviews.

---

# 8. Why #185 needs `DENSE_RANK`

Remember #185:

> Find employees who are among the top three **unique salaries** in each department.

"Unique salaries" is the giveaway.

Suppose:

```
```

```
IT

100000
80000
80000
60000
50000
```

The unique salary levels are:

```
```

```
100000 → 1
80000  → 2
60000  → 3
50000  → 4
```

Therefore:

```
```

```
100000
80000
80000
60000
```

should qualify.

`DENSE_RANK()` gives exactly that:

```
```

```
100000 → 1
80000  → 2
80000  → 2
60000  → 3
50000  → 4
```

So:

```
```

```
DENSE_RANK() OVER (
    PARTITION BY departmentId
    ORDER BY salary DESC
)
```

is the key.

---

# 9. #185 — Department Top Three Salaries

We cannot simply write:

```
```

```
WHERE DENSE_RANK() <= 3
```

in the same query level because window functions are evaluated after `WHERE`.

So we create an intermediate result.

```
```

```
SELECT *
FROM (
    SELECT
        d.name AS Department,
        e.name AS Employee,
        e.salary,
        DENSE_RANK() OVER (
            PARTITION BY e.departmentId
            ORDER BY e.salary DESC
        ) AS salary_rank
    FROM Employee e
    JOIN Department d
        ON e.departmentId = d.id
) ranked
WHERE salary_rank <= 3;
```

🔥 This is a very important pattern:

```
```

```
Original table
      ↓
Window function
      ↓
assign ranks
      ↓
derived table
      ↓
WHERE rank <= 3
```

---

# 10. Why can't we put the filter immediately after SELECT?

This won't work:

```
```

```
SELECT
    name,
    DENSE_RANK() OVER (...) AS r
FROM Employee
WHERE r <= 3;
```

Because `r` is generated by the window calculation, and `WHERE` happens earlier in SQL's logical processing.

So we do:

```
```

```
Query 1:
calculate rank

Query 2:
filter rank
```

This idea will appear repeatedly.

---

# 11. Window functions + `PARTITION BY`

Think of:

```
```

```
PARTITION BY department
```

as:

> "Reset the calculation for every department."

For example:

```
```

```
IT:
100k → rank 1
80k  → rank 2
60k  → rank 3

HR:
90k → rank 1
70k → rank 2
```

The ranking starts from 1 again when we enter HR.

---

# 12. `LAG()` — look at the previous row

Now we introduce another major interview function.

Suppose:

| datetemperature |    |
| --------------- | -- |
| Jan 1           | 10 |
| Jan 2           | 20 |
| Jan 3           | 15 |
| Jan 4           | 25 |

We can write:

```
```

```
SELECT
    date,
    temperature,
    LAG(temperature) OVER (
        ORDER BY date
    ) AS previous_temperature
FROM Weather;
```

Result:

| datetemperatureprevious\_temperature |    |      |
| ------------------------------------ | -- | ---- |
| Jan 1                                | 10 | NULL |
| Jan 2                                | 20 | 10   |
| Jan 3                                | 15 | 20   |
| Jan 4                                | 25 | 15   |

🔥 `LAG()` means:

> Give me a value from a previous row.

---

# 13. `LEAD()`

The opposite:

```
```

```
LEAD(temperature) OVER (
    ORDER BY date
)
```

Result:

| datetemperaturenext\_temperature |    |      |
| -------------------------------- | -- | ---- |
| Jan 1                            | 10 | 20   |
| Jan 2                            | 20 | 15   |
| Jan 3                            | 15 | 25   |
| Jan 4                            | 25 | NULL |

So:

```
```

```
LAG
→ previous

LEAD
→ next
```

---

# 14. Why `LAG()` is powerful

Suppose the interviewer asks:

> Find days where today's temperature is greater than yesterday's.

With a window function:

```
```

```
SELECT *
FROM (
    SELECT
        recordDate,
        temperature,
        LAG(temperature) OVER (
            ORDER BY recordDate
        ) AS previous_temperature
    FROM Weather
) x
WHERE temperature > previous_temperature;
```

That's conceptually much cleaner than a self join.

Notice how #197 can be solved with either:

```
```

```
SELF JOIN
```

or:

```
```

```
LAG()
```

Learning both approaches makes you much stronger.

---

# 15. `LAG()` with a partition

Suppose we have sales:

| employeedatesales |       |     |
| ----------------- | ----- | --- |
| Alice             | Jan 1 | 100 |
| Alice             | Jan 2 | 150 |
| Bob               | Jan 1 | 200 |
| Bob               | Jan 2 | 250 |

We want each employee's previous sale.

```
```

```
LAG(sales) OVER (
    PARTITION BY employee
    ORDER BY date
)
```

Result:

| employeedatesalesprevious |       |     |      |
| ------------------------- | ----- | --- | ---- |
| Alice                     | Jan 1 | 100 | NULL |
| Alice                     | Jan 2 | 150 | 100  |
| Bob                       | Jan 1 | 200 | NULL |
| Bob                       | Jan 2 | 250 | 200  |

Again:

```
```

```
PARTITION BY employee
```

means the calculation resets for every employee.

---

# 16. `ROW_NUMBER()` for first/latest records

This is another interview pattern you should memorize.

Suppose we want:

> The latest order for every customer.

Use:

```
```

```
ROW_NUMBER() OVER (
    PARTITION BY customer_id
    ORDER BY order_date DESC
)
```

Then:

```
```

```
rn = 1
```

means:

> This is the latest order for this customer.

Full pattern:

```
```

```
SELECT *
FROM (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC
        ) AS rn
    FROM Orders o
) x
WHERE rn = 1;
```

---

# 17. First record instead

Change:

```
```

```
ORDER BY order_date DESC
```

to:

```
```

```
ORDER BY order_date ASC
```

Then:

```
```

```
rn = 1
```

means:

> first order.

So:

```
```

```
ASC
→ first

DESC
→ latest
```

This is an incredibly useful interview pattern.

---

# 18. Window aggregate functions

Window functions aren't limited to ranking.

You can do:

```
```

```
SUM(salary) OVER (...)
```

```
```

```
AVG(salary) OVER (...)
```

```
```

```
MIN(salary) OVER (...)
```

```
```

```
MAX(salary) OVER (...)
```

Example:

```
```

```
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM Employee;
```

Result:

| employeedeptsalarydept\_avg |    |      |     |
| --------------------------- | -- | ---- | --- |
| Alice                       | IT | 100k | 80k |
| Bob                         | IT | 80k  | 80k |
| Carol                       | IT | 60k  | 80k |
| Emma                        | HR | 90k  | 80k |
| Frank                       | HR | 70k  | 80k |

Again:

### `GROUP BY`

```
```

```
3 IT rows
      ↓
1 IT result row
```

### Window

```
```

```
3 IT rows
      ↓
3 IT result rows
```

This distinction is fundamental.

---

# 19. Running totals

Suppose:

| datesales |     |
| --------- | --- |
| Jan 1     | 100 |
| Jan 2     | 200 |
| Jan 3     | 150 |

We want:

| datesalesrunning\_total |     |     |
| ----------------------- | --- | --- |
| Jan 1                   | 100 | 100 |
| Jan 2                   | 200 | 300 |
| Jan 3                   | 150 | 450 |

Use:

```
```

```
SELECT
    date,
    sales,
    SUM(sales) OVER (
        ORDER BY date
    ) AS running_total
FROM Sales;
```

This introduces the idea of a **window frame**, which we'll tackle soon.

---

# 20. The five window functions to master

For your SQL interview preparation, make these automatic:

```
```

```
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
```

And then:

```
```

```
SUM() OVER()
AVG() OVER()
MIN() OVER()
MAX() OVER()
```

---

# 🧠 Pattern recognition

When the interviewer says:

### "Top N in each department"

Think:

```
```

```
DENSE_RANK()
PARTITION BY department
ORDER BY salary DESC
```

---

### "First order per customer"

Think:

```
```

```
ROW_NUMBER()
PARTITION BY customer
ORDER BY date ASC
```

---

### "Latest order per customer"

Think:

```
```

```
ROW_NUMBER()
PARTITION BY customer
ORDER BY date DESC
```

---

### "Previous day's value"

Think:

```
```

```
LAG()
ORDER BY date
```

---

### "Next day's value"

Think:

```
```

```
LEAD()
ORDER BY date
```

---

### "Average for each department but retain employee rows"

Think:

```
```

```
AVG() OVER(PARTITION BY department)
```

---

### "Running total"

Think:

```
```

```
SUM() OVER(ORDER BY date)
```

---

# 🔥 Your next SQL 50 connection

Now revisit **#185**.

The English:

> "Top three unique salaries in each department."

Translate:

```
```

```
"each department"
       ↓
PARTITION BY department

"unique salaries"
       ↓
DENSE_RANK

"top three"
       ↓
rank <= 3
```

That's the complete thought process.

Not memorization.

---

# 🎯 Interview drill

Try these **without writing SQL yet**.

### Q1

For:

```
```

```
100
100
90
80
```

What are the results of:

```
```

```
ROW_NUMBER
RANK
DENSE_RANK
```

---

### Q2

What does:

```
```

```
PARTITION BY department
```

actually do?

---

### Q3

What's the difference between:

```
```

```
RANK()
```

and:

```
```

```
DENSE_RANK()
```

---

### Q4

How would you find the **latest order for every customer**?

---

### Q5

How would you find the **first order for every customer**?

---

### Q6 🔥

Explain why this:

```
```

```
AVG(salary) OVER (
    PARTITION BY department
)
```

is fundamentally different from:

```
```

```
AVG(salary)
FROM Employee
GROUP BY department
```

---

### Q7 🔥🔥

Suppose an interviewer asks:

> "For every employee, show their salary and the salary of the employee who joined immediately before them in the same department."

Which window function and which two window clauses would you think of immediately?

---

## Where we're going next

After this, we'll do **window functions properly at interview depth**:

```
```

```
ROW_NUMBER
RANK
DENSE_RANK
        ↓
LAG / LEAD
        ↓
window frames
        ↓
running totals
        ↓
moving averages
        ↓
first/last within groups
        ↓
Top-N per group
        ↓
consecutive rows
```

---

PART 14

# 🚀 Next: Window Functions

This is the next major jump in your SQL interview preparation.

The key distinction:

> **`GROUP BY`** **collapses rows. Window functions calculate across rows while keeping the individual rows.**

This single idea unlocks problems like **#185 Department Top Three Salaries**, and later makes many "first/latest/previous/next/top N per group" questions much easier.

---

# 1. Why do we need window functions?

Suppose we have:

| employeedepartmentsalary |    |        |
| ------------------------ | -- | ------ |
| Alice                    | IT | 100000 |
| Bob                      | IT | 80000  |
| Carol                    | IT | 80000  |
| David                    | IT | 60000  |
| Emma                     | HR | 90000  |
| Frank                    | HR | 70000  |

If we do:

```
```

```
SELECT department, MAX(salary)
FROM Employee
GROUP BY department;
```

we get:

| departmentmax\_salary |        |
| --------------------- | ------ |
| IT                    | 100000 |
| HR                    | 90000  |

The individual employee rows are gone.

That's what `GROUP BY` does.

---

# 2. Window functions don't collapse rows

Now:

```
```

```
SELECT
    name,
    department,
    salary,
    MAX(salary) OVER (
        PARTITION BY department
    ) AS department_max
FROM Employee;
```

Result:

| namedepartmentsalarydepartment\_max |    |        |        |
| ----------------------------------- | -- | ------ | ------ |
| Alice                               | IT | 100000 | 100000 |
| Bob                                 | IT | 80000  | 100000 |
| Carol                               | IT | 80000  | 100000 |
| David                               | IT | 60000  | 100000 |
| Emma                                | HR | 90000  | 90000  |
| Frank                               | HR | 70000  | 90000  |

🔥 **Rows remain.**

That's the magic.

---

# 3. The basic window syntax

You'll see:

```
```

```
FUNCTION(...) OVER (
    PARTITION BY ...
    ORDER BY ...
)
```

There are three important pieces.

### Function

For example:

```
```

```
ROW_NUMBER()
```

or:

```
```

```
RANK()
```

or:

```
```

```
SUM(salary)
```

### `PARTITION BY`

Defines the group/window.

```
```

```
PARTITION BY department
```

means:

> Treat each department separately.

### `ORDER BY`

Defines the order inside the window.

```
```

```
ORDER BY salary DESC
```

means:

> Highest salary first.

---

# 4. `ROW_NUMBER()`

Let's rank employees within each department:

```
```

```
SELECT
    name,
    department,
    salary,
    ROW_NUMBER() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS rn
FROM Employee;
```

Result:

| namedeptsalaryrn |    |        |   |
| ---------------- | -- | ------ | - |
| Alice            | IT | 100000 | 1 |
| Bob              | IT | 80000  | 2 |
| Carol            | IT | 80000  | 3 |
| David            | IT | 60000  | 4 |
| Emma             | HR | 90000  | 1 |
| Frank            | HR | 70000  | 2 |

Notice something important:

Bob and Carol have the same salary, but they receive different row numbers.

```
```

```
Bob   → 2
Carol → 3
```

That's exactly what `ROW_NUMBER()` means:

> **Every row gets a unique sequential number.**

---

# 5. `RANK()`

Now:

```
```

```
RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

Result:

| namesalaryrank |        |   |
| -------------- | ------ | - |
| Alice          | 100000 | 1 |
| Bob            | 80000  | 2 |
| Carol          | 80000  | 2 |
| David          | 60000  | 4 |

Bob and Carol tie.

Both receive:

```
```

```
2
```

But notice the next rank:

```
```

```
4
```

There is a gap.

That's the defining behavior of `RANK()`.

---

# 6. `DENSE_RANK()`

Now:

```
```

```
DENSE_RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

Result:

| namesalarydense\_rank |        |   |
| --------------------- | ------ | - |
| Alice                 | 100000 | 1 |
| Bob                   | 80000  | 2 |
| Carol                 | 80000  | 2 |
| David                 | 60000  | 3 |

No gap.

So:

```
```

```
ROW_NUMBER
→ unique number per row

RANK
→ ties share rank, gaps appear

DENSE_RANK
→ ties share rank, no gaps
```

---

# 7. Memorize this table

Suppose salaries are:

```
```

```
100
80
80
60
```

Then:

| salaryROW\_NUMBERRANKDENSE\_RANK |   |   |   |
| -------------------------------- | - | - | - |
| 100                              | 1 | 1 | 1 |
| 80                               | 2 | 2 | 2 |
| 80                               | 3 | 2 | 2 |
| 60                               | 4 | 4 | 3 |

This distinction is **critical** for SQL interviews.

---

# 8. Why #185 needs `DENSE_RANK`

Remember #185:

> Find employees who are among the top three **unique salaries** in each department.

"Unique salaries" is the giveaway.

Suppose:

```
```

```
IT

100000
80000
80000
60000
50000
```

The unique salary levels are:

```
```

```
100000 → 1
80000  → 2
60000  → 3
50000  → 4
```

Therefore:

```
```

```
100000
80000
80000
60000
```

should qualify.

`DENSE_RANK()` gives exactly that:

```
```

```
100000 → 1
80000  → 2
80000  → 2
60000  → 3
50000  → 4
```

So:

```
```

```
DENSE_RANK() OVER (
    PARTITION BY departmentId
    ORDER BY salary DESC
)
```

is the key.

---

# 9. #185 — Department Top Three Salaries

We cannot simply write:

```
```

```
WHERE DENSE_RANK() <= 3
```

in the same query level because window functions are evaluated after `WHERE`.

So we create an intermediate result.

```
```

```
SELECT *
FROM (
    SELECT
        d.name AS Department,
        e.name AS Employee,
        e.salary,
        DENSE_RANK() OVER (
            PARTITION BY e.departmentId
            ORDER BY e.salary DESC
        ) AS salary_rank
    FROM Employee e
    JOIN Department d
        ON e.departmentId = d.id
) ranked
WHERE salary_rank <= 3;
```

🔥 This is a very important pattern:

```
```

```
Original table
      ↓
Window function
      ↓
assign ranks
      ↓
derived table
      ↓
WHERE rank <= 3
```

---

# 10. Why can't we put the filter immediately after SELECT?

This won't work:

```
```

```
SELECT
    name,
    DENSE_RANK() OVER (...) AS r
FROM Employee
WHERE r <= 3;
```

Because `r` is generated by the window calculation, and `WHERE` happens earlier in SQL's logical processing.

So we do:

```
```

```
Query 1:
calculate rank

Query 2:
filter rank
```

This idea will appear repeatedly.

---

# 11. Window functions + `PARTITION BY`

Think of:

```
```

```
PARTITION BY department
```

as:

> "Reset the calculation for every department."

For example:

```
```

```
IT:
100k → rank 1
80k  → rank 2
60k  → rank 3

HR:
90k → rank 1
70k → rank 2
```

The ranking starts from 1 again when we enter HR.

---

# 12. `LAG()` — look at the previous row

Now we introduce another major interview function.

Suppose:

| datetemperature |    |
| --------------- | -- |
| Jan 1           | 10 |
| Jan 2           | 20 |
| Jan 3           | 15 |
| Jan 4           | 25 |

We can write:

```
```

```
SELECT
    date,
    temperature,
    LAG(temperature) OVER (
        ORDER BY date
    ) AS previous_temperature
FROM Weather;
```

Result:

| datetemperatureprevious\_temperature |    |      |
| ------------------------------------ | -- | ---- |
| Jan 1                                | 10 | NULL |
| Jan 2                                | 20 | 10   |
| Jan 3                                | 15 | 20   |
| Jan 4                                | 25 | 15   |

🔥 `LAG()` means:

> Give me a value from a previous row.

---

# 13. `LEAD()`

The opposite:

```
```

```
LEAD(temperature) OVER (
    ORDER BY date
)
```

Result:

| datetemperaturenext\_temperature |    |      |
| -------------------------------- | -- | ---- |
| Jan 1                            | 10 | 20   |
| Jan 2                            | 20 | 15   |
| Jan 3                            | 15 | 25   |
| Jan 4                            | 25 | NULL |

So:

```
```

```
LAG
→ previous

LEAD
→ next
```

---

# 14. Why `LAG()` is powerful

Suppose the interviewer asks:

> Find days where today's temperature is greater than yesterday's.

With a window function:

```
```

```
SELECT *
FROM (
    SELECT
        recordDate,
        temperature,
        LAG(temperature) OVER (
            ORDER BY recordDate
        ) AS previous_temperature
    FROM Weather
) x
WHERE temperature > previous_temperature;
```

That's conceptually much cleaner than a self join.

Notice how #197 can be solved with either:

```
```

```
SELF JOIN
```

or:

```
```

```
LAG()
```

Learning both approaches makes you much stronger.

---

# 15. `LAG()` with a partition

Suppose we have sales:

| employeedatesales |       |     |
| ----------------- | ----- | --- |
| Alice             | Jan 1 | 100 |
| Alice             | Jan 2 | 150 |
| Bob               | Jan 1 | 200 |
| Bob               | Jan 2 | 250 |

We want each employee's previous sale.

```
```

```
LAG(sales) OVER (
    PARTITION BY employee
    ORDER BY date
)
```

Result:

| employeedatesalesprevious |       |     |      |
| ------------------------- | ----- | --- | ---- |
| Alice                     | Jan 1 | 100 | NULL |
| Alice                     | Jan 2 | 150 | 100  |
| Bob                       | Jan 1 | 200 | NULL |
| Bob                       | Jan 2 | 250 | 200  |

Again:

```
```

```
PARTITION BY employee
```

means the calculation resets for every employee.

---

# 16. `ROW_NUMBER()` for first/latest records

This is another interview pattern you should memorize.

Suppose we want:

> The latest order for every customer.

Use:

```
```

```
ROW_NUMBER() OVER (
    PARTITION BY customer_id
    ORDER BY order_date DESC
)
```

Then:

```
```

```
rn = 1
```

means:

> This is the latest order for this customer.

Full pattern:

```
```

```
SELECT *
FROM (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC
        ) AS rn
    FROM Orders o
) x
WHERE rn = 1;
```

---

# 17. First record instead

Change:

```
```

```
ORDER BY order_date DESC
```

to:

```
```

```
ORDER BY order_date ASC
```

Then:

```
```

```
rn = 1
```

means:

> first order.

So:

```
```

```
ASC
→ first

DESC
→ latest
```

This is an incredibly useful interview pattern.

---

# 18. Window aggregate functions

Window functions aren't limited to ranking.

You can do:

```
```

```
SUM(salary) OVER (...)
```

```
```

```
AVG(salary) OVER (...)
```

```
```

```
MIN(salary) OVER (...)
```

```
```

```
MAX(salary) OVER (...)
```

Example:

```
```

```
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM Employee;
```

Result:

| employeedeptsalarydept\_avg |    |      |     |
| --------------------------- | -- | ---- | --- |
| Alice                       | IT | 100k | 80k |
| Bob                         | IT | 80k  | 80k |
| Carol                       | IT | 60k  | 80k |
| Emma                        | HR | 90k  | 80k |
| Frank                       | HR | 70k  | 80k |

Again:

### `GROUP BY`

```
```

```
3 IT rows
      ↓
1 IT result row
```

### Window

```
```

```
3 IT rows
      ↓
3 IT result rows
```

This distinction is fundamental.

---

# 19. Running totals

Suppose:

| datesales |     |
| --------- | --- |
| Jan 1     | 100 |
| Jan 2     | 200 |
| Jan 3     | 150 |

We want:

| datesalesrunning\_total |     |     |
| ----------------------- | --- | --- |
| Jan 1                   | 100 | 100 |
| Jan 2                   | 200 | 300 |
| Jan 3                   | 150 | 450 |

Use:

```
```

```
SELECT
    date,
    sales,
    SUM(sales) OVER (
        ORDER BY date
    ) AS running_total
FROM Sales;
```

This introduces the idea of a **window frame**, which we'll tackle soon.

---

# 20. The five window functions to master

For your SQL interview preparation, make these automatic:

```
```

```
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
```

And then:

```
```

```
SUM() OVER()
AVG() OVER()
MIN() OVER()
MAX() OVER()
```

---

# 🧠 Pattern recognition

When the interviewer says:

### "Top N in each department"

Think:

```
```

```
DENSE_RANK()
PARTITION BY department
ORDER BY salary DESC
```

---

### "First order per customer"

Think:

```
```

```
ROW_NUMBER()
PARTITION BY customer
ORDER BY date ASC
```

---

### "Latest order per customer"

Think:

```
```

```
ROW_NUMBER()
PARTITION BY customer
ORDER BY date DESC
```

---

### "Previous day's value"

Think:

```
```

```
LAG()
ORDER BY date
```

---

### "Next day's value"

Think:

```
```

```
LEAD()
ORDER BY date
```

---

### "Average for each department but retain employee rows"

Think:

```
```

```
AVG() OVER(PARTITION BY department)
```

---

### "Running total"

Think:

```
```

```
SUM() OVER(ORDER BY date)
```

---

# 🔥 Your next SQL 50 connection

Now revisit **#185**.

The English:

> "Top three unique salaries in each department."

Translate:

```
```

```
"each department"
       ↓
PARTITION BY department

"unique salaries"
       ↓
DENSE_RANK

"top three"
       ↓
rank <= 3
```

That's the complete thought process.

Not memorization.

---

# 🎯 Interview drill

Try these **without writing SQL yet**.

### Q1

For:

```
```

```
100
100
90
80
```

What are the results of:

```
```

```
ROW_NUMBER
RANK
DENSE_RANK
```

---

### Q2

What does:

```
```

```
PARTITION BY department
```

actually do?

---

### Q3

What's the difference between:

```
```

```
RANK()
```

and:

```
```

```
DENSE_RANK()
```

---

### Q4

How would you find the **latest order for every customer**?

---

### Q5

How would you find the **first order for every customer**?

---

### Q6 🔥

Explain why this:

```
```

```
AVG(salary) OVER (
    PARTITION BY department
)
```

is fundamentally different from:

```
```

```
AVG(salary)
FROM Employee
GROUP BY department
```

---

### Q7 🔥🔥

Suppose an interviewer asks:

> "For every employee, show their salary and the salary of the employee who joined immediately before them in the same department."

Which window function and which two window clauses would you think of immediately?

---

## Where we're going next

After this, we'll do **window functions properly at interview depth**:

```
```

```
ROW_NUMBER
RANK
DENSE_RANK
        ↓
LAG / LEAD
        ↓
window frames
        ↓
running totals
        ↓
moving averages
        ↓
first/last within groups
        ↓
Top-N per group
        ↓
consecutive rows
```


---
📍 EXACTLY WHERE WE ARE

I'd put us here:

DATABASE BASICS                 ✅
       ↓
CONSTRAINTS / KEYS / NULL       ✅
       ↓
SELECT / WHERE                  ✅
       ↓
DISTINCT / LIKE / IN / BETWEEN  ✅
       ↓
ORDER BY                        ✅
       ↓
JOINs                           ✅
       ↓
GROUP BY / AGGREGATION          ✅
       ↓
HAVING                          ✅
       ↓
SUBQUERIES                      🟡
       ↓
CASE WHEN                       ✅
       ↓
CONDITIONAL AGGREGATION         ✅
       ↓
DATE FUNCTIONS                  ✅
       ↓
WINDOW FUNCTIONS                🔥 WE ARE HERE
       ↓
CTEs                            ⏭️
       ↓
ADVANCED SUBQUERIES / EXISTS    ⏭️
       ↓
ADVANCED STRING / REGEX         ⏭️
       ↓
COMPLEX SQL PATTERNS             ⏭️
       ↓
SQL 50 FULL REVISION             ⏭️
       ↓
INTERVIEW MOCKS                  🎯
---
PART 15 

Absolutely. 🔥 Let's finish the core window-function chapter properly before moving on.

Window Functions — Part 3: Interview Mastery

The goal now isn't to learn more functions randomly. It's to recognize patterns.

1. The most important pattern: Top N per group

Suppose:

employee	dept	salary
A	IT	100
B	IT	90
C	IT	90
D	IT	70
E	HR	120
F	HR	80

Question:

Find the top 2 unique salaries in each department.

Step 1 — Rank within department
DENSE_RANK() OVER (
    PARTITION BY dept
    ORDER BY salary DESC
)

Result:

employee	dept	salary	rnk
A	IT	100	1
B	IT	90	2
C	IT	90	2
D	IT	70	3
E	HR	120	1
F	HR	80	2
Step 2 — Filter
WHERE rnk <= 2

This gives:

IT → 100, 90, 90
HR → 120, 80
Pattern
TOP N UNIQUE VALUES PER GROUP
        ↓
DENSE_RANK()
        ↓
PARTITION BY group
        ↓
ORDER BY value DESC
        ↓
outer WHERE rank <= N

This pattern alone is worth memorizing.

2. Exactly N rows vs N unique values

This distinction is an interview favorite.

"Give me the top 3 employees in each department"

Potentially:

ROW_NUMBER()

because you want 3 rows.

"Give me employees earning one of the top 3 salaries"

Use:

DENSE_RANK()

because you want 3 salary levels.

3. First row per group

Question:

Find each customer's first order.

Use:

ROW_NUMBER() OVER (
    PARTITION BY customer_id
    ORDER BY order_date ASC
)

Then:

WHERE rn = 1

Complete pattern:

WITH ranked AS (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date ASC
        ) AS rn
    FROM Orders o
)
SELECT *
FROM ranked
WHERE rn = 1;
Translate the English

each customer

→ PARTITION BY customer_id

first

→ ORDER BY order_date ASC

only the first

→ WHERE rn = 1

This translation skill is what we want.

4. Latest row per group

Exactly the same thing.

Only change:

ORDER BY order_date DESC

So:

ROW_NUMBER() OVER (
    PARTITION BY customer_id
    ORDER BY order_date DESC
)

Then:

WHERE rn = 1
Memorize:
FIRST
→ ASC

LATEST
→ DESC
5. What if two orders have exactly the same date?

Excellent interview question.

If you have:

Customer 1

Order A → 2024-01-01
Order B → 2024-01-01

then:

ORDER BY order_date DESC

doesn't completely determine which row comes first.

You should add a tie-breaker if the schema provides one:

ROW_NUMBER() OVER (
    PARTITION BY customer_id
    ORDER BY order_date DESC, order_id DESC
)

Now the ordering is deterministic.

Interview principle

If your ranking/order has ties and the problem requires one exact row, add a deterministic tie-breaker.

6. LAG() — comparing adjacent rows

Now let's shift from ranking to comparison.

Suppose:

day	sales
1	100
2	150
3	120
4	200

We want:

Today's sales compared with yesterday's.

SELECT
    day,
    sales,
    LAG(sales) OVER (
        ORDER BY day
    ) AS previous_sales
FROM Sales;

Result:

day	sales	previous
1	100	NULL
2	150	100
3	120	150
4	200	120

Now we can calculate the change:

sales - previous_sales
7. Growth percentage

This is a very common interview variation.

(current - previous) / previous * 100

For example:

WITH x AS (
    SELECT
        day,
        sales,
        LAG(sales) OVER (
            ORDER BY day
        ) AS previous_sales
    FROM Sales
)
SELECT
    day,
    sales,
    100.0 * (sales - previous_sales) / previous_sales
        AS growth_percentage
FROM x;

Notice the CTE/derived intermediate result.

That's an important pattern:

window calculation
       ↓
intermediate table
       ↓
calculation using window result
8. LAG() + condition

Question:

Find days where sales increased compared with the previous day.

WITH x AS (
    SELECT
        day,
        sales,
        LAG(sales) OVER (
            ORDER BY day
        ) AS previous_sales
    FROM Sales
)
SELECT *
FROM x
WHERE sales > previous_sales;

This is essentially the same pattern as LeetCode #197 Rising Temperature.

9. LEAD() — looking forward

Suppose we need:

Find the next event for each user.

LEAD(event_date) OVER (
    PARTITION BY user_id
    ORDER BY event_date
)

Then you can calculate:

DATEDIFF(next_event, event_date)

This combination is extremely useful:

LEAD()
+
DATEDIFF()

for questions about:

time until next event.

10. Running totals

Now let's understand window frames more deeply.

Data:

day	revenue
1	100
2	200
3	300
4	150

Running total:

100
300
600
750

SQL:

SELECT
    day,
    revenue,
    SUM(revenue) OVER (
        ORDER BY day
        ROWS BETWEEN UNBOUNDED PRECEDING
                     AND CURRENT ROW
    ) AS running_total
FROM Sales;

Read it literally:

start at the first row
        ↓
include every row
        ↓
stop at current row
11. Why ORDER BY matters inside OVER()

Compare:

SUM(revenue) OVER (
    PARTITION BY department
)

with:

SUM(revenue) OVER (
    PARTITION BY department
    ORDER BY date
)

The first means:

Give every row the department's total.

The second introduces an ordered window and can produce a cumulative calculation depending on the frame.

So:

PARTITION BY
→ WHO belongs to the window?

ORDER BY
→ IN WHAT ORDER are rows considered?

FRAME
→ WHICH rows around the current row are included?

That's the mental model.

12. Moving average

Suppose:

day	sales
1	10
2	20
3	30
4	40
5	50

Three-row moving average:

AVG(sales) OVER (
    ORDER BY day
    ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
)

Day 4:

20 + 30 + 40
------------
     3

= 30

Day 5:

30 + 40 + 50
------------
     3

= 40
13. ROWS means physical rows

This is worth understanding.

ROWS BETWEEN 2 PRECEDING AND CURRENT ROW

means:

Take the previous two rows and this row.

It is about rows in the ordered result.

This becomes important when there are duplicate ordering values.

14. RANGE is different

You may see:

RANGE BETWEEN ...

RANGE considers the ordering value, rather than simply counting physical rows.

For now, for your SQL 50 preparation, focus heavily on:

ROWS BETWEEN

and understand that RANGE has different semantics when ties exist.

15. FIRST_VALUE()

Suppose:

Department    Salary
IT            100
IT             80
IT             60

We can show the department's highest salary on every row:

FIRST_VALUE(salary) OVER (
    PARTITION BY department
    ORDER BY salary DESC
)

Result:

100 → 100
80  → 100
60  → 100

This is useful when the question says:

Compare each row against the first/highest/earliest value in its group.

16. Combining LAG() with CASE

Now we're combining chapters.

Suppose:

Classify each employee as having a salary increase or decrease compared with the previous employee in the department.

WITH x AS (
    SELECT
        name,
        department,
        salary,
        LAG(salary) OVER (
            PARTITION BY department
            ORDER BY employee_id
        ) AS previous_salary
    FROM Employee
)
SELECT
    name,
    department,
    salary,
    CASE
        WHEN previous_salary IS NULL THEN 'First'
        WHEN salary > previous_salary THEN 'Increase'
        WHEN salary < previous_salary THEN 'Decrease'
        ELSE 'Same'
    END AS status
FROM x;

Look at what we're combining:

PARTITION BY
+
ORDER BY
+
LAG
+
CASE

This is the level we want to reach.

17. A powerful interview pattern: detecting changes

Suppose user status is:

user  date       status

1     Jan 1      active
1     Jan 2      active
1     Jan 3      inactive
1     Jan 4      inactive
1     Jan 5      active

We can use:

LAG(status) OVER (
    PARTITION BY user_id
    ORDER BY date
)

Then compare:

CASE
    WHEN status <> previous_status THEN 1
    ELSE 0
END

This lets us identify state changes.

This pattern becomes useful for advanced questions involving:

consecutive states
sessions
streaks
status changes
gaps
18. The "consecutive rows" family

This is where SQL starts becoming genuinely interesting.

Suppose:

id
1
2
3
4
5

and some condition is true for:

1
2
3

We want to identify the consecutive sequence.

Window functions such as:

LAG()
ROW_NUMBER()

can help transform the data so that consecutive records can be grouped.

This is a major advanced SQL pattern.

We'll tackle it when we reach #180 Consecutive Numbers.

19. What you've now learned

You can now recognize:

Ranking
ROW_NUMBER
RANK
DENSE_RANK
Relative rows
LAG
LEAD
Group-level values while retaining rows
SUM() OVER
AVG() OVER
MIN() OVER
MAX() OVER
Ordered calculations
ORDER BY inside OVER
Sliding calculations
ROWS BETWEEN ...
Major patterns
Top N per group
First per group
Latest per group
Previous/next row
Running total
Moving average
Change detection
🧠 The interview cheat sheet

When you hear:

Top 3 unique salaries per department

Think:

DENSE_RANK()
PARTITION BY department
ORDER BY salary DESC

Exactly one latest record per customer

Think:

ROW_NUMBER()
PARTITION BY customer
ORDER BY date DESC

Compare current row with previous row

Think:

LAG()

Compare current row with next row

Think:

LEAD()

Running total

Think:

SUM() OVER (
    ORDER BY date
)

Last 7 rows average

Think:

AVG() OVER (
    ORDER BY date
    ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
)

Value for each group while keeping every row

Think:

SUM/AVG/MAX/MIN() OVER (
    PARTITION BY ...
)
🎯 Now let's make this interview-ready

Don't just read the next section.

Try these mentally:

Problem 1

You have:

employee  department  salary
A         IT          100
B         IT           90
C         IT           90
D         IT           80
E         HR          120
F         HR          100

Which function would you use to find employees earning the top 2 unique salaries in each department?

Problem 2

Find the latest order for every customer.

What goes inside:

ROW_NUMBER() OVER (...)

?

Problem 3

You have:

date   temperature
1      10
2      15
3      12
4      20

How would you find rows where today's temperature is higher than yesterday's?

Problem 4 🔥

You have:

date   revenue
1      100
2      200
3      300
4      400

What window expression gives:

100
300
600
1000

?

Problem 5 🔥🔥

Explain the difference between:

SUM(amount) OVER (
    PARTITION BY customer_id
)

and:

SUM(amount) OVER (
    PARTITION BY customer_id
    ORDER BY order_date
)

If you can explain these five confidently, you're ready for the next stage.

---

PART 16

Absolutely. 🔥 We now move to one of the most important query-structuring chapters:

CTEs + Subqueries + EXISTS + SQL Logical Execution Order

This chapter is crucial because Medium/Hard SQL problems often aren't difficult because of syntax. They're difficult because you need to build an intermediate result, then query that result.

1. First: Why do we need subqueries?

Imagine the interviewer asks:

Find employees whose salary is greater than the average salary.

There are two logical steps:

1. Calculate average salary
2. Find employees above that average

The average is itself a query:

SELECT AVG(salary)
FROM Employee;

We can use that query inside another query:

SELECT name, salary
FROM Employee
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
);

The inner query is a subquery.

2. The mental model

Think:

              OUTER QUERY
                  │
                  ↓
        "employees with salary > X"
                  │
                  ↑
              SUBQUERY
                  │
                  ↓
            "calculate X"

So when an interview question contains:

greater than the average

you should immediately think:

(
    SELECT AVG(...)
)
3. Scalar subquery

The previous example returns one value:

SELECT AVG(salary)
FROM Employee;

For example:

75,000

Therefore:

WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
)

is valid.

This is called a scalar subquery: a subquery that produces one value.

4. Subquery returning multiple values

Suppose:

Find employees who work in departments located in New York.

The subquery might return multiple department IDs:

SELECT id
FROM Department
WHERE location = 'New York';

Potentially:

1
3
7

We can't use:

WHERE department_id = (
    SELECT id ...
)

because = expects a single value.

Instead:

WHERE department_id IN (
    SELECT id
    FROM Department
    WHERE location = 'New York'
);
Rule
one value
→ =

multiple values
→ IN
5. EXISTS

Now we get to a very important interview concept.

Suppose:

Find customers who have placed at least one order.

You could use:

SELECT DISTINCT c.customer_id
FROM Customers c
JOIN Orders o
    ON c.customer_id = o.customer_id;

But another elegant approach is:

SELECT c.customer_id
FROM Customers c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
);

Read this as:

For this customer, does at least one matching order exist?

That's exactly what EXISTS asks.

6. Why SELECT 1?

You will often see:

EXISTS (
    SELECT 1
    FROM Orders o
    WHERE ...
)

The 1 isn't special.

EXISTS only cares whether the subquery produces at least one row.

So conceptually:

EXISTS (...)

means:

Did this query find anything?
       │
       ├── yes → TRUE
       └── no  → FALSE
7. Correlated subquery

Look carefully:

SELECT c.customer_id
FROM Customers c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
);

The inner query references:

c.customer_id

from the outer query.

That's why it's called a correlated subquery.

The inner query depends on the current outer row.

Mental model:

Customer A
   ↓
Does order exist for A?

Customer B
   ↓
Does order exist for B?

Customer C
   ↓
Does order exist for C?
8. NOT EXISTS

Now reverse the question:

Find customers who have never placed an order.

SELECT c.customer_id
FROM Customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
);

This is extremely useful.

Whenever you hear:

who did NOT...

for whom there is NO...

never...

think:

NOT EXISTS
9. NOT EXISTS vs NOT IN

This is an important interview topic because of NULL.

Suppose:

WHERE customer_id NOT IN (
    SELECT customer_id
    FROM Orders
)

If the subquery can contain NULL, NOT IN can produce unintuitive results because of SQL's three-valued logic.

For anti-matching questions, a safer/common pattern is:

WHERE NOT EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
)

This connects directly back to the NULL and three-valued logic chapter we learned earlier.

10. CTEs

Now let's make complex queries easier to read.

CTE:

Common Table Expression

Syntax:

WITH name AS (
    SELECT ...
)
SELECT ...
FROM name;

Example:

WITH high_salary AS (
    SELECT *
    FROM Employee
    WHERE salary > 100000
)
SELECT *
FROM high_salary;

Think of a CTE as:

temporary named result
        ↓
which the next query can use
11. Why CTEs are so useful

Suppose we need:

Find employees whose salary is greater than the average salary of their department.

That's more complicated.

We could use a correlated subquery:

SELECT e.name, e.salary
FROM Employee e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM Employee e2
    WHERE e2.department_id = e.department_id
);

But we can also calculate department averages first:

WITH department_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM Employee
    GROUP BY department_id
)
SELECT
    e.name,
    e.salary
FROM Employee e
JOIN department_avg d
    ON e.department_id = d.department_id
WHERE e.salary > d.avg_salary;

This is often easier to reason about.

12. CTE = breaking a problem into steps

This is exactly how I want you to approach interview problems.

Instead of thinking:

"How do I write one giant SQL query?"

Think:

Step 1 → calculate X
Step 2 → calculate Y
Step 3 → combine X and Y
Step 4 → filter
Step 5 → present result

Then:

WITH step1 AS (...),
step2 AS (...)
SELECT ...

This is query decomposition.

13. Multiple CTEs

You can have:

WITH
sales_summary AS (
    ...
),
customer_summary AS (
    ...
),
final_data AS (
    ...
)
SELECT *
FROM final_data;

The CTEs can build upon each other.

Example:

WITH sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM Orders
    GROUP BY customer_id
),
classified AS (
    SELECT
        customer_id,
        total_sales,
        CASE
            WHEN total_sales >= 10000 THEN 'VIP'
            ELSE 'Regular'
        END AS customer_type
    FROM sales
)
SELECT *
FROM classified;

This is much easier to debug than one enormous query.

14. CTE + window function

Here's why this chapter comes after window functions.

Suppose:

Find the top 3 salaries in each department.

We calculate the rank first:

WITH ranked AS (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM Employee e
)
SELECT *
FROM ranked
WHERE rnk <= 3;

Why can't we simply put:

WHERE rnk <= 3

in the same query level?

Because of logical query processing order.

And this brings us to one of the most important concepts in SQL.

15. SQL logical execution order

You write:

SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY

But conceptually SQL processes these stages approximately as:

FROM
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY

Window functions happen after the result rows have been formed, which is why you generally cannot directly use a window-function result in that query block's WHERE.

So:

WHERE ROW_NUMBER() OVER (...)

❌ Not valid.

Instead:

Query 1
  ↓
calculate row_number
  ↓
CTE / derived table
  ↓
Query 2
  ↓
WHERE rn = 1

That's the reason behind this incredibly common pattern:

WITH ranked AS (...)
SELECT *
FROM ranked
WHERE rn = 1;
16. The "SQL layer" mental model

Imagine SQL as layers:

┌─────────────────────────┐
│       ORDER BY          │
├─────────────────────────┤
│        SELECT           │
├─────────────────────────┤
│       HAVING            │
├─────────────────────────┤
│      GROUP BY           │
├─────────────────────────┤
│        WHERE            │
├─────────────────────────┤
│         FROM            │
└─────────────────────────┘

Window functions are evaluated late enough that their result isn't available to the same query block's WHERE.

So if you need:

window calculation
        ↓
filter based on it

you create another query layer.

17. Derived table vs CTE

These two are conceptually similar.

Derived table
SELECT *
FROM (
    SELECT
        *,
        ROW_NUMBER() OVER (...) AS rn
    FROM Employee
) x
WHERE rn = 1;
CTE
WITH x AS (
    SELECT
        *,
        ROW_NUMBER() OVER (...) AS rn
    FROM Employee
)
SELECT *
FROM x
WHERE rn = 1;

For interview readability, I generally prefer the CTE when the intermediate result has a meaningful name or the query has multiple stages.

18. SQL 50 connection: #185

We previously solved:

Department Top Three Salaries.

Now you should understand why the solution naturally has two query layers:

Employee
   ↓
DENSE_RANK per department
   ↓
ranked employees
   ↓
WHERE rank <= 3

That isn't arbitrary SQL syntax.

It's the structure of the problem.

19. SQL 50 connection: #1045

Customers Who Bought All Products

This problem is an excellent example of relational division.

The English says:

Find customers who have purchased every product.

Think:

Customer
   ↓
How many distinct products did they buy?
   ↓
Compare with total number of products

One possible strategy:

SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (
    SELECT COUNT(*)
    FROM Product
);

Look at the structure:

GROUP BY
+
COUNT(DISTINCT)
+
subquery
+
HAVING

This is exactly the kind of problem where combining concepts matters more than memorizing syntax.

20. SQL 50 connection: #1978

Employees Whose Manager Left the Company

Question:

Find employees whose manager no longer exists in the Employees table.

This is fundamentally an anti-match problem.

Think:

employee
   ↓
manager_id
   ↓
does manager exist?
   ↓
NO

You can approach this using a LEFT JOIN:

SELECT e.employee_id
FROM Employees e
LEFT JOIN Employees m
    ON e.manager_id = m.employee_id
WHERE m.employee_id IS NULL;

Or with NOT EXISTS:

SELECT e.employee_id
FROM Employees e
WHERE e.manager_id IS NOT NULL
  AND NOT EXISTS (
      SELECT 1
      FROM Employees m
      WHERE m.employee_id = e.manager_id
  );

This is a beautiful example of how:

SELF JOIN
+
NULL
+
NOT EXISTS

can solve the same conceptual problem.

21. SQL 50 connection: #176

Second Highest Salary

One possible approach:

SELECT MAX(salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (
    SELECT MAX(salary)
    FROM Employee
);

Break it down:

highest salary
       ↓
MAX(salary)

remove it
       ↓
salary < highest

highest remaining salary
       ↓
MAX()

Notice how simple the query becomes once you decompose the English.

22. The interview superpower: translate English → relational operation

This is what I want you practicing now.

Interview wording	Think
"for every department"	GROUP BY / PARTITION BY
"at least one"	EXISTS
"none" / "never"	NOT EXISTS
"greater than average"	subquery / CTE
"top N per group"	window ranking
"latest per customer"	ROW_NUMBER()
"previous row"	LAG()
"next row"	LEAD()
"all products"	count comparison / relational division
"doesn't have a matching row"	LEFT JOIN ... IS NULL / NOT EXISTS
"calculate first, then filter"	CTE / derived table
🧠 The big picture

You've now reached a very important point in the track:

BASIC SQL
   ↓
JOIN
   ↓
AGGREGATION
   ↓
HAVING
   ↓
CASE
   ↓
DATES
   ↓
WINDOW FUNCTIONS
   ↓
CTEs + SUBQUERIES   ← WE ARE HERE
   ↓
ADVANCED STRING / REGEX
   ↓
COMBINED SQL PATTERNS
   ↓
SQL 50 REVISION
   ↓
INTERVIEW MODE

And from here, we're going to stop learning features in isolation.

We'll start combining them.
---
PART 17

🔥 Next Lesson: EXISTS vs IN vs JOIN vs NOT EXISTS vs LEFT JOIN ... IS NULL

This is a high-value interview topic because several different SQL queries can answer almost the same English question, but their semantics are not identical.

The goal isn't to memorize five syntaxes.

The goal is to recognize:

"Am I trying to return rows from the left table, or am I trying to combine data from two tables?"

1. Start with the simplest distinction

Suppose we have:

Customers
customer_id	name
1	Alice
2	Bob
3	Charlie
4	David
Orders
order_id	customer_id
101	1
102	1
103	3

Question:

Find customers who have at least one order.

There are several ways.

2. EXISTS
SELECT c.customer_id, c.name
FROM Customers c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
);

Result:

Alice
Charlie

The important idea:

Customer
   ↓
Does a matching order exist?
   ↓
YES → keep customer
NO  → discard customer

EXISTS is asking a yes/no question.

3. EXISTS doesn't care how many matches

Alice has two orders:

Alice
 ├── Order 101
 └── Order 102

But:

EXISTS (...)

still produces only:

Alice

It doesn't return one Alice per order.

This is a major conceptual difference from a normal join.

4. JOIN

Now:

SELECT c.customer_id, c.name
FROM Customers c
JOIN Orders o
    ON c.customer_id = o.customer_id;

Result:

Alice
Alice
Charlie

Why two Alices?

Because Alice has two matching orders.

The join creates:

Alice × Order 101
Alice × Order 102
Charlie × Order 103

So:

EXISTS
→ "Does a match exist?"

JOIN
→ "Combine matching rows."

That's the fundamental difference.

5. Avoid blindly adding DISTINCT

You might write:

SELECT DISTINCT c.customer_id, c.name
FROM Customers c
JOIN Orders o
    ON c.customer_id = o.customer_id;

Now you get:

Alice
Charlie

Correct.

But notice what happened:

JOIN
 ↓
duplicate customers
 ↓
DISTINCT
 ↓
remove duplicates

If the question is simply:

Does at least one order exist?

then EXISTS expresses the intention more directly:

WHERE EXISTS (...)
6. IN

You can also write:

SELECT customer_id, name
FROM Customers
WHERE customer_id IN (
    SELECT customer_id
    FROM Orders
);

This means:

Keep customers whose ID belongs to the set of customer IDs returned by the subquery.

Think:

Orders
 ↓
{1, 3}
 ↓
Customers whose ID ∈ {1, 3}

Result:

Alice
Charlie
7. IN vs EXISTS

These often solve the same problem:

IN
WHERE customer_id IN (
    SELECT customer_id
    FROM Orders
)
EXISTS
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
)

But mentally they are different:

IN
→ Is my value inside this set?

EXISTS
→ Does a matching row exist?
8. When EXISTS feels natural

Question:

Find employees who have at least one project.

Think:

WHERE EXISTS (
    SELECT 1
    FROM EmployeeProject ep
    WHERE ep.employee_id = e.employee_id
)

Because the question is:

Does a matching project exist?

9. When IN feels natural

Question:

Find employees working in departments located in London.

You can think:

WHERE department_id IN (
    SELECT department_id
    FROM Department
    WHERE location = 'London'
)

The question is naturally:

Is this department ID in the set of London department IDs?

10. Now the important one: NOT EXISTS

Question:

Find customers who have never placed an order.

SELECT c.customer_id, c.name
FROM Customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
);

Result:

Bob
David

Mental translation:

"never ordered"
      ↓
"no matching order exists"
      ↓
NOT EXISTS

This is a pattern I want you to recognize instantly.

11. LEFT JOIN ... IS NULL

The same conceptual problem can be solved with:

SELECT c.customer_id, c.name
FROM Customers c
LEFT JOIN Orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;

Why?

LEFT JOIN preserves every customer:

Alice    → Order 101
Alice    → Order 102
Bob      → NULL
Charlie  → Order 103
David    → NULL

Then:

WHERE o.customer_id IS NULL

keeps:

Bob
David
12. The anti-join mental model

Both:

NOT EXISTS

and:

LEFT JOIN ... IS NULL

can express:

Find rows with no matching row.

Think:

                  MATCH?
                    │
             ┌──────┴──────┐
            YES            NO
             │              │
           EXISTS       NOT EXISTS

or:

LEFT JOIN
   ↓
unmatched → NULL
   ↓
IS NULL

These are commonly called anti-join patterns.

13. SQL 50 #1978

Let's revisit:

Employees whose manager left the company.

We have:

Employees
employee_id
name
manager_id

An employee's manager should be another employee.

Question:

Does the manager still exist?

That's an existence question.

LEFT JOIN solution
SELECT e.employee_id
FROM Employees e
LEFT JOIN Employees m
    ON e.manager_id = m.employee_id
WHERE e.manager_id IS NOT NULL
  AND m.employee_id IS NULL;

Mental model:

employee
   ↓
manager_id
   ↓
LEFT JOIN to Employees
   ↓
manager doesn't match
   ↓
manager columns = NULL
   ↓
manager left company
14. Same problem with NOT EXISTS
SELECT e.employee_id
FROM Employees e
WHERE e.manager_id IS NOT NULL
  AND NOT EXISTS (
      SELECT 1
      FROM Employees m
      WHERE m.employee_id = e.manager_id
  );

Read it almost like English:

Select employee where manager_id is not null and there does not exist an employee whose ID equals that manager ID.

This is why I want you to become comfortable reading SQL almost like English.

15. The dangerous NOT IN situation ⚠️

Suppose:

WHERE customer_id NOT IN (
    SELECT customer_id
    FROM Orders
)

Looks perfectly reasonable.

But imagine the subquery returns:

1
3
NULL

Now SQL's three-valued logic becomes relevant.

For:

customer_id = 2

SQL essentially asks:

2 NOT IN (1, 3, NULL)

The comparison involving NULL is UNKNOWN, not TRUE.

This can cause NOT IN to behave unexpectedly.

That's one reason NOT EXISTS is an important interview-safe pattern for anti-matching.

16. Connect this back to NULL

Remember our earlier lesson:

NULL ≠ 0
NULL ≠ ''
NULL ≠ FALSE

And:

NULL = something

doesn't produce TRUE or FALSE.

It produces:

UNKNOWN

So:

NOT IN (...)

and NULL can interact in surprising ways.

This is why your earlier lesson on three-valued logic wasn't just theoretical.

It becomes useful here.

17. JOIN when you need columns from the other table

Suppose the interviewer says:

Find customers and show their order dates.

Now EXISTS isn't enough because you actually need data from Orders.

Use:

SELECT
    c.name,
    o.order_date
FROM Customers c
JOIN Orders o
    ON c.customer_id = o.customer_id;

Remember:

Need information from both tables?
        ↓
JOIN
18. EXISTS when you only need to know whether a relationship exists

Question:

Find customers who have placed at least one order.

You don't need:

order ID
order date
order amount

You only need to know:

Does an order exist?

Therefore:

EXISTS

is conceptually excellent.

19. A very useful decision tree

When solving an interview problem:

Do I need columns from another table?
            │
       ┌────┴────┐
      YES        NO
       │          │
     JOIN       Do I only care
                whether a match exists?
                       │
                 ┌─────┴─────┐
                YES          NO
                 │             │
              EXISTS        IN /
                             subquery

For "no matching row":

No matching row?
       ↓
NOT EXISTS
or
LEFT JOIN + IS NULL
20. SQL 50 #1045 — "Bought ALL products"

This is a fantastic example of an ALL question.

Question:

Which customers bought every product?

Suppose there are 3 products:

P1
P2
P3

Customer A bought:

P1
P2
P3

Customer B bought:

P1
P2

Only A qualifies.

One elegant approach:

SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (
    SELECT COUNT(*)
    FROM Product
);

The reasoning is:

How many distinct products did customer buy?
                ↓
       COUNT(DISTINCT)

How many products exist?
                ↓
          COUNT(*)

Are they equal?
                ↓
           HAVING =
21. Another way to think about "ALL"

"Bought all products" can also be understood as:

There does not exist a product that this customer failed to buy.

That's a much more advanced logical transformation:

ALL
 ↓
NOT EXISTS something missing

This is the foundation of relational division questions.

You'll see this idea repeatedly in difficult SQL interviews.

22. SQL 50 #585 — Investments in 2016

This problem is another great example of combining conditions.

The question involves finding investments satisfying conditions based on:

matching values
location
year

The important lesson isn't merely the final query.

It's recognizing that SQL problems often say:

same X
BUT
different Y

which can translate into:

GROUP BY ...
HAVING COUNT(...) ...

or sometimes:

EXISTS / NOT EXISTS

depending on the structure.

We'll revisit #585 in our mixed-problem stage.

23. EXISTS vs JOIN: interview answer

If the interviewer asks:

What's the difference between EXISTS and JOIN?

A strong answer:

"EXISTS is a boolean existence test. It determines whether the subquery returns at least one matching row and doesn't multiply the outer rows based on the number of matches. A JOIN combines rows from two tables, so one outer row can produce multiple result rows when there are multiple matches."

That's an interview-quality answer.

24. IN vs EXISTS: interview answer

"IN compares a value against a set of values returned by a subquery. EXISTS checks whether at least one matching row exists, typically using a correlated condition. Both can express membership/existence queries, but they have different NULL semantics and communicate slightly different intent."

That's the level I want you to reach.

25. NOT EXISTS vs LEFT JOIN IS NULL

Both can answer:

Find customers with no orders.

NOT EXISTS
WHERE NOT EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.customer_id = c.customer_id
)
LEFT JOIN
LEFT JOIN Orders o
    ON o.customer_id = c.customer_id
WHERE o.customer_id IS NULL

Don't memorize one as universally "better."

Instead understand the semantics.

🧠 Your new mental dictionary

When you hear:

"At least one"
EXISTS
"None"
NOT EXISTS
"Belongs to this set"
IN
"Not in this set"
NOT IN

⚠️ Be careful with NULL.

"Combine matching records"
JOIN
"Keep unmatched left records"
LEFT JOIN
"Find unmatched left records"
LEFT JOIN
+
IS NULL
"Every/all"

Think:

COUNT comparison

or, at a deeper level:

NOT EXISTS a missing case
🔥 One level deeper: Semi-join vs Anti-join

These terms are useful in interviews.

Semi-join

Return left rows where a matching right row exists.

Conceptually:

LEFT ROW
   ↓
MATCH EXISTS?
   ↓
YES → return LEFT ROW

Typical SQL:

WHERE EXISTS (...)
Anti-join

Return left rows where no matching right row exists.

LEFT ROW
   ↓
MATCH EXISTS?
   ↓
NO → return LEFT ROW

Typical SQL:

WHERE NOT EXISTS (...)

or:

LEFT JOIN ...
WHERE right.id IS NULL
🎯 Where we are now

Our progression is becoming:

SELECT / WHERE                    ✅
DISTINCT / LIKE / IN / BETWEEN    ✅
ORDER BY                          ✅
JOINs                             ✅
GROUP BY / aggregates             ✅
HAVING                            ✅
CASE                              ✅
DATES                             ✅
WINDOW FUNCTIONS                  ✅
CTEs                              ✅
SUBQUERIES                        ✅
EXISTS / NOT EXISTS               🔥 JUST MASTERED
IN vs EXISTS                      🔥
ANTI-JOIN PATTERNS                🔥
Next lesson

We're ready for the last major syntax family from your SQL 50 list:
---
PART 18

Absolutely. 🔥 We're entering the Advanced String Functions + Regex chapter now.

One important source check first: your uploaded notes explicitly cover LIKE, %, _, IN, BETWEEN, IS NULL, and aliases, but they do not appear to give a detailed treatment of MySQL functions such as SUBSTRING(), LOWER(), TRIM(), or regular expressions.

So for this chapter I'll clearly separate:

📘 Your notes
🌐 MySQL/web knowledge
🎯 SQL 50 application
Chapter: Strings in MySQL

We're going to learn these systematically:

1. LOWER()
2. UPPER()
3. CONCAT()
4. LENGTH()
5. TRIM()
6. SUBSTRING()
7. LEFT()
8. RIGHT()
9. REPLACE()
10. LOCATE()
11. LIKE
12. REGEXP / REGEXP_LIKE
13. Combining string functions

And then immediately apply them to:

#1667 — Fix Names in a Table
#1527 — Patients With a Condition
#1517 — Find Users With Valid E-Mails
#196 — Delete Duplicate Emails
1. LOWER()

Converts a string to lowercase.

SELECT LOWER('HELLO');

Result:

hello

Example:

SELECT LOWER(name)
FROM Users;

If:

ALICE
Bob
CHARLIE

we get:

alice
bob
charlie
Interview use

Whenever you hear:

case-insensitive comparison

you should think about functions such as:

LOWER()
UPPER()

For example:

WHERE LOWER(email) = 'alice@gmail.com'
2. UPPER()

Opposite:

SELECT UPPER('hello');

→

HELLO

Example:

SELECT UPPER(name)
FROM Employee;
3. CONCAT()

Combines strings.

SELECT CONCAT('Hello', ' ', 'World');

Result:

Hello World

Very common:

SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM Employee;

Suppose:

first_name = Rahul
last_name  = Sharma

Result:

Rahul Sharma
Interview translation

Combine first and last name

→

CONCAT(first_name, ' ', last_name)
4. LENGTH()

Returns the length of a string in bytes in MySQL.

SELECT LENGTH('Hello');

Result:

5

This is especially useful for:

Find strings longer than X characters

But ⚠️ there's an important MySQL distinction:

LENGTH()

measures bytes, while:

CHAR_LENGTH()

measures characters.

For ordinary ASCII English:

LENGTH('Hello')      = 5
CHAR_LENGTH('Hello') = 5

But with multibyte characters, they can differ.

For our SQL 50 work, you'll mostly encounter ordinary text, but remember the distinction for interviews.

5. TRIM()

Removes leading and trailing spaces.

SELECT TRIM('   Alice   ');

Result:

Alice

This is useful when data contains accidental whitespace.

Think:

"   Alice   "
      ↓
TRIM()
      ↓
"Alice"
6. SUBSTRING() ⭐

This is one of the most important functions in this chapter.

Suppose:

ABCDEFG

We want:

CDE

We can use:

SELECT SUBSTRING('ABCDEFG', 3, 3);

Result:

CDE

The syntax:

SUBSTRING(string, start_position, length)

MySQL positions are 1-based.

So:

A B C D E F G
1 2 3 4 5 6 7

Therefore:

SUBSTRING('ABCDEFG', 3, 3)

means:

start at 3
take 3 characters

→ CDE

7. Why SUBSTRING() matters for interviews

Suppose an interviewer asks:

Extract the first 3 characters of a username.

You can write:

SUBSTRING(username, 1, 3)

Or:

Extract everything after the first 5 characters.

You can use:

SUBSTRING(username, 6)

The second argument starts the extraction; if length isn't supplied, MySQL returns the remainder.

8. LEFT()

If you want the first N characters:

SELECT LEFT('ABCDEFG', 3);

→

ABC

So:

LEFT(name, 3)

means:

Give me the first 3 characters.

This can sometimes be simpler than SUBSTRING().

9. RIGHT()

Same idea from the other side:

SELECT RIGHT('ABCDEFG', 3);

→

EFG

So:

RIGHT(phone, 4)

is useful for:

Get the last four digits.

10. REPLACE()

Replace one piece of text with another.

SELECT REPLACE(
    'hello world',
    'world',
    'SQL'
);

Result:

hello SQL

Syntax:

REPLACE(string, old_string, new_string)

Example:

SELECT REPLACE(phone, '-', '')
FROM Users;

If:

987-654-3210

becomes:

9876543210
11. LOCATE()

Find the position of a substring.

SELECT LOCATE('world', 'hello world');

Result:

7

Because:

hello world
123456789...
      ↑
      7

This becomes useful when you need to determine whether something occurs inside a string.

12. LIKE — your notes' foundation

Your notes already teach:

LIKE

with two major wildcards:

% → zero or more characters
_ → exactly one character

For example:

WHERE name LIKE 'A%'

means:

starts with A.

Your notes also give patterns such as:

LIKE '%a'

for values ending in a, and:

LIKE '%or%'

for values containing or.

This is extremely important because LIKE and regex solve related but different problems.

13. LIKE vs Regex

This is a key distinction.

LIKE

Good for simple patterns:

WHERE name LIKE 'A%'

Meaning:

starts with A.

Regex

Good for more precise patterns.

For example:

starts with A or B

A regex can express that as:

^[AB]

So think:

LIKE
→ simple wildcard matching

REGEXP
→ more expressive pattern matching
14. Regex fundamentals

Before touching SQL syntax, understand the regex symbols.

^

Beginning of string.

^A

means:

starts with A.

$

End of string.

A$

means:

ends with A.

[abc]

One character from the set.

[abc]

means:

a, b, or c.

[0-9]

Any digit.

[A-Z]

Any uppercase English letter.

[a-z]

Any lowercase English letter.

15. Regex in MySQL

MySQL supports regular-expression matching through REGEXP (also available as RLIKE).

For example:

SELECT *
FROM Users
WHERE name REGEXP '^A';

This means:

name starts with A.

16. Regex email validation

Now we're approaching SQL 50 #1517.

Suppose the interviewer says:

Find users with valid email addresses.

The classic structure is:

something
@
something
.
something

A regex can describe this much more precisely than LIKE.

For example, a simplified pattern:

WHERE mail REGEXP '^[A-Za-z0-9._-]+@[A-Za-z0-9.-]+\\.[A-Za-z]+$'

Don't memorize this yet.

Understand the structure:

^
↓
start

[A-Za-z0-9._-]+
↓
username

@
↓
literal @

[A-Za-z0-9.-]+
↓
domain

\\.
↓
literal .

[A-Za-z]+
↓
extension

$
↓
end
17. Why ^ and $ matter

Suppose we only write:

REGEXP '@'

That means:

Somewhere in the string, there is an @.

But:

hello@gmail.com

and:

garbage@something

both contain @.

If the question asks whether the whole string follows a pattern, anchors matter:

^
...
$

Think:

^ = start
$ = end
18. SQL 50 #1517 — Find Users With Valid E-Mails

This is our first direct application.

The problem essentially asks for users whose:

email has the required structure
domain is appropriate
username contains permitted characters

This is a regex recognition problem.

So when you see:

valid email

your brain should move toward:

REGEXP

rather than trying to build an enormous collection of LIKE conditions.

19. SQL 50 #1527 — Patients With a Condition

This one is especially interesting because it teaches an important difference.

Suppose a condition column contains medical codes such as:

DIAB1
DIAB2
ABC

and the question asks for patients whose conditions include a particular prefix.

You might initially think:

WHERE conditions LIKE 'DIAB%'

But the actual problem's condition string can contain multiple space-separated codes, and the desired code needs to occur as a complete code rather than merely as an arbitrary substring.

That's where a carefully designed pattern becomes important.

For example, the conceptual pattern is:

start OR space
   ↓
DIAB
   ↓
digits
   ↓
end OR space

This is a classic boundary-aware pattern matching problem.

20. Why naive LIKE can fail

Suppose:

conditions = 'ABC DIAB100 XYZ'

We want to detect:

DIAB100

But imagine:

conditions = 'XDIAB100'

A careless:

LIKE '%DIAB%'

would also match it.

But that's not necessarily the intended medical code.

The lesson:

Don't just ask "Does this text occur?" Ask "Does it occur as the correct token?"

That's a very important interview habit.

21. SQL 50 #1667 — Fix Names in a Table

This one combines:

LOWER()
UPPER()
SUBSTRING()

The desired output is essentially:

First character uppercase, remaining characters lowercase.

Suppose:

name
------
aLICE
bOB
cHARLIE

We want:

Alice
Bob
Charlie

Think in two pieces:

first character
+
remaining characters

First character:

UPPER(LEFT(name, 1))

Remaining:

LOWER(SUBSTRING(name, 2))

Combine:

CONCAT(
    UPPER(LEFT(name, 1)),
    LOWER(SUBSTRING(name, 2))
)

🔥 This is exactly why we're learning functions together, rather than memorizing them individually.

22. Let's dissect #1667

Suppose:

name = 'aLICE'
Step 1
LEFT(name, 1)

→

a
Step 2
UPPER(...)

→

A
Step 3
SUBSTRING(name, 2)

→

LICE
Step 4
LOWER(...)

→

lice
Step 5
CONCAT()

→

Alice

That's the entire problem.

23. This is how you should approach SQL interviews

Don't see:

CONCAT(
    UPPER(LEFT(...)),
    LOWER(SUBSTRING(...))
)

as one giant scary expression.

Break it down:

name
 ↓
first character
 ↓
uppercase
 +
remaining characters
 ↓
lowercase
 ↓
combine

This is expression decomposition.

24. SQL 50 #196 — Delete Duplicate Emails

This problem is slightly different.

It's not primarily a string-function problem.

The important concepts are:

duplicate detection
+
GROUP BY
+
MIN()
+
DELETE

For example, if:

id | email
---|------
1  | a@x.com
2  | a@x.com
3  | b@x.com

we want to keep:

id 1

and remove:

id 2

A common conceptual approach is:

For each email, preserve the smallest ID.

This gives us:

MIN(id)
GROUP BY email

We'll revisit the actual MySQL DELETE formulation separately because deleting from a table while selecting from that same table has MySQL-specific considerations.

25. The string-function map

Memorize this table conceptually:

Interview wording	Function
make lowercase	LOWER()
make uppercase	UPPER()
combine strings	CONCAT()
string length	LENGTH() / CHAR_LENGTH()
remove surrounding spaces	TRIM()
extract middle	SUBSTRING()
first N chars	LEFT()
last N chars	RIGHT()
replace text	REPLACE()
find position	LOCATE()
simple pattern	LIKE
complex pattern	REGEXP
🧠 The interview translation skill

If interviewer says:

"Normalize the name."

You might think:

UPPER()
LOWER()
SUBSTRING()
CONCAT()

"Extract the first three characters."

LEFT(column, 3)

"Get the last four digits."

RIGHT(column, 4)

"Remove hyphens."

REPLACE(column, '-', '')

"Find users whose email follows a pattern."

REGEXP

"Find values containing abc."

LIKE '%abc%'

"Find a token only when it occurs as a complete word/code."

Think:

REGEXP
+
boundaries
🎯 Where we are now

We've essentially completed the major SQL language families:

                 SQL 50 MASTERY

SELECT / WHERE                    ✅
NULL / logic                      ✅
DISTINCT / LIKE / IN / BETWEEN    ✅
ORDER BY                          ✅
JOINs                             ✅
GROUP BY                          ✅
Aggregates                        ✅
HAVING                            ✅
CASE                              ✅
Date functions                    ✅
Window functions                  ✅
CTEs                              ✅
Subqueries                        ✅
EXISTS / NOT EXISTS               ✅
String functions                  🔥
Regex                             🔥

The next phase should not be another giant list of SQL functions.
---
PART 19

🧪 Full Interview Walkthrough

Let's use:

LeetCode #1581 — Customers Who Visited but Did Not Make Any Transactions
Problem idea

We have:

Visits
visit_id	customer_id
1	23
2	9
4	30
5	54
Transactions
transaction_id	visit_id
2	5
3	9

Question:

Find the customers who visited but did not make any transactions, and count how many such visits each customer made.

Step 1 — Don't write SQL yet

First identify the English structure.

The important words are:

visited

and

did not make any transactions

So we need:

Visits
   ↓
Does this visit have a transaction?
   ↓
NO

This immediately tells me:

We need an anti-match.

And from our previous lesson:

NO matching row
        ↓
NOT EXISTS

or:

LEFT JOIN + IS NULL
Step 2 — What is the driving table?

Ask:

What population must appear in the answer?

The question says:

customers who visited

Therefore the driving table is:

Visits

Not Transactions.

This is a very important interview habit.

Step 3 — How are the tables related?

We have:

Visits.visit_id
        ↓
Transactions.visit_id

So:

ON v.visit_id = t.visit_id
Step 4 — Do we need a JOIN?

Yes.

We need to determine whether each visit has a transaction.

I'll use:

LEFT JOIN

Why?

Because we want to keep every visit, including visits that have no matching transaction.

That's exactly what LEFT JOIN does.

Step 5 — Build the JOIN

Start with:

SELECT
    v.customer_id,
    v.visit_id,
    t.transaction_id
FROM Visits v
LEFT JOIN Transactions t
    ON v.visit_id = t.visit_id;

Conceptually:

customer	visit	transaction
23	1	NULL
9	2	NULL
30	4	NULL
54	5	2

Now we can see the unmatched visits.

Step 6 — Filter unmatched rows

We want:

transaction = NULL

Therefore:

WHERE t.transaction_id IS NULL

Full intermediate query:

SELECT
    v.customer_id,
    v.visit_id
FROM Visits v
LEFT JOIN Transactions t
    ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL;

Now we've solved:

Which visits had no transaction?

Step 7 — But the question asks for COUNT

Read the question again:

Count how many such visits each customer made.

So now:

customer
   ↓
GROUP BY
   ↓
COUNT visits

Therefore:

SELECT
    v.customer_id,
    COUNT(*) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t
    ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;

That's the answer.

Step 8 — Now explain the query in English

This is very important for interviews.

Don't just submit:

SELECT ...

Explain it:

"I start from Visits because every relevant record is a visit. I use a LEFT JOIN to Transactions so that visits without transactions are preserved. I filter where the transaction ID is NULL to keep only visits with no transaction. Finally, I group by customer and count those visits."

That's a strong interview explanation.

Step 9 — Now identify the pattern

We just solved:

FILTER
   ↓
LEFT JOIN
   ↓
IS NULL
   ↓
GROUP BY
   ↓
COUNT

So next time you see:

Find X that did not have Y, and count them.

Your brain should immediately consider:

LEFT JOIN ... IS NULL
+
GROUP BY
+
COUNT

That's pattern recognition.

Step 10 — Could we solve it with NOT EXISTS?

Yes.

SELECT
    v.customer_id,
    COUNT(*) AS count_no_trans
FROM Visits v
WHERE NOT EXISTS (
    SELECT 1
    FROM Transactions t
    WHERE t.visit_id = v.visit_id
)
GROUP BY v.customer_id;

Same logical idea:

For each visit:
    Does a transaction exist?
        YES → exclude
        NO  → keep
Step 11 — Which solution would I choose?

For this problem, I'd be comfortable with either.

LEFT JOIN
LEFT JOIN ... IS NULL

is very visual:

match → data
no match → NULL
NOT EXISTS
NOT EXISTS (...)

expresses the business question directly:

There does not exist a transaction for this visit.

Both are valuable patterns to know.

🧠 Notice what we DIDN'T do

We didn't start by thinking:

"Which SQL function should I use?"

Instead:

English
  ↓
Relationship
  ↓
Population
  ↓
Matching / non-matching
  ↓
Aggregation
  ↓
SQL

That is the skill we're training now.

🔥 This is how our future sessions will work

For every SQL 50 problem, we'll go through this pipeline:

① Understand the English

What exactly is being requested?

↓

② Identify the tables

Which table is the driving table?

↓

③ Identify relationships

What columns connect the tables?

↓

④ Identify the operation

Is it:

FILTER?
JOIN?
ANTI-JOIN?
GROUP?
RANK?
COMPARE?

↓

⑤ Build the query skeleton

For example:

SELECT ...
FROM ...
LEFT JOIN ...
WHERE ...
GROUP BY ...

↓

⑥ Fill in the details

Functions, conditions, columns, etc.

↓

⑦ Test mentally against sample rows

Ask:

Why does this row appear?

Why does this row disappear?

↓

⑧ Explain it like an interviewer

One or two sentences describing the strategy.

↓

⑨ Look for an alternative solution

For example:

LEFT JOIN
vs
NOT EXISTS

↓

⑩ Extract the reusable pattern

So the next problem becomes easier.

🎯 And eventually I'll stop helping

At first:

ME → 80%
YOU → 20%

Then:

ME → 50%
YOU → 50%

Then:

ME → 20%
YOU → 80%

Eventually:

Here's the problem. Talk me through your approach.

You give me the approach.

I'll act like the interviewer and challenge it:

Why LEFT JOIN?

Why not INNER JOIN?

What happens with NULL?

Could duplicates occur?

Why COUNT(*) instead of COUNT(column)?

What happens if a customer has multiple transactions?

That's where your interview instincts will develop.

🚀 One important change from our previous learning style

We have already covered the SQL toolbox:

SELECT
WHERE
JOIN
GROUP BY
HAVING
CASE
DATES
WINDOWS
CTEs
SUBQUERIES
EXISTS
REGEX
STRING FUNCTIONS

So from this point, we're going to emphasize:

"Given this English question, which tools should I combine?"

rather than:

"Here's another SQL function."

That's the transition from learning SQL → solving SQL.

---

PART 20

🚀 SQL 50 Interview Mode — #1757

We're going to do exactly what we agreed: I tell you everything for this walkthrough, but I’ll show you how an interviewer expects you to think, not just dump the query.

Problem #1757 — Recyclable and Low Fat Products

You have a table:

Products
product_id	low_fats	recyclable
0	Y	N
1	Y	Y
2	N	Y
3	Y	Y

The question is:

Find the IDs of products that are both low fat and recyclable.

Expected result:

1
3
🧠 Step 1 — Translate the English

The key phrase is:

both low fat and recyclable.

Whenever you hear:

A AND B

think:

WHERE condition_A
  AND condition_B

So immediately:

low_fats = 'Y'
        AND
recyclable = 'Y'
Step 2 — Which table?

Only one table is involved:

Products

Therefore:

FROM Products

No JOIN.

No subquery.

No GROUP BY.

No aggregation.

This is important.

A common beginner mistake is trying to make simple problems complicated.

Step 3 — What columns do we return?

The question asks:

Find the IDs.

Therefore:

SELECT product_id

Not:

SELECT *

We should return exactly what the problem asks for.

Step 4 — Construct the WHERE

First condition:

low_fats = 'Y'

Second:

recyclable = 'Y'

Because both must be true:

WHERE low_fats = 'Y'
  AND recyclable = 'Y'
Step 5 — Final answer
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';

That's it.

🔍 Let's execute it mentally

Original:

product_id	low_fats	recyclable
0	Y	N
1	Y	Y
2	N	Y
3	Y	Y
Product 0
low_fats = Y       → TRUE
recyclable = Y     → FALSE

TRUE AND FALSE
→ FALSE

❌ Exclude.

Product 1
low_fats = Y       → TRUE
recyclable = Y     → TRUE

TRUE AND TRUE
→ TRUE

✅ Include.

Product 2
low_fats = Y       → FALSE
recyclable = Y     → TRUE

FALSE AND TRUE
→ FALSE

❌ Exclude.

Product 3
low_fats = Y       → TRUE
recyclable = Y     → TRUE

TRUE AND TRUE
→ TRUE

✅ Include.

Result:

1
3
🎯 What did we actually learn?

The query is tiny.

But the pattern is important:

Question
   ↓
"both A and B"
   ↓
WHERE
   ↓
A AND B

This is one of the most fundamental SQL interview translations.

🧩 Interviewer's follow-up #1
"Why didn't you use OR?"

Because:

A OR B

means at least one condition is true.

But the problem says:

both

Therefore:

A AND B
Example
A	B	A AND B	A OR B
TRUE	TRUE	TRUE	TRUE
TRUE	FALSE	FALSE	TRUE
FALSE	TRUE	FALSE	TRUE
FALSE	FALSE	FALSE	FALSE

So:

AND → both
OR  → at least one
🧩 Interviewer's follow-up #2
"Could you write this using WHERE low_fats = 'Y' AND recyclable = 'Y'?"

Yes.

That's exactly the correct solution.

There is no reason to introduce:

CASE
GROUP BY
HAVING
JOIN
subquery
window function

The best SQL is often the simplest SQL that expresses the requirement.

🧩 Interviewer's follow-up #3
"What if low_fats is NULL?"

This is where our earlier three-valued logic lesson becomes useful.

Suppose:

low_fats = NULL
recyclable = 'Y'

Then:

low_fats = 'Y'

is:

UNKNOWN

So:

UNKNOWN AND TRUE

is:

UNKNOWN

A WHERE clause keeps rows only when the condition evaluates to TRUE.

Therefore the row is excluded.

This is why understanding NULL matters even in a beginner problem.

🧠 Interview pattern extracted

When you see:

Find records where A and B

your first thought should be:

SELECT ...
FROM ...
WHERE A
  AND B;
🔥 Now let's make it slightly harder
#584 — Find Customer Referee

Table:

Customer
id	name	referee_id
1	Will	NULL
2	Jane	NULL
3	Alex	2
4	Bill	NULL
5	Zack	1
6	Mark	2

Question:

Find the names of customers who were not referred by customer 2.

Step 1 — Translate the English

We want:

referee_id != 2

Seems obvious.

So you might write:

WHERE referee_id != 2

But wait. 🚨

We have:

NULL

Remember our earlier lesson.

For:

NULL != 2

the result isn't TRUE.

It's:

UNKNOWN

Therefore a simple:

WHERE referee_id != 2

will not include customers whose referee is NULL.

But the problem wants customers who were not referred by customer 2.

A customer with no referee qualifies.

So we need:

WHERE referee_id <> 2
   OR referee_id IS NULL
Final #584
SELECT name
FROM Customer
WHERE referee_id <> 2
   OR referee_id IS NULL;

Result:

Will
Jane
Bill
Zack

Let's verify.

name	referee_id	qualifies?
Will	NULL	✅
Jane	NULL	✅
Alex	2	❌
Bill	NULL	✅
Zack	1	✅
Mark	2	❌
💡 This is an excellent interview trap

The tempting answer is:

SELECT name
FROM Customer
WHERE referee_id <> 2;

But that's incomplete.

Why?

Because:

NULL ≠ 2

doesn't evaluate to TRUE.

It evaluates to UNKNOWN.

Therefore:

WHERE referee_id <> 2

doesn't mean:

"anything except 2, including NULL."

It means:

"values that can be proven to be different from 2."

That distinction is huge in SQL.

🚀 #595 — Big Countries

Now we're going to combine two conditions with OR.

Table:

World
name	continent	area	population	gdp
Afghanistan	Asia	652230	25500100	20343000000
Albania	Europe	28748	2831741	12960000000
Algeria	Africa	2381741	37100000	188681000000
Andorra	Europe	468	78115	3712000000
Angola	Africa	1246700	20609294	100990000000

A country is considered big if:

area >= 3000000
OR
population >= 25000000
Translate the English

area is at least 3 million OR population is at least 25 million.

Therefore:

WHERE area >= 3000000
   OR population >= 25000000

Final:

SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
🧠 Pattern

Now we have:

#1757
"both"
 ↓
AND

#595
"either / or"
 ↓
OR

And:

#584
"not X"
 ↓
<> / !=
+
NULL consideration

These three problems look easy.

But they're teaching you to translate English logical operators into SQL.

🔥 #1148 — Article Views I

Now we get our first slightly more interesting pattern.

Table:

Views
article_id	author_id	viewer_id	view_date
1	3	5	2019-08-01
1	3	6	2019-08-02
2	7	7	2019-08-01
2	7	6	2019-08-02
4	7	1	2019-07-22
3	4	4	2019-07-21
3	4	4	2019-07-21

Question:

Find all authors who viewed at least one of their own articles.

Step 1 — Translate

"author viewed their own article."

That means:

author_id = viewer_id

So:

WHERE author_id = viewer_id
Step 2 — What about duplicates?

Article 3 has:

author_id = 4
viewer_id = 4

twice.

But we only want each author once.

Therefore:

DISTINCT
Final
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
🧠 Pattern extracted

This problem teaches:

"same value in two columns"
          ↓
column1 = column2

and:

"each person only once"
          ↓
DISTINCT

So:

#1148
same-column comparison
+
DISTINCT
🔥 #1683 — Invalid Tweets

Now we use our string chapter.

Table:

Tweets

with:

tweet_id
content

A tweet is invalid if its content has more than 15 characters.

Step 1 — Translate

more than 15 characters

We need a string-length function.

LENGTH(content)

So:

WHERE LENGTH(content) > 15
Final
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
🚨 Interview detail

Remember:

LENGTH()

in MySQL measures bytes, while:

CHAR_LENGTH()

measures characters.

For the LeetCode data here, LENGTH() is the expected/simple solution.

But if an interviewer asks:

"What is the difference between LENGTH() and CHAR_LENGTH() in MySQL?"

You should know it.

🎯 Look at what we just did

Five problems:

Problem	Core pattern
#1757	WHERE + AND
#584	NULL + <> + OR
#595	WHERE + OR
#1148	DISTINCT + column comparison
#1683	LENGTH() + WHERE

Notice something?

We didn't learn five unrelated solutions.

We learned five reusable patterns.

🧠 THIS is how I want you to think

When an interviewer gives you:

Find products that are both recyclable and low fat.

Don't think:

"What's the LeetCode solution?"

Think:

One table
↓
Need filtering
↓
Both conditions
↓
AND

When they say:

Find users who have no matching record.

Think:

No matching row
↓
NOT EXISTS
or
LEFT JOIN + IS NULL

When they say:

Return each person once.

Think:

DISTINCT

When they say:

More than 15 characters.

Think:

LENGTH()

When they say:

Either A or B.

Think:

OR
🏆 The real goal

We're no longer trying to memorize:

50 LeetCode answers

We're trying to build this mapping in your brain:

English requirement
       ↓
SQL concept
       ↓
SQL pattern
       ↓
Query

For example:

"both"
   ↓
AND
   ↓
WHERE A AND B
"either"
   ↓
OR
   ↓
WHERE A OR B
"not X"
   ↓
<> / NOT
   ↓
NULL consideration
"each once"
   ↓
DISTINCT
"no matching record"
   ↓
NOT EXISTS
or
LEFT JOIN + IS NULL
"at least N"
   ↓
GROUP BY + HAVING
"top N per group"
   ↓
Window function
"latest record before date"
   ↓
MAX / ROW_NUMBER / correlated logic
"every product"
   ↓
COUNT comparison
or
NOT EXISTS missing item

---
part 21 
Absolutely. We’ll pause the interview-mode exercises and return to the structured learning flow.

We’ve already covered the string/regex chapter, so the next logical step is:

🔥 Next Lesson: Advanced GROUP BY + Aggregation Patterns

This is one of the most important parts of SQL because it changes the question from:

"Which rows satisfy this condition?"

to:

"What can I calculate about groups of rows?"

And this is where many SQL interview questions start becoming genuinely interesting.

1. First, the core idea

Suppose we have:

Employee
employee_id	department	salary
1	Engineering	80000
2	Engineering	90000
3	HR	60000
4	HR	70000
5	Sales	50000

Without grouping:

SELECT *
FROM Employee;

we're working with individual rows.

But suppose the interviewer asks:

What is the average salary in each department?

Now the question is about groups.

Engineering → 80000, 90000
HR          → 60000, 70000
Sales       → 50000

We need:

GROUP BY department
2. GROUP BY
SELECT department
FROM Employee
GROUP BY department;

Result:

Engineering
HR
Sales

Think:

GROUP BY department
        ↓
put rows with the same department together
3. GROUP BY + aggregate

Now:

SELECT
    department,
    AVG(salary) AS avg_salary
FROM Employee
GROUP BY department;

Result:

department	avg_salary
Engineering	85000
HR	65000
Sales	50000

The mental model is:

FROM
 ↓
rows
 ↓
GROUP BY
 ↓
groups
 ↓
aggregate each group
 ↓
result
4. The five aggregate functions you should know cold
COUNT()

How many?

COUNT(*)

Example:

SELECT department, COUNT(*)
FROM Employee
GROUP BY department;
SUM()

Total:

SUM(salary)
AVG()

Average:

AVG(salary)
MIN()

Smallest:

MIN(salary)
MAX()

Largest:

MAX(salary)

These five are fundamental:

COUNT
SUM
AVG
MIN
MAX
5. COUNT(*) vs COUNT(column) ⚠️

This is an interview favorite.

Suppose:

id	bonus
1	1000
2	NULL
3	2000
COUNT(*)
SELECT COUNT(*)
FROM Employee;

Result:

3

It counts rows.

COUNT(bonus)
SELECT COUNT(bonus)
FROM Employee;

Result:

2

Because COUNT(column) ignores NULL.

So remember:

COUNT(*)       → rows
COUNT(column)  → non-NULL values
6. COUNT(DISTINCT ...)

Now suppose:

customer_id	product
1	Phone
1	Laptop
1	Phone
2	Phone

Question:

How many different products did each customer buy?

We need:

SELECT
    customer_id,
    COUNT(DISTINCT product) AS product_count
FROM Purchases
GROUP BY customer_id;

For customer 1:

Phone
Laptop
Phone

Distinct:

Phone
Laptop

→ 2

7. This directly connects to SQL 50 #1045

Customers Who Bought All Products

Remember the idea from earlier:

Which customers bought every product?

The powerful pattern is:

GROUP BY customer_id

and then:

COUNT(DISTINCT product_key)

compared with:

COUNT(products)

Conceptually:

customer's distinct products
          =
all available products

Then the customer bought everything.

This is a very important "ALL" pattern.

8. WHERE vs HAVING

This distinction must become automatic.

Suppose:

Find departments whose average salary is greater than 70,000.

You cannot use:

WHERE AVG(salary) > 70000

because WHERE operates before grouping.

Instead:

SELECT
    department,
    AVG(salary) AS avg_salary
FROM Employee
GROUP BY department
HAVING AVG(salary) > 70000;
9. The mental difference
WHERE

Filters rows.

rows
 ↓
WHERE
 ↓
remaining rows
 ↓
GROUP BY
HAVING

Filters groups.

rows
 ↓
GROUP BY
 ↓
groups
 ↓
HAVING
 ↓
remaining groups

This is one of the most important SQL concepts.

10. Example

Suppose:

employee	department	salary
A	Engineering	100000
B	Engineering	80000
C	Engineering	60000
D	HR	50000
E	HR	40000

Question:

Find departments whose average salary is greater than 70k.

SELECT
    department,
    AVG(salary) AS avg_salary
FROM Employee
GROUP BY department
HAVING AVG(salary) > 70000;

Engineering:

(100000 + 80000 + 60000) / 3
= 80000

✅ Keep.

HR:

(50000 + 40000) / 2
= 45000

❌ Remove.

11. The SQL execution mental model

For interviews, think approximately:

FROM
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY
  ↓
LIMIT

This explains many SQL rules.

For example:

WHERE AVG(salary) > 70000

doesn't make sense because the average hasn't been computed yet.

The groups haven't been formed.

12. Multiple columns in GROUP BY

Suppose:

department	gender	salary
Engineering	M	80000
Engineering	F	90000
Engineering	M	70000
HR	F	60000

Question:

Average salary by department and gender.

SELECT
    department,
    gender,
    AVG(salary)
FROM Employee
GROUP BY department, gender;

Now each group is defined by the combination:

(department, gender)

So:

Engineering + M
Engineering + F
HR + F

are separate groups.

13. A very important interview pattern

Whenever you hear:

"for each X"

think:

GROUP BY X

Examples:

Average salary for each department

GROUP BY department

Number of orders for each customer

GROUP BY customer_id

Number of products for each category

GROUP BY category

Maximum salary for each department

GROUP BY department

This translation should become automatic.

14. GROUP BY + COUNT

Question:

Find classes with at least 5 students.

This is SQL 50 #596.

English:

classes
 ↓
count students
 ↓
at least 5

SQL pattern:

SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(*) >= 5;

Notice the crucial point:

"at least 5 students"
        ↓
COUNT(*)
        ↓
HAVING >= 5
15. Why HAVING, not WHERE?

Because:

COUNT(*)

is an aggregate.

We're asking about the group's count, not an individual student's row.

Therefore:

HAVING COUNT(*) >= 5

is correct.

16. SQL 50 #1729 — Find Followers Count

Question:

Find the number of followers for each user.

We have something like:

user_id | follower_id

We want:

user_id → number of followers

Pattern:

SELECT
    user_id,
    COUNT(*) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;

Again:

for each user

→

GROUP BY user_id
17. SQL 50 #619 — Biggest Single Number

This one introduces an interesting aggregation pattern.

Question:

Find the biggest number that appears exactly once.

Suppose:

num
8
8
3
7
7
5

First identify numbers appearing once:

3
5

Then choose the largest:

5

Conceptually:

GROUP BY num
 ↓
COUNT(*) = 1
 ↓
MAX()

A common solution:

SELECT MAX(num) AS num
FROM MyNumbers
WHERE num IN (
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING COUNT(*) = 1
);

This is a beautiful example of combining:

GROUP BY
+
HAVING
+
subquery
+
MAX
18. This is the next level we're targeting

We're moving from:

Simple filtering

to:

Aggregation

to:

Aggregation + filtering groups

to:

Aggregation + subqueries

to:

Aggregation + windows

That's the progression toward the Medium/Hard SQL 50 problems.

🧠 The pattern library is growing

You should now have these mental translations:

English	SQL pattern
both	AND
either	OR
not equal	<> / !=
missing	IS NULL
each X	GROUP BY X
how many	COUNT()
total	SUM()
average	AVG()
largest	MAX()
smallest	MIN()
unique count	COUNT(DISTINCT ...)
at least N per group	HAVING COUNT(...) >= N
group average condition	HAVING AVG(...) ...
no matching row	NOT EXISTS / LEFT JOIN ... IS NULL
all	often COUNT comparison / NOT EXISTS
🔥 One crucial warning

Don't confuse:

WHERE

with:

HAVING

Think:

WHERE

Which rows should participate?

HAVING

Which groups should survive?

Example:

SELECT department, AVG(salary)
FROM Employee
WHERE salary > 50000
GROUP BY department
HAVING AVG(salary) > 70000;

This means:

Remove employees earning ≤ 50k.
Group remaining employees by department.
Calculate average salary.
Keep departments whose resulting average > 70k.

That's a very powerful pattern.
---
part 22

🔥 Next Lesson: Conditional Aggregation

This is a major milestone in your SQL learning.

You already know:

GROUP BY
COUNT()
SUM()
AVG()
MIN()
MAX()
HAVING

Now we're going to learn how to make aggregates answer questions like:

"How many were successful?"

"How many were cancelled?"

"What percentage were approved?"

"How many users did X but not Y?"

The core technique is:

CASE WHEN + COUNT/SUM

This pattern unlocks a huge part of SQL 50.

1. First: What is conditional aggregation?

Suppose we have:

user	status
A	approved
B	rejected
C	approved
D	approved
E	rejected

Question:

How many users were approved?

One way to think about it:

Look at every row
       ↓
Is status = 'approved'?
       ↓
YES → count it
NO  → don't count it

That's conditional aggregation.

2. CASE WHEN

First learn the smaller piece.

CASE
    WHEN condition THEN result
    ELSE result
END

Example:

SELECT
    name,
    CASE
        WHEN salary >= 100000 THEN 'High'
        ELSE 'Low'
    END AS salary_category
FROM Employee;

Suppose:

name	salary
Alice	120000
Bob	80000
Charlie	150000

Result:

name	salary_category
Alice	High
Bob	Low
Charlie	High
3. Think of CASE as SQL's IF/ELSE

In programming:

if salary >= 100000:
    "High"
else:
    "Low"

SQL:

CASE
    WHEN salary >= 100000 THEN 'High'
    ELSE 'Low'
END

So:

CASE WHEN
   ↓
conditional value
4. Multiple conditions

You can have multiple branches:

CASE
    WHEN salary >= 150000 THEN 'Very High'
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END

Important:

The conditions are evaluated from top to bottom.

So if salary is 160000:

salary >= 150000 → TRUE

SQL returns:

Very High

and doesn't continue checking the later conditions.

5. CASE inside SUM()

Now things get powerful.

Suppose:

user	status
A	approved
B	rejected
C	approved
D	approved
E	rejected

We want:

Number of approved users.

We can write:

SELECT
    SUM(
        CASE
            WHEN status = 'approved' THEN 1
            ELSE 0
        END
    ) AS approved_count
FROM Users;

Let's mentally transform the rows:

approved → 1
rejected → 0
approved → 1
approved → 1
rejected → 0

Then:

1 + 0 + 1 + 1 + 0 = 3

Result:

3
6. This pattern is HUGE

Memorize the shape:

SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)

Meaning:

Count how many rows satisfy this condition.

This is one of the most useful SQL patterns you'll ever learn.

7. COUNT(CASE WHEN ...)

There's another common form:

COUNT(
    CASE
        WHEN status = 'approved' THEN 1
    END
)

Why does this work?

Remember:

COUNT(column)

ignores NULL.

So:

approved → 1
rejected → NULL
approved → 1
approved → 1
rejected → NULL

COUNT() sees:

1
1
1

→ 3.

Therefore:

COUNT(
    CASE WHEN condition THEN 1 END
)

is another way to count rows satisfying a condition.

8. SUM(CASE...) vs COUNT(CASE...)

Both can be useful.

SUM
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
COUNT
COUNT(
    CASE
        WHEN condition THEN 1
    END
)

For beginners, I recommend mentally associating:

SUM(CASE)
    ↓
count condition as 1/0

It's extremely intuitive.

9. Multiple conditional counts in ONE query

This is where things get really powerful.

Suppose:

user	status
A	approved
B	rejected
C	approved
D	pending
E	rejected

We want:

approved count
rejected count
pending count

We don't need three queries.

SELECT
    SUM(CASE WHEN status = 'approved' THEN 1 ELSE 0 END) AS approved,
    SUM(CASE WHEN status = 'rejected' THEN 1 ELSE 0 END) AS rejected,
    SUM(CASE WHEN status = 'pending' THEN 1 ELSE 0 END) AS pending
FROM Users;

Result:

approved	rejected	pending
2	2	1

🔥 This is conditional aggregation.

10. Why interviewers love this

Imagine the interviewer asks:

For each department, give me the number of employees earning above $100k and the number earning below $50k.

You can do:

SELECT
    department,
    SUM(
        CASE
            WHEN salary > 100000 THEN 1
            ELSE 0
        END
    ) AS high_salary,
    SUM(
        CASE
            WHEN salary < 50000 THEN 1
            ELSE 0
        END
    ) AS low_salary
FROM Employee
GROUP BY department;

Now you're combining:

GROUP BY
+
CASE
+
SUM

This is a very common interview pattern.

11. Conditional aggregation + GROUP BY

Suppose:

department	status
Engineering	active
Engineering	active
Engineering	inactive
HR	active
HR	inactive
HR	inactive

Question:

For each department, how many employees are active?

SELECT
    department,
    SUM(
        CASE
            WHEN status = 'active' THEN 1
            ELSE 0
        END
    ) AS active_count
FROM Employee
GROUP BY department;

Result:

department	active_count
Engineering	2
HR	1

Mental model:

GROUP BY department
       ↓
create department groups
       ↓
within each group
       ↓
CASE checks each row
       ↓
SUM the 1s
12. Now percentages 🔥

This is where SQL 50 becomes much more interesting.

Suppose:

status
success
success
failed
success
failed

Question:

What percentage of requests were successful?

We need:

successful requests
------------------- × 100
total requests

SQL:

SELECT
    100.0 *
    SUM(CASE WHEN status = 'success' THEN 1 ELSE 0 END)
    / COUNT(*) AS success_percentage
FROM Requests;

Important:

numerator
    ↓
conditional count

denominator
    ↓
total count
13. Why 100.0 instead of 100?

Depending on the expression and data types, using a decimal value helps ensure you don't accidentally perform integer-style division.

So:

100.0 * ...

is a useful habit when calculating percentages.

14. SQL 50 #1633
Percentage of Users Attended a Contest

This is a direct application.

Conceptually we need:

users who attended contest
--------------------------- × 100
total users

For each contest:

GROUP BY contest_id

Then:

COUNT(DISTINCT user_id)

gives the number of participants.

The denominator comes from total users.

Conceptually:

SELECT
    contest_id,
    ROUND(
        100.0 * COUNT(DISTINCT user_id)
        / (SELECT COUNT(*) FROM Users),
        2
    ) AS percentage
FROM Register
GROUP BY contest_id;

The important pattern is:

COUNT(DISTINCT)
+
GROUP BY
+
percentage
+
subquery denominator
15. Why COUNT(DISTINCT)?

Suppose:

contest	user
1	A
1	A
1	B

If we use:

COUNT(user)

we get:

3

But there are only:

A
B

two unique users.

Therefore:

COUNT(DISTINCT user_id)

→ 2.

Whenever the English says:

unique users

think:

COUNT(DISTINCT user_id)
16. SQL 50 #1211 — Queries Quality and Percentage

This is another conditional aggregation problem.

The question involves calculating things like:

How many queries have a particular property?

and:

What percentage satisfy that property?

The underlying pattern is:

GROUP BY query_name
       ↓
calculate aggregates
       ↓
conditional count / average
       ↓
percentage

For example, if "poor query" means:

rating < 3

then:

SUM(
    CASE
        WHEN rating < 3 THEN 1
        ELSE 0
    END
)

counts poor queries.

And:

100.0 *
SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END)
/
COUNT(*)

gives their percentage.

17. Conditional AVG()

Here's another beautiful trick.

Suppose:

Find the average salary of employees whose salary is above 100k.

You could filter:

SELECT AVG(salary)
FROM Employee
WHERE salary > 100000;

But conditional aggregation allows:

SELECT
    AVG(
        CASE
            WHEN salary > 100000 THEN salary
        END
    )
FROM Employee;

Why?

For employees below 100k:

CASE → NULL

And:

AVG()

ignores NULL.

So only qualifying salaries participate.

18. Conditional SUM()

Suppose:

Calculate total revenue from completed orders.

SELECT
    SUM(
        CASE
            WHEN status = 'completed'
            THEN amount
            ELSE 0
        END
    ) AS completed_revenue
FROM Orders;

Example:

status	amount
completed	100
cancelled	200
completed	300

Becomes:

100
0
300

→

400
19. Conditional aggregation is basically "multiple questions in one scan"

This is the big idea.

Suppose the interviewer asks:

For every department, show:

total employees
active employees
inactive employees
employees earning over 100k

We can do:

SELECT
    department,

    COUNT(*) AS total_employees,

    SUM(
        CASE
            WHEN status = 'active' THEN 1
            ELSE 0
        END
    ) AS active_employees,

    SUM(
        CASE
            WHEN status = 'inactive' THEN 1
            ELSE 0
        END
    ) AS inactive_employees,

    SUM(
        CASE
            WHEN salary > 100000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees

FROM Employee
GROUP BY department;

One grouped query gives us four different metrics.

That's why this technique is so valuable.

20. CASE inside ORDER BY

Another useful application:

ORDER BY
    CASE
        WHEN status = 'urgent' THEN 1
        WHEN status = 'normal' THEN 2
        ELSE 3
    END;

This allows custom ordering.

For example:

urgent
normal
everything else

rather than alphabetical ordering.

21. CASE inside WHERE

You can use CASE, but don't automatically reach for it.

For example:

WHERE
    CASE
        WHEN type = 'A' THEN value_a
        ELSE value_b
    END > 100

Sometimes that's useful.

But frequently a normal boolean condition is clearer.

Use CASE primarily when you're producing a value, categorizing, or conditionally aggregating.

22. The critical distinction

These are different:

Filtering rows
WHERE status = 'active'

This removes rows.

Categorizing rows
CASE
    WHEN status = 'active' THEN 'A'
    ELSE 'I'
END

This creates a value.

Conditional aggregation
SUM(
    CASE
        WHEN status = 'active' THEN 1
        ELSE 0
    END
)

This converts the condition into a number that can be aggregated.

23. A powerful mental transformation

Whenever you see:

Count rows satisfying condition X

translate it to:

SUM(
    CASE
        WHEN X THEN 1
        ELSE 0
    END
)

Whenever you see:

Percentage of rows satisfying X

translate it to:

conditional count
-----------------
total count

Whenever you see:

For each X

add:

GROUP BY X

Put those together and you can solve a huge class of interview questions.

24. SQL 50 #1193 — Monthly Transactions I

This problem is an excellent combination of:

DATE
+
GROUP BY
+
conditional aggregation

The question asks for monthly statistics such as:

total transactions
approved transactions
total amount
approved amount

The conceptual structure is:

GROUP BY month

Then calculate:

total transactions
        ↓
COUNT

approved transactions
        ↓
SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END)

total amount
        ↓
SUM(amount)

approved amount
        ↓
SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END)

This is an extremely important interview pattern.

25. The structure

Conceptually:

SELECT
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,

    COUNT(*) AS trans_count,

    SUM(
        CASE
            WHEN state = 'approved' THEN 1
            ELSE 0
        END
    ) AS approved_count,

    SUM(amount) AS trans_total_amount,

    SUM(
        CASE
            WHEN state = 'approved' THEN amount
            ELSE 0
        END
    ) AS approved_total_amount

FROM Transactions

GROUP BY
    DATE_FORMAT(trans_date, '%Y-%m'),
    country;

🔥 This one query combines almost everything we've learned so far.

26. Notice something important

The CASE expression doesn't always return 1.

It can return the actual value we want to aggregate.

For counting:

CASE WHEN condition THEN 1 ELSE 0 END

For conditional revenue:

CASE WHEN condition THEN amount ELSE 0 END

So:

CASE
 ↓
conditional value
 ↓
aggregate
27. CASE + COUNT + SUM cheat sheet
Conditional count
SUM(CASE WHEN condition THEN 1 ELSE 0 END)
Conditional sum
SUM(CASE WHEN condition THEN amount ELSE 0 END)
Conditional average
AVG(CASE WHEN condition THEN amount END)
Conditional existence/count of non-null values
COUNT(CASE WHEN condition THEN 1 END)
🧠 The pattern you should now have
"for each department"
        ↓
GROUP BY department

"how many"
        ↓
COUNT / SUM(CASE)

"how many satisfy X"
        ↓
SUM(CASE WHEN X THEN 1 ELSE 0 END)

"total amount satisfying X"
        ↓
SUM(CASE WHEN X THEN amount ELSE 0 END)

"percentage satisfying X"
        ↓
conditional count / total count

"unique users"
        ↓
COUNT(DISTINCT user_id)
🎯 Where we are in the learning track

Our progression is now:

DATABASE FUNDAMENTALS                 ✅
Keys / Constraints / NULL             ✅

SELECT / WHERE                        ✅
DISTINCT / LIKE / IN / BETWEEN        ✅
ORDER BY                              ✅

JOINs                                 ✅
INNER / LEFT / SELF JOIN              ✅

GROUP BY                              ✅
COUNT / SUM / AVG / MIN / MAX         ✅
HAVING                                ✅

CASE WHEN                             ✅
CONDITIONAL AGGREGATION               🔥 NOW

And we're about to enter another very important chapter:

📅 Date & Time SQL

We'll systematically learn:

YEAR()
MONTH()
DAY()
DATE()
DATEDIFF()
TIMESTAMPDIFF()
DATE_ADD()
DATE_SUB()
DATE_FORMAT()
LAST_DAY()

Then combine them with:

GROUP BY
CASE
aggregation
---
part 23

Absolutely. Let's continue systematically.

The next chapter is:

📅 MySQL Date & Time Functions

Dates are extremely important for SQL interviews because real-world data is full of questions like:

"How many transactions happened in each month?"
"What happened in the last 30 days?"
"Find users who returned the next day."
"Calculate the number of days between two events."
"Find the first/most recent event."
"Group sales by month."
"Find records within a date range."

And several SQL 50 problems depend heavily on these patterns.

1. First: MySQL date/time data types

The two you'll encounter most often are:

DATE

Stores a calendar date:

2026-08-25
DATETIME

Stores date + time:

2026-08-25 14:30:45

You may also encounter TIMESTAMP, but for our SQL 50 preparation, focus heavily on understanding DATE and DATETIME.

2. Extracting parts of a date

Suppose:

2026-08-25

We can extract:

YEAR(date_column)

→

2026
MONTH(date_column)

→

8
DAY(date_column)

→

25

Example:

SELECT
    YEAR(order_date) AS year,
    MONTH(order_date) AS month
FROM Orders;
3. Why this matters for GROUP BY

Suppose we have:

order_date	amount
2026-01-03	100
2026-01-15	200
2026-02-04	150
2026-02-20	300

Question:

Total sales for each month.

We want:

January → 300
February → 450

We could group by:

GROUP BY YEAR(order_date), MONTH(order_date)

For example:

SELECT
    YEAR(order_date) AS year,
    MONTH(order_date) AS month,
    SUM(amount) AS total_sales
FROM Orders
GROUP BY
    YEAR(order_date),
    MONTH(order_date);
4. Why YEAR + MONTH together?

Imagine:

2025-01
2026-01

Both have:

MONTH() = 1

If you group only by:

GROUP BY MONTH(order_date)

you accidentally combine January 2025 and January 2026.

So when your data spans multiple years:

GROUP BY YEAR(date), MONTH(date)

is important.

5. DATE_FORMAT()

MySQL gives us another extremely useful function:

DATE_FORMAT(date_column, format)

For example:

DATE_FORMAT(order_date, '%Y-%m')

turns:

2026-08-25

into:

2026-08

This is particularly useful when the output needs a year-month string.

6. Important format codes

You should know these:

Format	Meaning	Example
%Y	4-digit year	2026
%y	2-digit year	26
%m	month 01-12	08
%d	day 01-31	25
%H	hour	14
%i	minute	30
%s	second	45

So:

DATE_FORMAT(order_date, '%Y-%m')

→

2026-08

And:

DATE_FORMAT(order_date, '%Y-%m-%d')

→

2026-08-25
7. SQL 50 #1193 — Monthly Transactions I

Now we can understand the date component of this problem.

The requirement asks for monthly transaction statistics.

The first transformation is:

DATE_FORMAT(trans_date, '%Y-%m')

That gives us:

2020-01
2020-01
2020-02
2020-02

Then:

GROUP BY
    DATE_FORMAT(trans_date, '%Y-%m')

Now every transaction in the same month belongs to the same group.

Then we apply the conditional aggregation we just learned.

The overall mental model is:

trans_date
    ↓
YEAR-MONTH
    ↓
GROUP BY
    ↓
COUNT / SUM / CASE

This is exactly why we learned conditional aggregation before dates.

8. Date comparisons

Dates can be compared directly.

Suppose:

order_date = '2026-08-20'

You can write:

WHERE order_date >= '2026-08-01'

or:

WHERE order_date < '2026-09-01'

This is often preferable to wrapping the column in a function.

For example, to get August 2026:

WHERE order_date >= '2026-08-01'
  AND order_date < '2026-09-01'
9. Why this pattern is powerful

You might be tempted to write:

WHERE YEAR(order_date) = 2026
  AND MONTH(order_date) = 8

That can express the idea, but a range condition is often preferable for querying indexed date columns:

WHERE order_date >= '2026-08-01'
  AND order_date < '2026-09-01'

This is an important interview + practical SQL distinction.

10. BETWEEN

For dates:

WHERE order_date BETWEEN '2026-08-01' AND '2026-08-31'

can be useful with a DATE column.

But be careful with DATETIME.

Suppose:

2026-08-31 18:30:00

If you write:

BETWEEN '2026-08-01' AND '2026-08-31'

the upper bound effectively corresponds to midnight at the start of August 31, so later times on August 31 may be excluded.

For DATETIME, the safer pattern is often:

WHERE event_time >= '2026-08-01'
  AND event_time < '2026-09-01'

This half-open interval pattern is worth remembering.

11. DATEDIFF()

Now we move from:

"What date is this?"

to:

"How far apart are these dates?"

Use:

DATEDIFF(date1, date2)

It returns the difference in days.

Example:

SELECT DATEDIFF('2026-08-25', '2026-08-20');

Result:

5

Conceptually:

Aug 20
 ↓
Aug 25

5 days
12. Important: DATEDIFF() ignores the time portion

For example, conceptually:

2026-08-25 23:59:00
2026-08-24 00:01:00

DATEDIFF() is concerned with the date difference, not the precise elapsed hours.

If you need a precise difference in units such as hours or minutes, another function becomes useful.

13. TIMESTAMPDIFF()

Syntax:

TIMESTAMPDIFF(unit, start, end)

Examples:

TIMESTAMPDIFF(DAY, start_time, end_time)
TIMESTAMPDIFF(HOUR, start_time, end_time)
TIMESTAMPDIFF(MINUTE, start_time, end_time)
TIMESTAMPDIFF(SECOND, start_time, end_time)

This is useful when an interview question says:

How many hours did this process take?

or:

How many days passed between signup and purchase?

14. Example

Suppose:

start = 2026-08-20 10:00:00
end   = 2026-08-20 14:30:00

Then:

TIMESTAMPDIFF(HOUR, start, end)

returns:

4

And:

TIMESTAMPDIFF(MINUTE, start, end)

returns:

270
15. This directly connects to SQL 50 #1661
Average Time of Process per Machine

This problem has:

machine_id
process_id
activity_type
timestamp

There are typically two relevant events:

start
end

We need:

end timestamp - start timestamp

Conceptually:

process duration
       ↓
TIMESTAMPDIFF()
       ↓
AVG()
       ↓
GROUP BY machine

This is an excellent example of combining concepts.

16. SQL 50 #197 — Rising Temperature

This problem is another important date pattern.

Question essentially asks:

Find days where today's temperature is higher than the previous day.

Notice something:

We need to compare:

today

with:

previous day

This is where we eventually need to learn self joins and window functions.

A classic approach uses a self-join:

Weather w1
   JOIN
Weather w2

where:

w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)

Then compare:

w1.temperature > w2.temperature

We'll return to this problem when we deepen our date + join patterns.

17. DATE_ADD()

To move a date forward:

DATE_ADD(date, INTERVAL value unit)

Example:

DATE_ADD('2026-08-20', INTERVAL 1 DAY)

→

2026-08-21

You can also use:

DATE_ADD(date, INTERVAL 1 MONTH)

or:

DATE_ADD(date, INTERVAL 1 YEAR)
18. DATE_SUB()

Same idea, backwards:

DATE_SUB(date, INTERVAL 1 DAY)

Example:

DATE_SUB('2026-08-20', INTERVAL 7 DAY)

→

2026-08-13

This is extremely useful for questions like:

Find activity in the previous 30 days.

19. The "last N days" pattern

Suppose the current date is represented by:

CURDATE()

Then:

WHERE activity_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)

means:

activity during the last 30 days.

This connects directly to:

SQL 50 #1141 — User Activity for the Past 30 Days I

The important concepts are:

date range
+
DISTINCT
+
GROUP BY
+
COUNT

We'll solve the complete problem later.

20. CURDATE() vs NOW()
CURDATE()

Returns today's date:

2026-08-25
NOW()

Returns current date and time:

2026-08-25 14:30:45

So:

CURDATE()

is appropriate when you care about the calendar date.

And:

NOW()

when you need date + time.

21. LAST_DAY()

Another useful MySQL function:

LAST_DAY(date)

For example:

LAST_DAY('2026-02-10')

→

2026-02-28

This can be useful for month-end calculations.

22. A very important interview pattern: "same day"

Suppose:

2026-08-25 10:00
2026-08-25 18:00

If you need to determine whether two timestamps occurred on the same calendar day, you might compare their date portions.

For example:

DATE(timestamp_column)

returns the date component.

But again, be thoughtful about using functions on indexed columns in filtering conditions.

23. Date functions vs date filtering

This distinction is important.

For displaying/grouping:

Functions are excellent:

DATE_FORMAT(date, '%Y-%m')
For filtering indexed columns:

Prefer appropriate ranges when possible:

WHERE date >= '2026-08-01'
  AND date < '2026-09-01'

This distinction will become more important when we discuss SQL performance.

🧠 Your Date Pattern Library

Start building this mental map:

English	MySQL
extract year	YEAR(date)
extract month	MONTH(date)
extract day	DAY(date)
year-month	DATE_FORMAT(date,'%Y-%m')
difference in days	DATEDIFF()
difference in hours/minutes/etc.	TIMESTAMPDIFF()
add time	DATE_ADD()
subtract time	DATE_SUB()
today	CURDATE()
current date/time	NOW()
month end	LAST_DAY()
format date	DATE_FORMAT()
🔥 The combinations matter more than the functions

Don't memorize these as isolated functions.

Think:

"Monthly report"
DATE_FORMAT
+
GROUP BY
+
COUNT/SUM
"Last 30 days"
CURDATE
+
DATE_SUB
+
WHERE
"Duration"
TIMESTAMPDIFF
+
AVG/SUM
+
GROUP BY
"Previous day"
DATE_ADD / DATE_SUB
+
JOIN
"Percentage by month"
DATE_FORMAT
+
GROUP BY
+
CASE
+
COUNT/SUM
🎯 Where we are now

Our learning track is becoming:

DATABASE BASICS                  ✅
CONSTRAINTS / KEYS / NULL        ✅

SELECT / WHERE                   ✅
DISTINCT / LIKE / IN / BETWEEN   ✅
ORDER BY                         ✅

JOINS                            ✅

GROUP BY                         ✅
AGGREGATES                       ✅
HAVING                           ✅

CASE WHEN                        ✅
CONDITIONAL AGGREGATION          ✅

DATE & TIME                      🔥 CURRENT

And the next major chapter after we finish the date material is:

🪟 Window Functions

This is the big leap.

We'll learn:

ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM() OVER()
AVG() OVER()

And then concepts like:

"Find the top 3 salaries in each department."

"Find the second-highest salary."

"Compare today's value with yesterday's."

"Find each user's first activity."

"Find the running total."

That will directly unlock the harder SQL 50 problems, especially #185 Department Top Three Salaries, #176 Second Highest Salary, and several of the more advanced problems.

So we're right at the point where SQL starts becoming interview-level rather than syntax-level.
---
part 24 - other notes concepts 

📚 NOTES COMPLETION TRACK

We've already done:

✅ Database / DBMS / RDBMS
✅ Tables / rows / columns
✅ Keys / relationships
✅ Constraints
✅ NULL
✅ SELECT / WHERE
✅ Operators
✅ DISTINCT / LIKE / IN / BETWEEN
✅ ORDER BY
✅ GROUP BY / aggregates / HAVING
✅ JOINs
✅ CASE / conditional aggregation
✅ Date basics

Remaining important notes material:

⬜ Data Types
⬜ SQL command categories
⬜ DDL
⬜ INSERT
⬜ UPDATE
⬜ DELETE
⬜ DCL
⬜ TCL / Transactions
⬜ Set Operations
⬜ Views
⬜ Indexes
⬜ Subqueries — systematic notes pass
⬜ Final notes revision

So let's start with the first missing chapter.

🧱 LESSON: MySQL Data Types

Your notes explicitly have a data-types section covering character, numeric, date/time, boolean, bit, and UNSIGNED types.

1. What is a data type?

When we create a table:

CREATE TABLE employees (
    id INT,
    name VARCHAR(50),
    salary DECIMAL(10,2)
);

we are telling MySQL:

"id contains integers."

"name contains strings."

"salary contains decimal numbers."

That's what a data type does.

Think:

COLUMN
  ↓
What kind of value can live here?
  ↓
DATA TYPE
2. The major categories

For our purposes:

MySQL Data Types
│
├── String
│   ├── CHAR
│   ├── VARCHAR
│   └── BLOB
│
├── Numeric
│   ├── INT
│   ├── TINYINT
│   ├── BIGINT
│   ├── BIT
│   ├── FLOAT
│   └── DOUBLE
│
├── Date / Time
│   ├── DATE
│   ├── TIME
│   └── YEAR
│
└── Boolean
    └── BOOLEAN

That's essentially the structure presented in your notes.

3. INT

Stores integers.

age INT

Examples:

10
25
100
-50

Your notes give the signed INT range as:

-2,147,483,648
to
2,147,483,647

Typical usage:

CREATE TABLE employees (
    id INT,
    age INT
);
4. TINYINT

Smaller integer type.

Your notes give its signed range as:

-128 to 127

A common MySQL use is:

is_active TINYINT

where:

1 → true
0 → false
5. BIGINT

For very large integers.

Your notes list its signed range as approximately:

-9.22 quintillion
to
+9.22 quintillion

Typical example:

user_id BIGINT

when IDs can become extremely large.

6. DECIMAL — VERY IMPORTANT FOR INTERVIEWS

Interestingly, your data-type table focuses heavily on FLOAT and DOUBLE, but you have already seen DECIMAL in the notes' table-creation example:

salary DECIMAL(10, 2)

For monetary values, DECIMAL is generally the better choice because it represents fixed-point decimal values exactly.

Example:

price DECIMAL(10,2)

means a value with up to 10 digits total and 2 digits after the decimal.

For example:

99999999.99

can fit.

Interview rule:
Money → DECIMAL

rather than casually using floating-point types.

7. FLOAT vs DOUBLE

Your notes describe:

FLOAT  → decimal number, precision to 23 digits
DOUBLE → decimal number, precision to 24–53 digits

The simple mental model:

FLOAT
  ↓
less precision

DOUBLE
  ↓
more precision

They're floating-point types.

For exact financial calculations, prefer DECIMAL.

8. CHAR

Fixed-length string.

country_code CHAR(2)

If the column is:

CHAR(2)

it is designed for exactly that fixed-width concept.

Your notes summarize:

CHAR = fixed length.

Good mental examples:

country code
fixed-format code
9. VARCHAR

Variable-length string.

name VARCHAR(100)

The actual string can have varying length up to the specified maximum.

Examples:

"Bob"
"Alice"
"Alexander"

Your notes contrast:

CHAR      → fixed length
VARCHAR   → variable length

and note that VARCHAR is generally preferable when the values don't all have the same length.

Interview question:

CHAR vs VARCHAR?

Answer:

CHAR     → fixed-length strings
VARCHAR  → variable-length strings
10. BLOB

BLOB stands for:

Binary Large Object

Your notes include BLOB for binary large objects.

Conceptually:

BLOB
 ↓
binary data

It's different from ordinary textual data.

For our interview preparation, know what it is, but don't spend excessive time memorizing its variants yet.

11. BOOLEAN

Your notes describe:

BOOLEAN → 0 or 1

So:

is_active BOOLEAN

conceptually:

TRUE
FALSE

In MySQL, boolean handling is closely associated with 0 and 1.

12. BIT

Your notes list:

BIT(x)

for storing x-bit values, with x ranging from 1 to 64.

Example:

flags BIT(4)

This is more specialized than the everyday types we'll use in SQL 50.

For now:

BIT → bit-oriented values.

That's enough.

13. DATE

This one is very important.

Format:

YYYY-MM-DD

Example:

2026-08-25

Your notes specify DATE as the date type with the YYYY-MM-DD representation.

Example:

birth_date DATE
14. TIME

Stores time:

HH:MM:SS

Example:

14:30:25

Your notes list:

TIME → HH:MM:SS

15. YEAR

Stores a year.

Example:

birth_year YEAR

Your notes describe the four-digit YEAR type and its supported range.

16. UNSIGNED

This is an important little concept.

Your notes explicitly mention that numeric data types can be declared UNSIGNED when only positive values are needed.

Example:

age INT UNSIGNED

Conceptually:

INT
↓
can represent negative + positive

INT UNSIGNED
↓
only non-negative values

This gives more range on the positive side.

🧠 Data Types — Interview Cheat Sheet
Type	Think
INT	normal integer
BIGINT	very large integer
TINYINT	small integer
DECIMAL	exact decimal / money
FLOAT	floating-point
DOUBLE	higher-precision floating-point
CHAR	fixed-length string
VARCHAR	variable-length string
BLOB	binary large object
BOOLEAN	true/false concept
BIT	bit values
DATE	calendar date
TIME	time
YEAR	year
UNSIGNED	non-negative numeric range
🎯 Interview questions you should be able to answer
Q1. CHAR vs VARCHAR?
CHAR → fixed length
VARCHAR → variable length
Q2. What should you generally use for money?
DECIMAL
Q3. INT vs BIGINT?
BIGINT supports a much larger integer range.
Q4. What does UNSIGNED mean?
The numeric type does not store negative values,
allowing a larger non-negative range.
Q5. DATE format?
YYYY-MM-DD
✅ Data Types: DONE

We don't need to over-study this chapter.

You need to recognize the types and know when/why they're used, not memorize every MySQL storage byte and obscure edge case.

🚀 NEXT: SQL COMMAND CATEGORIES

Now we move to the next missing section from your notes:

                    SQL
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
      DDL            DQL           DML
       │             │             │
 CREATE/ALTER      SELECT       INSERT/UPDATE
 DROP/TRUNCATE                    /DELETE
       │
       └──────────────┬──────────────┐
                      ↓              ↓
                     DCL             TCL
                      │               │
                 GRANT/REVOKE   COMMIT/ROLLBACK
                                  SAVEPOINT

Your notes explicitly lay out these five categories and their commands.

---
part 25
🚀 Lesson: DDL — Data Definition Language

Good. We're now following the notes exactly, filling the gaps rather than jumping ahead.

Your notes define DDL as the part of SQL used to create, modify, and delete database objects such as tables and indexes. They list CREATE, ALTER, DROP, RENAME, and TRUNCATE as the key DDL commands.

1. First: What does DDL mean?

DDL = Data Definition Language

The key word is:

Definition

DDL deals primarily with the structure/schema of the database.

Think:

DDL
 │
 ├── CREATE
 ├── ALTER
 ├── DROP
 ├── RENAME
 └── TRUNCATE

Compare that with what we've already learned:

DQL
 └── SELECT       → retrieve data

DML
 ├── INSERT       → add data
 ├── UPDATE       → modify data
 └── DELETE       → remove data

Your notes make this same distinction.

2. CREATE TABLE

The most fundamental DDL operation.

Suppose we want:

employees
-------------------------
id
name
salary

We write:

CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10, 2)
);

This does not insert employees.

It creates the structure that employees can later be inserted into.

Your notes give essentially this exact example.

Mental model:

CREATE TABLE
     ↓
create the container/structure
     ↓
columns + data types + constraints

Then later:

INSERT INTO employees ...

adds actual rows.

3. CREATE DATABASE

You can also create a database:

CREATE DATABASE company;

Then:

USE company;

Now subsequent table creation occurs in that database:

CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

Think:

DATABASE
   ↓
TABLE
   ↓
COLUMNS
   ↓
ROWS
4. ALTER TABLE

This is one of the most important DDL commands.

Your notes define ALTER TABLE as modifying the structure of an existing table. They specifically show adding, dropping, modifying, and renaming columns.

Suppose:

CREATE TABLE employees (
    id INT,
    name VARCHAR(50)
);

Later we decide employees need an email.

We don't recreate the table.

We use:

ALTER TABLE employees
ADD COLUMN email VARCHAR(100);
5. Add a column
ALTER TABLE employees
ADD COLUMN email VARCHAR(100);

Before:

id | name

After:

id | name | email

This is a schema change.

6. Drop a column

Your notes give:

ALTER TABLE table_name
DROP COLUMN column_name;

Example:

ALTER TABLE employees
DROP COLUMN email;

Now email is removed from the table structure.

⚠️ This is different from:

DELETE

because DELETE removes rows, while DROP COLUMN removes a column from the schema.

7. Modify a column

Your notes specifically show:

ALTER TABLE table_name
MODIFY col_name new_datatype new_constraint;

Example:

ALTER TABLE employees
MODIFY name VARCHAR(100);

We've changed:

VARCHAR(50)

to:

VARCHAR(100)

The table remains; we're modifying its structure.

8. Rename a column

Your notes use MySQL's:

ALTER TABLE employees
CHANGE COLUMN old_name new_name new_datatype new_constraint;

Example:

ALTER TABLE employees
CHANGE COLUMN name full_name VARCHAR(100);

Now:

name

becomes:

full_name
Important MySQL detail

With CHANGE COLUMN, you specify the new data type too:

CHANGE COLUMN old_name new_name new_datatype

That's worth remembering.

9. Rename a table

Your notes show:

ALTER TABLE table_name
RENAME TO new_table_name;

Example:

ALTER TABLE employees
RENAME TO staff;

Now the table is:

staff

instead of:

employees
10. RENAME

You may also encounter:

RENAME TABLE employees TO staff;

For your notes, remember the central idea:

RENAME changes the name of a database object without changing the underlying data.

11. DROP TABLE

This is very important.

Your notes say:

DROP TABLE deletes an existing table along with its data and structure.

Example:

DROP TABLE employees;

After this:

employees

is gone.

Both:

structure ❌
data      ❌

are removed.

12. TRUNCATE TABLE

Now we reach one of the most common interview questions.

Your notes define:

TRUNCATE TABLE deletes the data inside a table, but not the table itself.

Example:

TRUNCATE TABLE employees;

Afterward:

employees table → still exists
columns         → still exist
rows            → gone

Mental picture:

DROP
 ↓
table gone

TRUNCATE
 ↓
table remains
rows gone
13. DELETE vs TRUNCATE vs DROP

🔥 MEMORIZE THIS TABLE

Command	Table structure	Rows
DELETE	remains	selected/all rows removed
TRUNCATE	remains	all rows removed
DROP	❌ removed	❌ removed

Example:

DELETE
DELETE FROM employees
WHERE id = 10;

Only matching rows are removed.

TRUNCATE
TRUNCATE TABLE employees;

All rows are removed.

But:

employees table

still exists.

DROP
DROP TABLE employees;

The entire table disappears.

14. Interview question 🔥
"What's the difference between DELETE and TRUNCATE?"

A good answer:

DELETE is a DML operation that removes rows and can use a WHERE condition. TRUNCATE removes all rows from a table while retaining the table structure and is classified as DDL in the notes.

That's much better than simply saying:

"TRUNCATE is faster."

Don't make speed the main definition.

15. Another interview question
"What's the difference between TRUNCATE and DROP?"

Answer:

TRUNCATE
→ removes all table data
→ table remains

DROP
→ removes table itself
→ structure + data disappear
16. DDL also includes indexes

Your notes include:

CREATE INDEX

and:

DROP INDEX

They explain that indexes can improve query performance by enabling faster data retrieval.

For example:

CREATE INDEX idx_employee_name
ON employees(name);

Conceptually:

Table
  ↓
Index on name
  ↓
faster lookup of names

We'll have a separate proper lesson on indexes later because they're important for interviews and performance.

For now, know:

An index is a database structure that can make certain lookups faster.

17. Constraints can also be added through DDL

Your notes show:

ALTER TABLE orders
ADD CONSTRAINT fk_customer
FOREIGN KEY (customer_id)
REFERENCES customers(id);

This connects directly to our earlier constraints lesson.

We already know:

PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK

So DDL isn't only about tables.

It can modify their associated structure and constraints.

18. Removing a constraint

Your notes show:

ALTER TABLE orders
DROP CONSTRAINT fk_customer;

Conceptually:

ADD CONSTRAINT
     ↓
schema becomes more restrictive

DROP CONSTRAINT
     ↓
remove that rule
🧠 The DDL mental model

When the interviewer says:

"DDL?"

Immediately think:

DDL
│
├── CREATE
│   ├── DATABASE
│   ├── TABLE
│   └── INDEX
│
├── ALTER
│   ├── ADD COLUMN
│   ├── DROP COLUMN
│   ├── MODIFY COLUMN
│   ├── CHANGE COLUMN
│   └── constraints
│
├── RENAME
│
├── TRUNCATE
│
└── DROP
    ├── TABLE
    └── INDEX / other objects
🎯 Mini interview drill

Before we leave DDL, make sure these are automatic:

1. Create a table
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);
2. Add a column
ALTER TABLE employees
ADD COLUMN salary DECIMAL(10,2);
3. Modify a column
ALTER TABLE employees
MODIFY name VARCHAR(100);
4. Rename a column
ALTER TABLE employees
CHANGE COLUMN name full_name VARCHAR(100);
5. Remove a column
ALTER TABLE employees
DROP COLUMN salary;
6. Rename a table
ALTER TABLE employees
RENAME TO staff;
7. Empty the table
TRUNCATE TABLE staff;
8. Destroy the table
DROP TABLE staff;
✅ DDL status

We've now covered the DDL material represented in your notes:

CREATE              ✅
ALTER               ✅
ADD COLUMN          ✅
DROP COLUMN         ✅
MODIFY COLUMN       ✅
CHANGE COLUMN       ✅
RENAME              ✅
TRUNCATE            ✅
DROP                ✅
CREATE INDEX        ✅ conceptually
DROP INDEX          ✅ conceptually
DDL constraints     ✅

The next missing notes chapter is:

👉 DML — INSERT, UPDATE, DELETE

This is important because we've spent a lot of time reading data with SELECT, but now we'll learn how MySQL actually changes rows.

We'll also cover the dangerous interview/practical mistakes:

UPDATE without WHERE
DELETE without WHERE

and understand exactly what they do.


---
part 26

Absolutely. We're now on the DML section from your notes. Your notes define DML as the commands used to manipulate records: INSERT, UPDATE, and DELETE.

Lesson: DML — INSERT, UPDATE, DELETE

First remember the distinction:

DDL → changes structure
DML → changes data
DQL → reads data

For example:

CREATE TABLE     → DDL
INSERT row       → DML
UPDATE row       → DML
DELETE row       → DML
SELECT row       → DQL
1. INSERT

INSERT adds new records to an existing table.

Your notes give this syntax:

INSERT INTO table_name
(column1, column2, ...)
VALUES
(value1, value2, ...);

Suppose:

CREATE TABLE employees (
    id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    salary DECIMAL(10,2)
);

Insert one employee:

INSERT INTO employees
(id, first_name, last_name, salary)
VALUES
(1, 'John', 'Doe', 50000);

Now the table has:

id | first_name | last_name | salary
1  | John       | Doe       | 50000
2. Why specify the columns?

You might see:

INSERT INTO employees
VALUES (1, 'John', 'Doe', 50000);

This can work when the values exactly correspond to the table's column order.

But this is generally clearer:

INSERT INTO employees
(id, first_name, last_name, salary)
VALUES
(1, 'John', 'Doe', 50000);

Because you're explicitly saying which value belongs to which column.

Interview mental model
INSERT INTO
    ↓
which table?
    ↓
(columns)
    ↓
VALUES
    ↓
what data?
3. Insert multiple rows

You can insert multiple records in one statement:

INSERT INTO employees
(id, first_name, last_name, salary)
VALUES
(1, 'John', 'Doe', 50000),
(2, 'Alice', 'Smith', 60000),
(3, 'Bob', 'Brown', 55000);

Result:

1 | John  | Doe   | 50000
2 | Alice | Smith | 60000
3 | Bob   | Brown | 55000

This is a useful practical pattern.

4. What if a column has a default?

Suppose:

CREATE TABLE employees (
    id INT,
    name VARCHAR(50),
    status VARCHAR(20) DEFAULT 'Active'
);

Then:

INSERT INTO employees
(id, name)
VALUES
(1, 'John');

The omitted status can receive its default:

1 | John | Active

This connects directly to the DEFAULT constraint we already studied.

5. UPDATE

Now we're modifying existing rows.

Your notes give:

UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE condition;

Example:

UPDATE employees
SET salary = 55000
WHERE first_name = 'John';

John's salary changes from:

50000

to:

55000
6. Updating multiple columns

You can change several columns:

UPDATE employees
SET salary = 60000,
    last_name = 'Smith'
WHERE id = 1;

So:

salary
+
last_name

are both changed for the matching row(s).

🚨 7. The most dangerous DML mistake

Look at this:

UPDATE employees
SET salary = 60000;

Where is the WHERE?

There isn't one.

That means:

Update every row in the table.

So if you had:

John   50000
Alice  70000
Bob    45000

you now get:

John   60000
Alice  60000
Bob    60000

This is one of the first things you should learn to notice in an interview or real database environment.

Always ask:

Which rows am I modifying?

Usually:

WHERE ...

answers that question.

8. UPDATE can use expressions

You don't have to assign a fixed value.

For example:

UPDATE employees
SET salary = salary * 1.10
WHERE department = 'Sales';

This means:

Increase the salary of every Sales employee by 10%.

This is exactly the kind of operation that later becomes useful when learning transactions.

9. DELETE

DELETE removes records.

Your notes give:

DELETE FROM table_name
WHERE condition;

Example:

DELETE FROM employees
WHERE id = 3;

Employee 3 is removed.

10. DELETE without WHERE

Just like UPDATE, this is dangerous:

DELETE FROM employees;

It means:

Delete all rows from employees.

But the table itself remains.

That's an important distinction:

DELETE FROM employees;

Rows       → gone
Table      → remains
Columns    → remain
Structure  → remains
11. DELETE vs TRUNCATE vs DROP

Now everything starts fitting together.

Command	What happens?
DELETE FROM employees WHERE ...	selected rows removed
DELETE FROM employees	all rows removed
TRUNCATE TABLE employees	all rows removed
DROP TABLE employees	table + structure removed

Think:

DELETE
   ↓
rows

TRUNCATE
   ↓
all rows

DROP
   ↓
entire table
12. DML + WHERE

The WHERE clause becomes especially important with DML.

UPDATE:
UPDATE employees
SET salary = 70000
WHERE id = 5;
DELETE:
DELETE FROM employees
WHERE id = 5;

The structure is:

COMMAND
   ↓
TABLE
   ↓
WHAT CHANGE?
   ↓
WHICH ROWS?
   ↓
WHERE
13. NULL and UPDATE

Suppose:

id | name | email
1  | John | john@gmail.com
2  | Alice| NULL

You can set a value to NULL:

UPDATE employees
SET email = NULL
WHERE id = 1;

Now:

John | NULL

And remember our earlier rule:

❌ Don't write:

WHERE email = NULL

Use:

WHERE email IS NULL

That connection between DML and NULL is important.

14. DML and primary keys

Suppose:

CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

Then:

INSERT INTO employees
VALUES (1, 'John');

works.

But:

INSERT INTO employees
VALUES (1, 'Alice');

will violate the primary-key uniqueness requirement.

So our earlier constraints knowledge applies directly to DML.

15. DML and foreign keys

Suppose:

customers
---------
id
1

orders
------
customer_id
1

If orders.customer_id references customers.id, deleting customer 1 may be restricted depending on the foreign-key rule.

Or if the relationship was created with:

ON DELETE CASCADE

the related child rows can be deleted automatically.

That's why:

DML
+
Constraints
+
Foreign Keys

are connected concepts.

🧠 The three commands

You should now be able to instantly translate:

"Add a new employee"
INSERT
"Change John's salary"
UPDATE
"Remove employee 10"
DELETE
🎯 Interview drill
Q1. What is DML?

Data Manipulation Language. It is used to manipulate data/records in database tables, including INSERT, UPDATE, and DELETE.

Q2. What does INSERT do?

Adds new records to a table.

Q3. What does UPDATE do?

Modifies existing records.

Q4. What does DELETE do?

Removes records from a table.

Q5. What happens if UPDATE has no WHERE?

All rows are updated.

Q6. What happens if DELETE has no WHERE?

All rows are deleted, while the table structure remains.

🧩 One complete example

Let's put everything together.

Create:

CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10,2)
);

Insert:

INSERT INTO employees
(id, name, salary)
VALUES
(1, 'John', 50000),
(2, 'Alice', 60000),
(3, 'Bob', 55000);

Update:

UPDATE employees
SET salary = salary * 1.10
WHERE id = 1;

Delete:

DELETE FROM employees
WHERE id = 3;

Final data:

id | name  | salary
1  | John  | 55000
2  | Alice | 60000

Notice the progression:

CREATE → structure
INSERT → data enters
UPDATE → data changes
DELETE → data leaves
✅ DML COMPLETE

From your notes:

DML
├── INSERT    ✅
├── UPDATE    ✅
└── DELETE    ✅

Your notes' next section is DCL — Data Control Language, covering GRANT and REVOKE.

That's a shorter chapter, so next we'll do DCL → then TCL/transactions, and after those we'll return to the remaining notes topics like set operations, subqueries, views, and indexes.

---
part 27


Absolutely. We stay on the notes-completion track.

🔐 Lesson: DCL — Data Control Language

Your notes define DCL as the part of SQL concerned with access rights, permissions, and database security. The two commands covered are:

GRANT
REVOKE

This is a relatively small chapter, so we'll learn it cleanly and move on.

1. What problem does DCL solve?

Imagine a company database:

company
│
├── employees
├── salaries
├── customers
└── orders

You don't necessarily want every database user to be able to do everything.

For example:

Analyst
→ can SELECT data

HR
→ can SELECT + UPDATE employees

Admin
→ can do almost everything

DCL controls these permissions.

Think:

DCL
 ↓
WHO
 ↓
CAN DO WHAT
 ↓
ON WHICH OBJECT?
2. GRANT

GRANT gives a user or role a privilege.

Your notes give the general syntax:

GRANT privilege_type
ON object_name
TO user_or_role;

For example:

GRANT SELECT
ON Employees
TO Analyst;

Meaning:

Give Analyst permission to SELECT from Employees.

3. What is a privilege?

A privilege is essentially an allowed operation.

Your notes give examples including:

SELECT
INSERT
UPDATE
DELETE

So conceptually:

Analyst
   │
   └── SELECT
          │
          ↓
      Employees

The analyst can read the table.

4. Grant multiple privileges

You can grant more than one privilege.

For example:

GRANT SELECT, INSERT
ON Employees
TO Analyst;

Now the user can:

SELECT  → read
INSERT  → add records

but doesn't automatically have every possible privilege.

5. REVOKE

Now the opposite.

REVOKE removes a privilege that was previously granted.

Your notes give:

REVOKE privilege_type
ON object_name
FROM user_or_role;

Example:

REVOKE SELECT
ON Employees
FROM Analyst;

Meaning:

Remove the SELECT privilege on Employees from Analyst.

6. GRANT vs REVOKE

This should become automatic:

GRANT
  ↓
give permission

REVOKE
  ↓
remove permission

Interview question:

What is the difference between GRANT and REVOKE?

Answer:

GRANT assigns privileges to a user or role, while REVOKE removes previously assigned privileges.

7. DCL vs DML

This is another useful distinction.

DML

Changes data:

INSERT
UPDATE
DELETE
DCL

Controls who can manipulate/access data:

GRANT
REVOKE

Think:

DML:
"What happens to the data?"

DCL:
"Who is allowed to do it?"
8. Example: company scenario

Suppose:

Database: company

Table: employees

User: Analyst

We want the analyst to read employee information:

GRANT SELECT
ON employees
TO Analyst;

Later, the analyst should no longer have access:

REVOKE SELECT
ON employees
FROM Analyst;

That's the entire basic DCL workflow.

9. Why DCL matters

Your notes emphasize database security.

The goal is to prevent unauthorized users from:

❌ reading sensitive data
❌ modifying data
❌ deleting data
❌ performing administrative operations

and ensure users get only the privileges they need.

This leads to a broader security principle:

Give users only the permissions they actually need.

You don't need to memorize security architecture for SQL 50, but you should understand this principle for interviews.

🧠 DCL Cheat Sheet
DCL
│
├── GRANT
│     ↓
│   give permission
│
└── REVOKE
      ↓
    remove permission
Syntax
GRANT SELECT
ON Employees
TO Analyst;
REVOKE SELECT
ON Employees
FROM Analyst;
🎯 Interview drill

Q: What is DCL?

Data Control Language. It manages database access rights and permissions.

Q: What are the two main DCL commands in your notes?

GRANT and REVOKE.

Q: What does GRANT do?

Gives a user or role a specified privilege.

Q: What does REVOKE do?

Removes a previously granted privilege.

Q: Does GRANT modify table rows?

No. It controls permissions.

✅ DCL COMPLETE

Our notes tracker now looks like:

DATABASE BASICS              ✅
DATA TYPES                   ✅
DDL                          ✅
DQL                          ✅
DML                          ✅
DCL                          ✅

And the next lesson is very important:

💳 TCL — Transactions

Your notes cover exactly three major commands:

START TRANSACTION / BEGIN
        ↓
     changes
        ↓
COMMIT  OR  ROLLBACK
        ↓
SAVEPOINT for partial rollback

They specifically explain COMMIT, ROLLBACK, and SAVEPOINT, including a bank-account-style example where a transaction can partially roll back to a savepoint.

We'll do that next, including the interview-critical question:

"What exactly happens when I COMMIT vs ROLLBACK?"
---
part 28
💳 Lesson: TCL — Transactions

Now we're covering the TCL section directly from your notes.

Your notes define a transaction as a sequence of one or more SQL statements treated as a single unit of work, so related operations can either be committed or rolled back together. They list COMMIT, ROLLBACK, and SAVEPOINT as the main TCL commands.

1. What is a transaction?

Imagine transferring ₹100 from Account A to Account B.

There are two operations:

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

and:

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

What if the first succeeds but the second fails?

We don't want:

Account A → -₹100
Account B → unchanged

That would leave our database in an inconsistent state.

Instead, we want:

Both succeed → COMMIT
                    ↓
               permanent

Something fails → ROLLBACK
                    ↓
               undo changes

That's the fundamental purpose of a transaction.

2. The mental model

Think of a transaction as a temporary workspace:

BEGIN
  ↓
change data
  ↓
change data
  ↓
something goes wrong?
  │
  ├── YES → ROLLBACK
  │
  └── NO  → COMMIT

Your notes emphasize that transactions help maintain data consistency, integrity, and reliability.

3. Starting a transaction

You can start with:

START TRANSACTION;

or:

BEGIN;

Your notes use BEGIN in their examples.

Example:

START TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

COMMIT;

Now we've grouped the related changes into one transaction.

4. COMMIT

This is the first command you absolutely need to understand.

COMMIT;

means:

Make the transaction's changes permanent.

Your notes describe COMMIT as permanently saving changes made during a transaction.

So:

START TRANSACTION
       ↓
UPDATE
       ↓
UPDATE
       ↓
COMMIT
       ↓
Changes become permanent
5. ROLLBACK

Now suppose something goes wrong.

ROLLBACK;

means:

Undo the changes made during the transaction.

Your notes explicitly describe ROLLBACK as reverting changes made during the transaction.

Example:

BEGIN;

UPDATE inventory
SET quantity = quantity - 10
WHERE product_id = 101;

-- Something goes wrong

ROLLBACK;

The change is undone.

Conceptually:

Before:
quantity = 50

UPDATE:
quantity = 40

ROLLBACK:
quantity = 50
6. COMMIT vs ROLLBACK

This should become automatic:

Command	Meaning
COMMIT	Keep changes permanently
ROLLBACK	Undo transaction changes

Think:

COMMIT   → YES, keep it
ROLLBACK → NO, undo it
7. SAVEPOINT

Now we get to the interesting part.

Suppose a transaction has three operations:

Operation A
Operation B
Operation C

Operation C fails.

Do we necessarily want to undo A and B?

Maybe not.

We can create a savepoint.

Your notes define SAVEPOINT as a named point within a transaction to which you can later roll back.

Syntax:

SAVEPOINT savepoint_name;
8. Example

Imagine:

BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 123;

SAVEPOINT before_withdrawal;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 456;

-- Something goes wrong

We can do:

ROLLBACK TO before_withdrawal;

Now what happens?

The changes after the savepoint are undone, while the earlier transaction work remains.

Your notes use this exact pattern.

Then:

COMMIT;

can commit the remaining work.

9. Visualize SAVEPOINT

This is the easiest way to remember it:

BEGIN
  │
  ├── Operation A
  │
  ├── SAVEPOINT X
  │
  ├── Operation B
  │
  ├── Operation C ❌
  │
  ↓
ROLLBACK TO X
  │
  └── B and C undone
      A remains

Then:

COMMIT;

can make the remaining changes permanent.

10. Very important distinction
ROLLBACK
ROLLBACK;

Undo the transaction's changes.

ROLLBACK TO SAVEPOINT
ROLLBACK TO before_withdrawal;

Undo changes back to a particular savepoint, rather than abandoning the entire transaction.

Your notes specifically demonstrate this distinction.

11. Complete banking example

Let's make the whole thing intuitive.

Starting balances:

Account 123 → ₹1000
Account 456 → ₹500

We want to transfer ₹100.

BEGIN;

UPDATE Accounts
SET Balance = Balance - 100
WHERE AccountID = 123;

SAVEPOINT before_deposit;

UPDATE Accounts
SET Balance = Balance + 100
WHERE AccountID = 456;

Suppose the second operation causes an error.

We can:

ROLLBACK TO before_deposit;

Now:

Account 123 → ₹900
Account 456 → ₹500

The first operation remains.

If the application decides this is acceptable:

COMMIT;

Otherwise:

ROLLBACK;

would undo the transaction's changes.

12. Why transactions matter in interviews

A classic interview question:

Why do we need transactions?

Good answer:

Transactions group related SQL operations into a single unit of work so that changes can be committed or rolled back, helping maintain consistency and integrity when operations succeed or fail.

That's essentially the concept your notes teach.

13. TCL + DML

Notice something important.

Transactions are usually useful around data-changing operations:

TCL
 ↓
controls
 ↓
DML
 ↓
INSERT / UPDATE / DELETE

Example:

START TRANSACTION;

UPDATE employees
SET salary = salary * 1.10
WHERE department = 'Sales';

DELETE FROM employees
WHERE status = 'Inactive';

COMMIT;

So don't think of TCL as completely separate from DML.

They work together.

Your notes explicitly say TCL commands are used in combination with DML and other SQL commands to help maintain reliable database state.

🧠 TCL Cheat Sheet
                 TCL
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
    COMMIT     ROLLBACK   SAVEPOINT
       │          │          │
       ↓          ↓          ↓
   keep it     undo it    mark a point
                           ↓
                    ROLLBACK TO
Start:
START TRANSACTION;

or:

BEGIN;
Save:
COMMIT;
Undo:
ROLLBACK;
Partial undo:
SAVEPOINT sp1;

ROLLBACK TO sp1;
🎯 Interview Drill
Q1. What is a transaction?

A group of related SQL operations treated as one unit of work.

Q2. What does COMMIT do?

Makes the transaction's changes permanent.

Q3. What does ROLLBACK do?

Undoes changes made during the transaction.

Q4. What is a SAVEPOINT?

A named point inside a transaction to which you can later roll back.

Q5. Difference between ROLLBACK and ROLLBACK TO SAVEPOINT?
ROLLBACK
→ undo the transaction's changes

ROLLBACK TO SAVEPOINT
→ undo changes back to a particular savepoint
Q6. Why are transactions important?

For maintaining consistency and integrity when multiple related operations must succeed or fail together.

✅ TCL COMPLETE

Our notes tracker is now:

Database Basics       ✅
Data Types            ✅
DDL                   ✅
DQL                   ✅
DML                   ✅
DCL                   ✅
TCL                   ✅

And now we're getting into the remaining SQL/query material from the notes.

The next chapter I want to cover is:

🔀 Set Operations

Specifically:

UNION
UNION ALL
INTERSECT
EXCEPT

with an important MySQL-specific point because your notes show set-operation concepts, while MySQL's support differs by version. After that we'll systematically cover subqueries → views → indexes, and then do a final "have we covered every note?" audit.


---
part 29
🔀 Lesson: SQL Set Operations

Good. This is another chapter explicitly present in your notes, so we'll learn exactly what you need, without going unnecessarily deep.

Your notes describe set operations as ways to combine/manipulate the result sets of multiple SELECT queries, based on set-theory ideas. They list four operations: UNION, INTERSECT, EXCEPT, and UNION ALL.

1. First: What problem do Set Operations solve?

Suppose we have two queries:

SELECT name FROM Customers;

and:

SELECT name FROM Suppliers;

Each query produces its own result set.

Set operations let us ask:

                         Two result sets
                              │
              ┌───────────────┼───────────────┐
              ↓               ↓               ↓
            UNION         INTERSECT        EXCEPT
              ↓               ↓               ↓
          combine          common          first only

And:

UNION ALL
    ↓
combine everything, including duplicates
2. UNION

UNION combines the results of two or more SELECT queries.

Your notes emphasize:

UNION removes duplicates by default.

Example:

SELECT CustomerName FROM Customers

UNION

SELECT SupplierName FROM Suppliers;

Suppose:

Customers
Alice
Bob
Suppliers
SupplierA
SupplierB

Result:

Alice
Bob
SupplierA
SupplierB

This is the exact type of example used in your notes.

3. Why is it called a "set" operation?

Think mathematically.

Suppose:

A = {Alice, Bob, Carol}

B = {Bob, Carol, David}

Then:

A UNION B

gives:

{Alice, Bob, Carol, David}

Duplicates don't appear.

So:

UNION
 ↓
A OR B
4. UNION ALL

Now we have:

SELECT name FROM Customers

UNION ALL

SELECT name FROM Suppliers;

The important difference:

UNION ALL does not remove duplicates.

Your notes explicitly state that it simply concatenates all rows from the result sets.

Suppose:

Query 1
Alice
Bob
Query 2
Bob
Carol
UNION
Alice
Bob
Carol
UNION ALL
Alice
Bob
Bob
Carol
5. Memorize this difference
UNION
   ↓
combine
   ↓
remove duplicates

UNION ALL
   ↓
combine
   ↓
keep duplicates
Interview question:

Why might you choose UNION ALL instead of UNION?

Because if duplicates are supposed to remain, UNION ALL preserves them. It also avoids the duplicate-elimination step.

For SQL interview problems, this distinction is important.

6. INTERSECT

Now imagine:

A = {Alice, Bob, Carol}

B = {Bob, Carol, David}

What elements exist in both?

Bob
Carol

That's:

SELECT name FROM Customers

INTERSECT

SELECT name FROM Suppliers;

Your notes define INTERSECT as returning common rows appearing in all result sets.

Mental model:

INTERSECT
     ↓
   common
     ↓
 A ∩ B
7. EXCEPT

Now ask:

What exists in A but not in B?

Given:

A = {Alice, Bob, Carol}

B = {Bob, Carol, David}

Then:

A EXCEPT B

returns:

Alice

Your notes define EXCEPT as returning distinct rows present in the first result set but absent from the second.

This direction is extremely important.

A EXCEPT B

is not the same as:

B EXCEPT A
8. Visualizing all four

Let's use:

A = {1, 2, 3}
B = {2, 3, 4}

Then:

UNION
A UNION B
→ {1, 2, 3, 4}
UNION ALL

If each appears once:

A UNION ALL B
→ {1, 2, 3, 2, 3, 4}
INTERSECT
A INTERSECT B
→ {2, 3}
EXCEPT
A EXCEPT B
→ {1}

This is the easiest way to remember them.

9. The biggest requirement: compatible result sets

Suppose:

SELECT name
FROM Customers

UNION

SELECT name
FROM Suppliers;

Both queries return:

1 column

Good.

But imagine:

SELECT name, age
FROM Customers

UNION

SELECT name
FROM Suppliers;

That's not compatible because the two result sets don't have matching column counts.

Your notes emphasize that set operations require the queries to have the same number of output columns and compatible data types.

So remember:

Query A
columns: 3
       +
Query B
columns: 3
       ↓
compatible structure
10. Set Operations vs JOINs

This is an important interview distinction, and your notes explicitly compare them.

Set operation

Combines rows from result sets.

Query A
   +
Query B
   ↓
UNION
JOIN

Combines columns/data from related tables based on a condition.

Table A
   +
Table B
   ↓
JOIN
   ↓
more columns
11. Example

Suppose:

Customers
id | name
1  | Alice
2  | Bob
Orders
id | customer_id | amount
10 | 1           | 500
11 | 2           | 700

A JOIN can produce:

Alice | 500
Bob   | 700

because we're combining related information horizontally.

A UNION instead might do:

SELECT name FROM Customers

UNION

SELECT supplier_name FROM Suppliers;

and combine the result vertically:

Alice
Bob
SupplierA
SupplierB
🧠 Horizontal vs Vertical

This is a great mental shortcut:

JOIN
→ horizontal combination
→ combines columns from related rows

UNION
→ vertical combination
→ combines rows from result sets

Not a formal definition, but an excellent interview intuition.

12. UNION and ORDER BY

One thing to be aware of:

If you want to order the final combined result, the ORDER BY generally belongs at the end of the combined query:

SELECT name FROM Customers

UNION

SELECT name FROM Suppliers

ORDER BY name;

Think:

Query 1
   ↓
UNION
   ↓
Query 2
   ↓
combined result
   ↓
ORDER BY
13. UNION and duplicates

This is worth drilling because interviewers love it.

Suppose:

A:
Alice
Bob

B:
Bob
Charlie
UNION
Alice
Bob
Charlie
UNION ALL
Alice
Bob
Bob
Charlie

So if the question says:

"Return all records including duplicates"

you should immediately think:

UNION ALL

If it says:

"Return unique records"

think:

UNION
14. A practical example

Suppose we have:

current_students
----------------
Alice
Bob

former_students
---------------
Bob
Charlie

Question:

Give me all students who have ever been enrolled.

SELECT name
FROM current_students

UNION

SELECT name
FROM former_students;

Result:

Alice
Bob
Charlie

Bob appears only once.

15. Question: Who appears in both?
SELECT name
FROM current_students

INTERSECT

SELECT name
FROM former_students;

Result:

Bob
16. Question: Who is currently enrolled but wasn't a former student?
SELECT name
FROM current_students

EXCEPT

SELECT name
FROM former_students;

Result:

Alice

Again, notice the direction:

current
   EXCEPT
former

means:

Current but not former.

⚠️ MySQL-specific note

Here I want to distinguish your notes from actual MySQL behavior.

Your notes teach the four general SQL set operations:

UNION
UNION ALL
INTERSECT
EXCEPT

For our MySQL interview track, don't blindly assume every operation behaves identically across all MySQL versions/dialects. Set-operation support is version-sensitive, so when we actually solve a MySQL problem, we'll use syntax supported by the target MySQL version rather than mechanically copying generic SQL notes.

The conceptual knowledge, however, is absolutely worth knowing:

UNION      → A + B, distinct
UNION ALL  → A + B, duplicates preserved
INTERSECT  → A ∩ B
EXCEPT     → A - B
🎯 Interview Drill
Q1. Difference between UNION and UNION ALL?

UNION removes duplicate rows; UNION ALL preserves duplicates.

Q2. What does INTERSECT return?

Rows common to both result sets.

Q3. What does EXCEPT return?

Distinct rows in the first query's result that aren't in the second query's result.

Q4. Can you UNION queries with different numbers of columns?

No. The result sets need compatible column structures, including the same number of output columns.

Q5. UNION vs JOIN?

Set operations combine result sets; joins combine data from tables based on join conditions.

🧠 One-minute memory trick
UNION
A + B
unique

UNION ALL
A + B
everything

INTERSECT
A ∩ B
common

EXCEPT
A - B
first only

If you remember those four lines, you've essentially mastered the conceptual part of this chapter.

✅ Notes Tracker

We're getting very close:

Database Basics       ✅
Data Types            ✅
DDL                   ✅
DQL                   ✅
DML                   ✅
DCL                   ✅
TCL                   ✅
Set Operations        ✅

Remaining major notes chapters:

⬜ Subqueries — systematic pass
⬜ Views
⬜ Indexes
⬜ Final notes audit
Next: 🧩 Subqueries

This is especially important for your SQL 50 goal because your notes cover subqueries in WHERE, FROM, and HAVING, and distinguish them from joins.

We'll learn scalar vs multi-row vs correlated subqueries, IN, EXISTS, and then connect them directly to the SQL 50 problems where they actually help.


---
part 30
🧩 Lesson: Subqueries

Now we're entering one of the most important SQL concepts for interviews.

Your notes define a subquery as a query inside another SQL query—also called an inner query or nested query. The inner query produces a result that the outer query uses for filtering, comparison, or calculation.

The key idea:

Outer Query
    ↓
needs some information
    ↓
Subquery
    ↓
produces that information
    ↓
Outer Query uses it
1. The simplest subquery

Suppose we have:

employees
----------------
name    salary
Alice   50000
Bob     70000
Carol   90000
David   60000

Question:

Find employees earning more than the average salary.

First, conceptually:

SELECT AVG(salary)
FROM employees;

Maybe result:

67500

Then:

SELECT name
FROM employees
WHERE salary > 67500;

Result:

Bob
Carol

A subquery combines those two steps:

SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

This is exactly the style shown in your notes: first calculate the class average, then find students whose marks exceed it.

2. Read the query from inside out

This is a very useful interview technique.

Look at:

SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

Don't try to understand everything simultaneously.

First:

SELECT AVG(salary)
FROM employees

produces one value.

Then the outer query effectively becomes:

SELECT name
FROM employees
WHERE salary > 67500;

So:

SUBQUERY
   ↓
calculate something
   ↓
OUTER QUERY
   ↓
use that result
3. Why use a subquery?

Your notes give three major purposes:

Filtering
Comparison
Calculation

For example:

Filtering
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
Comparison
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
)
Calculation
SELECT salary - (
    SELECT AVG(salary)
    FROM employees
)
FROM employees;
4. Scalar subquery

This is the first type you should know.

A scalar subquery returns one value.

Example:

SELECT AVG(salary)
FROM employees;

returns:

67500

Then:

WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)

works nicely because > expects a single comparable value.

Think:

Subquery
   ↓
one value
   ↓
50000

Examples of functions commonly producing scalar results:

AVG()
MAX()
MIN()
SUM()
COUNT()
5. Subquery returning multiple values

Now suppose:

employees
----------------
name      dept
Alice     IT
Bob       HR
Carol     Sales
David     IT

Question:

Find employees who work in departments located in New York.

Maybe another table:

departments
----------------
dept   city
IT     New York
HR     London
Sales  New York

The subquery:

SELECT dept
FROM departments
WHERE city = 'New York';

returns:

IT
Sales

That's multiple values.

So this is appropriate:

SELECT name
FROM employees
WHERE dept IN (
    SELECT dept
    FROM departments
    WHERE city = 'New York'
);

Notice:

=       → usually one value
IN      → can handle multiple values

This distinction is extremely important.

6. IN with a subquery

Your notes explicitly mention comparison operators including IN and NOT IN.

Example:

SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'New York'
);

Read it in English:

Find employees whose department ID is among the department IDs located in New York.

This is a very natural subquery pattern.

IN
 ↓
one of these values
 ↓
(subquery result)
7. NOT IN

The opposite:

SELECT name
FROM employees
WHERE department_id NOT IN (
    SELECT department_id
    FROM departments
    WHERE location = 'New York'
);

Meaning:

Employees whose department isn't among those located in New York.

⚠️ One interview-level warning: NOT IN combined with NULL can produce surprising results because of SQL's three-valued logic.

We've already learned NULL, so this is where that knowledge becomes useful.

When NULL-sensitive exclusion is involved, NOT EXISTS is often safer.

We'll come back to that.

8. Subquery in WHERE

This is the most common beginner form.

Your notes give the general pattern:

SELECT columns
FROM table
WHERE column OPERATOR (
    SELECT column
    FROM table
    WHERE condition
);

Example:

SELECT ProductName, Price
FROM Products
WHERE Price > (
    SELECT AVG(Price)
    FROM Products
);

Read:

Find products whose price is greater than the average product price.

9. Subquery in FROM

This is another important pattern in your notes.

Here, the subquery creates a temporary result set that the outer query can treat like a table.

Example:

SELECT MAX(marks)
FROM (
    SELECT marks
    FROM students
    WHERE city = 'Delhi'
) AS delhi_students;

Conceptually:

Subquery
   ↓
students from Delhi
   ↓
temporary result
   ↓
MAX()

Your notes describe this as a two-step process: first retrieve the relevant students, then calculate the maximum marks from that result.

Important:

A subquery in FROM generally needs an alias:

) AS delhi_students

Think:

FROM
(
    SELECT ...
) AS temporary_table
10. Why AS matters here

We've already learned aliases.

Now they become useful with derived tables:

FROM (
    SELECT ...
) AS t

Then you can reference:

SELECT t.name
FROM (
    SELECT name
    FROM employees
) AS t;

So aliases aren't just cosmetic.

They're required/useful when giving a name to a derived table.

11. Subquery in HAVING

Your notes also mention subqueries being usable in HAVING.

For example, conceptually:

SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > (
    SELECT AVG(salary)
    FROM employees
);

Meaning:

Show departments whose average salary is greater than the overall company average salary.

Notice the two levels:

GROUP BY
   ↓
calculate department average
   ↓
HAVING
   ↓
compare against
   ↓
overall average

This is an excellent interview pattern.

12. Subquery vs JOIN

Your notes have a dedicated comparison.

Subquery
Query A
   ↓
produces result
   ↓
Query B uses it
JOIN
Table A
   +
Table B
   ↓
JOIN condition
   ↓
combined result

Your notes summarize the difference as:

	Subquery	JOIN
Main purpose	Filtering/comparison/calculation	Combine related tables
Input	Result of another query	Related tables
Common location	WHERE, FROM, HAVING	Primarily FROM
Output	Scalar/single-column/result set	Often multi-column result
Complexity	Can be simple for smaller tasks	Often useful for related-table retrieval

13. Don't memorize "subquery = slower"

Your notes mention that subqueries can be slower and joins can be more efficient for some large-data scenarios.

Don't turn that into:

"Subqueries are always bad."

That's false.

The correct interview mindset is:

Choose the formulation that clearly expresses the requirement and produces an efficient execution plan.

In SQL 50, we're primarily learning problem recognition, not premature optimization.

14. Correlated subquery

Now one important concept.

A normal subquery can execute independently:

SELECT AVG(salary)
FROM employees;

A correlated subquery depends on the current row of the outer query.

Example:

SELECT e1.name
FROM employees e1
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e1.department_id
);

Read this carefully:

Find employees whose salary is greater than the average salary of their own department.

The inner query references:

e1.department_id

from the outer query.

That's why it's correlated.

15. Visualizing correlation

Normal:

Outer query
    │
    └── Subquery
          │
          └── independent

Correlated:

Outer row
    │
    ├── employee Alice
    │       ↓
    │   subquery uses Alice's department
    │
    ├── employee Bob
    │       ↓
    │   subquery uses Bob's department
    │
    └── employee Carol
            ↓
        subquery uses Carol's department

Conceptually:

outer row → inner query
              ↑
              │
         depends on outer row
16. Why correlated subqueries matter for interviews

Because they appear when the question contains phrases like:

"for each employee"

"their department"

"their category"

"greater than the average for their department"

That word "their" is often a clue that the calculation depends on the current outer row.

17. EXISTS

Another extremely important subquery pattern:

WHERE EXISTS (
    SELECT 1
    ...
)

EXISTS asks:

Does the subquery return at least one row?

Example:

SELECT c.customer_id
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);

Meaning:

Find customers who have at least one order.

Notice that we don't care what the subquery returns.

We care whether a matching row exists.

18. EXISTS vs IN

This distinction is worth learning now.

IN
WHERE department_id IN (
    SELECT department_id
    FROM departments
)

asks:

Is this value among these values?

EXISTS
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
)

asks:

Does at least one matching row exist?

Mental shortcut:

IN
 ↓
value membership

EXISTS
 ↓
row existence
19. Why SELECT 1?

You'll often see:

WHERE EXISTS (
    SELECT 1
    FROM orders
    WHERE orders.customer_id = customers.customer_id
)

Beginners sometimes wonder:

"Why 1?"

Because EXISTS only cares whether a row exists. The actual selected value isn't important.

This:

SELECT 1

communicates the intent clearly:

I only care whether a matching row exists.

20. Three patterns you MUST recognize

When you see an interview question, identify which of these structures you're dealing with.

Pattern 1 — Single calculated value
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)

Think:

scalar subquery
Pattern 2 — List of values
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'NY'
)

Think:

multi-row subquery + IN
Pattern 3 — Does a related row exist?
WHERE EXISTS (
    SELECT 1
    FROM orders
    WHERE orders.customer_id = customers.customer_id
)

Think:

EXISTS
🎯 SQL 50 Connection

This chapter connects strongly with the later SQL 50 problems involving:

Employees Whose Manager Left the Company #1978
Investments in 2016 #585
Department Top Three Salaries #185
Customers Who Bought All Products #1045
and several problems where aggregation + filtering can be expressed using subqueries.

But here's an important point for our learning:

Don't force a subquery just because we've learned subqueries.

Sometimes a JOIN, GROUP BY, or window function is a cleaner solution.

Our goal is to recognize the shape of the problem.

🧠 Subquery Cheat Sheet
SUBQUERY
│
├── WHERE
│    ├── scalar
│    │    └── =, >, <, etc.
│    │
│    ├── multi-row
│    │    └── IN / NOT IN
│    │
│    └── EXISTS
│         └── does a row exist?
│
├── FROM
│    └── derived table
│
├── HAVING
│    └── compare aggregate results
│
└── Correlated
     └── inner query references outer row
🔥 Interview Translation Skill

This is the part I really want you to develop.

Question:

Find employees who earn more than the average salary.

Your brain should go:

"average salary"
      ↓
aggregate
      ↓
one value
      ↓
scalar subquery
      ↓
salary > (...)

SQL:

SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
Question:

Find customers who have placed at least one order.

Brain:

"at least one"
      ↓
existence
      ↓
EXISTS

SQL:

SELECT c.customer_id
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
Question:

Find employees in departments located in Delhi.

Brain:

department IDs
      ↓
multiple values
      ↓
IN

SQL:

SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE city = 'Delhi'
);

That English → SQL structure translation is what will eventually make the SQL 50 problems much easier.

✅ Subqueries — core material covered

From your notes:

Subquery definition                 ✅
Nested query                        ✅
WHERE subqueries                    ✅
Comparison operators                ✅
Scalar result                       ✅
Multiple-row result                ✅
IN / NOT IN                         ✅
FROM subquery                       ✅
HAVING subquery                     ✅
Subquery vs JOIN                    ✅
Correlated subquery                ✅
EXISTS                              ✅

The next notes chapter is Views.

That's much shorter:

CREATE VIEW
SELECT FROM view
UPDATE/DELETE considerations

---
part 31

👁️ Lesson: MySQL Views

We're continuing strictly through your notes, and this one is short but useful.

Your notes define a view as a virtual table based on the result set of an SQL statement. They also note that a view shows up-to-date data because the database engine recreates the view's result when it is queried.

1. What is a View?

Imagine we have a complicated query:

SELECT
    e.name,
    e.salary,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
WHERE e.salary > 50000;

Suppose we use this query again and again.

Instead of rewriting it every time, we can create a view.

Think:

Complex SELECT query
        ↓
     CREATE VIEW
        ↓
   named virtual table
        ↓
     SELECT from it

The important word is:

Virtual

A view is not simply another physical copy of the table data.

2. Creating a View

The basic pattern is:

CREATE VIEW view_name AS
SELECT ...
FROM ...
WHERE ...;

For example:

CREATE VIEW high_salary_employees AS
SELECT
    name,
    salary
FROM employees
WHERE salary > 50000;

Now you can query it like a table:

SELECT *
FROM high_salary_employees;

So instead of repeatedly writing:

SELECT name, salary
FROM employees
WHERE salary > 50000;

you can write:

SELECT *
FROM high_salary_employees;
3. What does the View actually contain?

This is the key conceptual point.

Suppose:

employees
----------------
Alice  40000
Bob    60000
Carol  70000

We create:

CREATE VIEW high_salary_employees AS
SELECT name, salary
FROM employees
WHERE salary > 50000;

The view gives us:

high_salary_employees
---------------------
Bob     60000
Carol   70000

Now imagine Bob's salary changes:

UPDATE employees
SET salary = 80000
WHERE name = 'Bob';

Query:

SELECT *
FROM high_salary_employees;

will reflect the updated underlying data.

That's exactly the point made by your notes: the view shows up-to-date data rather than being a separate static result.

4. View vs Table

This is a common interview question.

Table
Table
 ↓
stores data
 ↓
actual rows
View
View
 ↓
defined by a query
 ↓
virtual table
 ↓
shows result of that query

Mental model:

TABLE
→ actual stored data

VIEW
→ saved query / virtual table
5. Why use Views?

A view is useful when you want to make a complicated query easier to reuse.

For example:

CREATE VIEW employee_details AS
SELECT
    e.name,
    e.salary,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;

Now someone can simply do:

SELECT *
FROM employee_details;

Instead of remembering the entire join.

6. Views can also simplify access

Suppose the actual employee table contains:

id
name
salary
phone
address
bank_account

But another user only needs:

name
department

You could define a view containing only the required information.

Conceptually:

Actual table
    │
    ├── salary
    ├── phone
    ├── address
    ├── bank_account
    │
    └── other sensitive data
          ↓
       VIEW
          ↓
     name + department

So views can provide a simpler interface to underlying data.

7. DROP VIEW

When you no longer need a view:

DROP VIEW high_salary_employees;

This removes the view definition.

It does not mean that the underlying employee table is deleted.

Remember:

DROP TABLE employees
→ employees table gone

DROP VIEW high_salary_employees
→ view gone
→ employees table remains
8. CREATE OR REPLACE VIEW

A useful MySQL pattern is:

CREATE OR REPLACE VIEW high_salary_employees AS
SELECT
    name,
    salary
FROM employees
WHERE salary > 60000;

This lets you replace the existing view definition.

For our notes-level understanding, the important idea is:

CREATE VIEW
→ create virtual table

DROP VIEW
→ remove virtual table definition
9. View + SELECT

Once a view exists, you query it like a table:

SELECT *
FROM high_salary_employees;

You can also filter it:

SELECT name
FROM high_salary_employees
WHERE salary > 70000;

And sort it:

SELECT *
FROM high_salary_employees
ORDER BY salary DESC;

This is why views are convenient: the underlying query becomes reusable.

10. View vs Subquery

This connects directly to our previous lesson.

Subquery

Usually embedded inside another query:

SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
View

The query is given a reusable name:

CREATE VIEW high_salary_employees AS
SELECT ...

Then later:

SELECT *
FROM high_salary_employees;

Think:

SUBQUERY
→ query inside query

VIEW
→ named reusable query result

That's a very useful distinction.

11. View vs SELECT directly

Suppose you repeatedly need:

SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;

Without a view:

write query
write query
write query
write query

With a view:

CREATE VIEW employee_department AS
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;

Then:

SELECT *
FROM employee_department;

Much cleaner.

🧠 Interview Question
"What is a view?"

A strong answer:

A view is a virtual table based on the result of an SQL query. It provides a reusable way to query the underlying data, and according to the notes, it reflects up-to-date data when queried.

"Does a view store a separate copy of the data?"

For the basic MySQL view concept we're studying:

No. Think of it as a stored query definition whose result is generated from the underlying data.

"What happens to a view when the underlying data changes?"

The view reflects the current underlying data when queried, consistent with the notes' description of views showing up-to-date data.

🎯 One Complete Example

Base tables:

employees
-----------------------
id | name  | salary
1  | Alice | 40000
2  | Bob   | 60000
3  | Carol | 70000

Create:

CREATE VIEW high_salary_employees AS
SELECT
    id,
    name,
    salary
FROM employees
WHERE salary > 50000;

Query:

SELECT *
FROM high_salary_employees;

Result:

2 | Bob   | 60000
3 | Carol | 70000

Update base table:

UPDATE employees
SET salary = 80000
WHERE id = 1;

Now:

SELECT *
FROM high_salary_employees;

returns:

1 | Alice | 80000
2 | Bob   | 60000
3 | Carol | 70000

The view's result changed because the underlying data changed.

🧠 Remember This
VIEW
│
├── virtual table
│
├── based on SELECT query
│
├── CREATE VIEW
│
├── SELECT FROM view
│
└── DROP VIEW

And the most important conceptual distinction:

TABLE
→ stores actual rows

VIEW
→ presents rows through a stored query
✅ Notes Tracker

We're now at:

Database Basics       ✅
Data Types            ✅
Constraints/Keys      ✅
DDL                   ✅
DQL                   ✅
DML                   ✅
DCL                   ✅
TCL                   ✅
Joins                 ✅
Set Operations        ✅
Subqueries            ✅
Views                 ✅

One major notes topic remains:

⚡ INDEXES

Your notes introduce indexes under DDL and explain that they can improve query performance by enabling faster data retrieval.

We'll do Indexes next, including:

CREATE INDEX
DROP INDEX
single-column index
multi-column index
why indexes speed up queries
when indexes help
why too many indexes are bad

Then we'll perform the final complete audit of your uploaded notes before returning to our SQL 50 interview-solving flow.

---
part 32

⚡ Lesson: INDEXES

Perfect. This is the last major topic in the notes before we do our full coverage audit.

Your notes place indexes under DDL and describe them as structures created on one or more columns to improve query performance by enabling faster data retrieval.

1. What is an Index?

Imagine a book with 1,000 pages.

You want to find:

"Database normalization"

Without an index, you might scan page after page:

Page 1
Page 2
Page 3
...
Page 1000

With the book's index:

Normalization → page 527

You jump much closer to what you need.

A database index serves a similar purpose.

Table
  ↓
Index on column
  ↓
faster lookup
2. Without an Index

Suppose:

employees
--------------------------------
id | name | email | department
--------------------------------
1  | Alice | alice@x.com | IT
2  | Bob   | bob@x.com   | HR
3  | Carol | carol@x.com | IT
...
1,000,000 rows

And we run:

SELECT *
FROM employees
WHERE email = 'carol@x.com';

Conceptually, without a useful index the database may need to examine many rows to locate the matching one.

3. Create an Index

Your notes give this pattern:

CREATE INDEX idx_employee_name
ON employees (name);

For our example:

CREATE INDEX idx_employee_email
ON employees (email);

Now we have an index associated with:

employees.email

So a lookup such as:

SELECT *
FROM employees
WHERE email = 'carol@x.com';

can potentially use that index.

4. The basic syntax

Memorize:

CREATE INDEX index_name
ON table_name (column_name);

Example:

CREATE INDEX idx_customer_name
ON customers (name);

Break it down:

CREATE INDEX
     ↓
idx_customer_name
     ↓
ON customers
     ↓
(name)
5. Why does an index improve performance?

The important idea is:

Without useful index
       ↓
more data may need to be examined

With useful index
       ↓
database can locate relevant rows more efficiently

Your notes explicitly describe indexes as improving query performance through faster data retrieval.

Don't memorize the simplistic statement:

"Index always makes queries faster."

Instead:

An appropriate index can make certain queries substantially faster.

That's the interview-quality understanding.

6. Index on multiple columns

Your notes say indexes can be created on one or more columns.

For example:

CREATE INDEX idx_employee_dept_name
ON employees (department_id, name);

This is a composite index (multi-column index).

Conceptually:

Index
 ↓
department_id
      +
name

This becomes particularly relevant when queries frequently filter or sort using those columns together.

7. Single-column vs Composite Index
Single-column
CREATE INDEX idx_email
ON employees (email);

Index:

email
Composite
CREATE INDEX idx_dept_name
ON employees (department_id, name);

Index:

department_id + name

Remember:

single-column
→ one column

composite
→ multiple columns
8. DROP INDEX

Your notes also explicitly cover removing an index:

DROP INDEX idx_employee_name;

So:

CREATE INDEX
→ create index

DROP INDEX
→ remove index
9. Indexes are NOT free

This is an important practical idea.

If indexes only made everything faster and had no downside, we'd index every column.

But maintaining indexes has a cost.

Think:

                 INDEX
                   │
          ┌────────┴────────┐
          ↓                 ↓
      SELECT faster      maintenance cost
                            ↓
                       INSERT/UPDATE/DELETE

Why?

When underlying indexed data changes, the database has to maintain the index as well.

So indexes involve a performance/storage trade-off.

10. Example

Suppose:

CREATE INDEX idx_email
ON employees(email);

Now:

SELECT *
FROM employees
WHERE email = 'alice@example.com';

may benefit from the index.

But when we do:

INSERT INTO employees (...);

the index also needs to be updated.

Similarly:

UPDATE employees
SET email = 'new@example.com'
WHERE id = 1;

the index has to reflect the changed value.

So:

Indexes help:
     SELECT
       ↑

Indexes add work:
 INSERT
 UPDATE
 DELETE

That's why we don't blindly create indexes everywhere.

11. Indexes and WHERE

This is where your SQL-learning journey connects beautifully.

We've learned:

SELECT *
FROM employees
WHERE email = 'alice@example.com';

The WHERE clause identifies what we're searching for.

An index on email can potentially make that search much more efficient.

So think:

SQL query
   ↓
WHERE email = ?
   ↓
Is email indexed?
   ↓
Potentially faster lookup
12. Indexes and JOINs

This connects to everything we've already learned.

Suppose:

SELECT *
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;

Indexes on columns involved in joins can be useful depending on the query and execution plan.

This is one reason you'll hear interviewers ask:

"Which columns should you index?"

A reasonable starting point is:

Columns frequently used in filtering, joining, ordering, or other operations where an index can help—while considering write and storage costs.

But don't say:

"Index every column used in WHERE."

The actual usefulness depends on the query and data distribution.

13. Indexes and ORDER BY

Consider:

SELECT *
FROM employees
ORDER BY name;

An appropriate index may help certain ordering operations.

Again:

Potentially.

The database optimizer decides whether using an index is actually beneficial.

This is where real database performance becomes more sophisticated than memorizing rules.

14. The optimizer decides

This is an important interview concept.

Creating an index doesn't mean:

CREATE INDEX
      ↓
EVERY QUERY MUST USE IT

Instead:

SQL query
   ↓
optimizer
   ↓
examines possible execution strategies
   ↓
chooses a plan

So when someone asks:

"I created an index. Why isn't MySQL using it?"

The answer isn't automatically:

"MySQL is broken."

The optimizer may determine that another strategy is cheaper.

15. Composite Index — important mental model

Suppose:

CREATE INDEX idx_dept_name
ON employees(department_id, name);

The order matters.

Think of it conceptually as:

(department_id, name)
       ↑
   first column
       ↓
     name

So don't think:

INDEX(department_id, name)
=
INDEX(department_id)
+
INDEX(name)

It's a specific multi-column index with a defined column order.

For interview purposes, remember:

The order of columns in a composite index matters.

We'll go deeper into the leftmost-prefix principle later only if your interview preparation requires it. It isn't necessary for completing the notes.

16. Index vs Primary Key

This is another common interview question.

We learned earlier:

id INT PRIMARY KEY

A primary key is a constraint that identifies rows uniquely.

An index is primarily a data-access structure that can improve retrieval.

They are related, but they're not conceptually the same thing.

PRIMARY KEY
→ data integrity / row identity

INDEX
→ efficient data access

A primary key in MySQL is indexed automatically, but don't confuse the constraint with the index concept itself.

17. Index vs UNIQUE

Similarly:

email VARCHAR(255) UNIQUE

The UNIQUE constraint is about:

preventing duplicate values.

An index is about:

efficient access.

Again:

UNIQUE
→ integrity rule

INDEX
→ access/performance structure

A unique constraint is implemented with an index in MySQL, but the concepts serve different purposes.

18. Interview Question
"What is an index?"

Good answer:

An index is a database structure created on one or more columns to allow the database to retrieve matching data more efficiently. In the notes, indexes are presented as a DDL object used to improve query performance through faster data retrieval.

"How do you create an index?"
CREATE INDEX idx_name
ON table_name (column_name);

From the notes:

CREATE INDEX idx_employee_name
ON employees (name);

"How do you remove an index?"
DROP INDEX idx_employee_name;

"Why not create indexes on every column?"

Because indexes require storage and need maintenance when indexed data changes. Therefore, unnecessary indexes can hurt write performance and consume resources.

🧠 Index Cheat Sheet
INDEX
│
├── Purpose
│     └── faster data retrieval
│
├── Create
│     └── CREATE INDEX ...
│
├── Single column
│     └── INDEX(email)
│
├── Multiple columns
│     └── INDEX(department_id, name)
│
└── Remove
      └── DROP INDEX ...

Your notes' core definition is very simple:

Create an index on one or more columns to improve query performance by enabling faster data retrieval.

🎉 WE HAVE REACHED THE END OF THE NOTES

Now this is important because earlier you asked:

"Did we cover everything taught in the notes first?"

We've now gone through the major material systematically.

📚 Coverage
Topic	Status
What is SQL / DBMS basics	✅
Databases / tables / rows / columns	✅
Data types	✅
DDL	✅
CREATE DATABASE / DROP DATABASE	✅
CREATE TABLE	✅
ALTER TABLE	✅
DROP TABLE	✅
TRUNCATE	✅
Constraints	✅
NOT NULL	✅
UNIQUE	✅
PRIMARY KEY	✅
FOREIGN KEY	✅
DEFAULT	✅
CHECK	✅
Cascading actions	✅
DQL / SELECT	✅
WHERE	✅
Comparison operators	✅
AND / OR / NOT	✅
NULL / IS NULL	✅
DISTINCT	✅
LIKE	✅
IN	✅
BETWEEN	✅
AS / aliases	✅
ORDER BY	✅
GROUP BY	✅
Aggregate functions	✅
HAVING	✅
DML	✅
INSERT	✅
UPDATE	✅
DELETE	✅
DCL	✅
GRANT	✅
REVOKE	✅
TCL	✅
COMMIT	✅
ROLLBACK	✅
SAVEPOINT	✅
Joins	✅
Inner / outer / cross / self join	✅
Set operations	✅
Subqueries	✅
Views	✅
Indexes	✅

The notes explicitly classify SQL into DQL, DDL, DML, DCL and TCL, with examples such as CREATE, DROP, ALTER, TRUNCATE, SELECT, INSERT, UPDATE, DELETE, GRANT, REVOKE, COMMIT, ROLLBACK, and SAVEPOINT.

And we've covered the core query progression all the way from:

SELECT
 ↓
WHERE
 ↓
DISTINCT / LIKE / IN / BETWEEN
 ↓
ORDER BY
 ↓
GROUP BY
 ↓
HAVING
 ↓
JOINS
 ↓
SUBQUERIES
 ↓
SET OPERATIONS
 ↓
VIEWS
 ↓
INDEXES
🚀 NOW WE CHANGE MODE

This is where your original goal kicks in.

You do not need another giant theory chapter.

We've built the foundation.

Now our learning loop should become:

CONCEPT
   ↓
INTERVIEW QUESTION
   ↓
SQL 50 PROBLEM
   ↓
YOU ATTEMPT
   ↓
I REVIEW
   ↓
OPTIMIZE / EXPLAIN
   ↓
INTERVIEW VARIATION
   ↓
NEXT PROBLEM

And we'll use the SQL 50 list you gave me, rather than randomly jumping around.

We already conceptually touched many of its required building blocks.

So next, we'll start solving the SQL 50 systematically from #1757 onward, but now I'll make you think like an interviewer:

"What is the question actually asking?" → "Which SQL operation maps to that phrase?" → "Write the query."

That's the skill that will take you from knowing MySQL to actually solving SQL interview problems.

---
part 33

Yes — for the material contained in the notes, we've now covered the full core syllabus. I just checked the uploaded notes again rather than relying on our conversation history.

The notes organize SQL into DQL, DDL, DML, DCL, and TCL, and we've covered those areas.

✅ Our notes coverage
Area	Covered
Database / DBMS / RDBMS / SQL / MySQL	✅
Tables, rows, columns, relationships	✅
CRUD vs SQL command categories	✅
DDL	✅
CREATE, ALTER, DROP, TRUNCATE	✅
Data types	✅
Constraints	✅
PRIMARY KEY	✅
FOREIGN KEY	✅
NOT NULL, UNIQUE, DEFAULT, CHECK	✅
ON DELETE CASCADE / ON UPDATE CASCADE	✅
SELECT / FROM / WHERE	✅
Comparison operators	✅
AND / OR / NOT	✅
NULL / IS NULL	✅
DISTINCT	✅
LIKE	✅
IN	✅
BETWEEN	✅
AS / aliases	✅
ORDER BY	✅
GROUP BY	✅
Aggregate functions	✅
HAVING	✅
INSERT / UPDATE / DELETE	✅
GRANT / REVOKE	✅
Transactions	✅
COMMIT / ROLLBACK / SAVEPOINT	✅
INNER JOIN	✅
Outer joins	✅
CROSS JOIN	✅
Self join	✅
Set operations	✅
UNION / UNION ALL	✅
INTERSECT / EXCEPT concepts	✅
Subqueries	✅
Correlated subqueries	✅
Views	✅
Indexes	✅

The notes explicitly include joins, including inner/outer joins and self joins, followed by set operations.

They also explicitly cover GROUP BY, HAVING, and aggregate functions such as COUNT, SUM, AVG, MAX, and MIN.

And the notes cover DML, DCL, and TCL, including INSERT, UPDATE, DELETE, GRANT, REVOKE, COMMIT, ROLLBACK, and SAVEPOINT.

One important clarification

"Covered" doesn't mean "mastered."

We've covered the theory in the notes. Now we need to turn that knowledge into problem-solving ability.

That's exactly where your original goal comes in:

Master MySQL → solve SQL 50 → become interview-ready.

So I would not add more theory right now.

Our next phase should be:

                NOTES
                  ✅
                  ↓
        SQL 50 PROBLEM SOLVING
                  ↓
       ┌──────────┴──────────┐
       ↓                     ↓
  Easy problems         Medium problems
       ↓                     ↓
  pattern recognition   interview thinking
       └──────────┬──────────┘
                  ↓
           Hard SQL problems
                  ↓
        MOCK INTERVIEWS

And we'll go in the exact SQL 50 order you gave me, starting with:

#1757 — Recyclable and Low Fat Products

But now I won't just give you solutions. I'll train you to look at a problem and immediately identify:

What tables?
    ↓
What columns?
    ↓
What is being asked?
    ↓
Filter or aggregation?
    ↓
JOIN?
    ↓
GROUP BY?
    ↓
Subquery?
    ↓
ORDER BY?
    ↓
Final SQL

So yes: notes first = done. ✅

Now it's time to turn the knowledge into skill.
