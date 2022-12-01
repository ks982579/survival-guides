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

After creating a table, we insert data into a table with the `INSERT INTO` keywords, followed by the name of the table and the columns we will insert data into.

```SQL
INSERT INTO cities (name, country, population, area)
VALUES ('Tokyo', 'Japan', 38505000, 8223);
```

Then, as seen, we use the `VALUES` keyword, and list out the values to insert in **order**. Don't forget your semicolon.

```SQL
INSERT INTO cities (name, country, population, area)
VALUES 
	('Tokyo', 'Japan', 38505000, 8223)
	('Shanghai', 'China', 22125000, 4015);
```

That is how you can add multiple records with one query. 

He also made it a point that the text is enclosed in _single quotes_.

### Retrieving Data with Select

To pull information out of a table, we use the `SELECT` and `FROM` statements.

```SQL
SELECT * FROM cities;
```

The \* is a wild-card meaning "everything". With the above statement, we literally request everything from the 'cities' table. It's worth noting that the \* is requesting all of the columns in the table.

```SQL
SELECT name, country FROM cities;
```

We can request specific column names as well. You can change the order you request the information to also change the order it is received. You can also list the same column multiple times, and it will be returned multiple times. 

### Calculated Columns

With SQL, we can also _transform_ or _process_ data before we receive it. Consider finding the "population density" of our cities, which is $population/area$. 

```SQL
SELECT name, population / area FROM cities;
```

We are requesting the columns, but specifying that we want to perform an operation. Think of it like creating a new column that isn't in the database. The above will (should) give you the information requested, but the column name won't look right. 

We can use many different operators:
- add $\rightarrow +$
- subtract $\rightarrow -$
- multiply -> \*
- divide -> /
- exponent -> ^
- square root -> |/
- Absolute Value -> @
- Remainder -> %

There are probably even more, but these will be most common. 

```SQL
SELECT name, population / area AS population_density
FROM cities;
```

The above uses the `AS` keyword to rename the column to something more human readable. 

### String Operators and Functions

part 12