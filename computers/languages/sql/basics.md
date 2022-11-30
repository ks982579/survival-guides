Sources:
- [SQL and PostgreSQL: The Complete Developer's Guide](https://www.udemy.com)
	- By: Stephen Grider

# Part 1 - SQL Statements

### Overview

We use databases to store data. We connect to a database, such as a PostgreSQL database with a client, which is software. It can be an API on a server or a utility program. Once we connect a client to a database, we write SQL to query the data, create/add, read, update, or delete.

SQL is the language used to interact with databases. Examples of SQL databases are PostgreSQL, Oracle, MySQL, and MS SQL Server. SQL is more like a standard, and not every database implements the standards 100%, so milage may vary. However, learning SQL for one database system tranfers over very well for many others. 

The four main challenges we face when working with a database are:
1. Writing efficient queries to _retrieve_ information.
2. Designing the schema (or structure) of the database.
3. Understanding when to use _advanced_ features.
4. Managing the database in a production environment.

### Database Design

First focus has to be the design of the database. The design process has three parts:
1. What kind of _thing(s)_ are we storing?
2. What properties does this thing have?
3. What **type** of data does each of the properties contain?

Don't overthink these questions. If we are talking about cities in a country, then the thing we are storing is a **list** of cities. Cities can have properites like a name, population, and area, whose data types are strings and numbers. 

The information tranfers to the schema. We can create a **table** called "cities". Each record, or row, in the table will be a city. The columns will list the properties, which stores the data type specified. 

The main takeaway is that a database can be throught of as a collection of tables. Each table is made of rows and columns, the rows represent records of datas, and the columns hold values for each record. 

### Creating Tables

We won't create an actual database just yet because that is a lot of work. Instead, we are using [pg-sql.com](https://pg-sql.com/), which connects to a dummy database to play with. This scenario is actually an example of a client, the website, connecting to a database.

Let's create a table in SQL:

```SQL
CREATE TABLE cities (
	name VARCHAR(50),
	country VARCHAR(50),
	population INTEGER,
	area INTEGER
);
```

We use keywords, and then name the table "cities". We then must specify each column and its associated data type. A semicolon is also required to end the query. This will create a table called "cities", with columns "name", "country", etc... that store values of strings and integers. 

To breakdown the query, it is made up of **keywords** and **identifiers**. A keyword is a predetermined word by the database that tells it to do something, and is always written in capital letters by convention. An identifier provides the database with the _thing_ we want it to act on, and are written in lower-case by convention. 

`VARCHAR(50)` is short for "variable-character", and the numebr limits the number of characters the field will accept. You will get an error if you try to store something larger than that limit. 

`INTEGER` values are whole numbers, typically made of 32 bits. That means:

$$
2^{32}/2 = 2,147,483,648
$$

Largest positive value is one less the above amount to include 0, and the smallest values is the negative of the above amount. 

### Inserting Data into a Table

part 7