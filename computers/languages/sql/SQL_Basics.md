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

There are also operators and functions to manipulate strings
- The `||` operator joins two strings together.
- The `CONCAT()` function joins two strings.
- The `LOWER()` gives a lower case string.
-  `LENGTH()` gives number of character in a string.
- `UPPER()` gives an upper case string. 

```SQL
SELECT name || ', ' || country AS location FROM cities;
```

That's not a great example, but can give strings like "Tokyo, Japan". Again, the single quotes are stressed. We also use the `AS` keyword to give the results a column name of "location". 

We can do the same thing with a function.

```SQL
SELECT CONCAT(name, ', ', country) AS location FROM cities;
```

This is essentially the same results. 

# Part 2 - Filtering Records

### Filtering Rows with "Where"

If we need to filter out records that do not fit a certain criteria, such as cities that are smaller than a particular area, we use the `WHERE` keyword. 

```SQL
SELECT name, area FROM cities WHERE area > 4000;
```

Write the bulk of the query to the left (or above) the `WHERE` statement, and then the filtering statement to the right. 

We can discuss how a database management system, like PostgreSQL, exectutes a statement like this as it's not exaclty read left to right. The _actual steps_ taken are:
1. Fetch the table (gets the data source).
2. Apply the filter (criteria).
3. Take only necessary columns. 

That probably means we don't need to include the column we are filtering on because all of the columns are pulled for filtering first. You will need to understand the order of operations for writing more advanced queries. 

The `WHERE` keyword allows us to filter down the set of results we get from a query. We can make use of many different operators in a `WHERE` statement, and some keywords.
- Operators: =, <, >, <=, >=, <>, !=.
- Keywords: `IN`, `BETWEEN`, `NOT IN`. 

Most operators are (probably) self-explanitory. There are some neat options like seeing if a value is `IN` a list or not. Note that unlike most programming languages, we use the single equal sign as a comparison because it's not an assignment operator. The `!=` and `<>` are the same way of writing the same thing. 

### Compound `WHERE` Clauses

video 15