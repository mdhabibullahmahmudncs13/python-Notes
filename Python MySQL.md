# Python MySQL

Work with MySQL databases using Python.

## Installation

```bash
pip install mysql-connector-python
```

## Connect to Database

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="username",
    password="password",
    database="mydatabase"
)

print(mydb)
```

## Create Database

```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="username",
    password="password"
)

mycursor = mydb.cursor()
mycursor.execute("CREATE DATABASE mydatabase")
```

## Create Table

```python
mycursor = mydb.cursor()

mycursor.execute("""
CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    address VARCHAR(255)
)
""")
```

## Insert Data

```python
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("John", "Highway 21")

mycursor.execute(sql, val)
mydb.commit()

print(mycursor.rowcount, "record inserted")
```

## Insert Multiple Rows

```python
sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = [
    ("Peter", "Lowstreet 4"),
    ("Amy", "Apple st 652"),
    ("Hannah", "Mountain 21")
]

mycursor.executemany(sql, val)
mydb.commit()
```

## Select Data

```python
# Select all
mycursor.execute("SELECT * FROM customers")
result = mycursor.fetchall()

for row in result:
    print(row)

# Select specific columns
mycursor.execute("SELECT name, address FROM customers")

# Fetch one
mycursor.execute("SELECT * FROM customers")
result = mycursor.fetchone()
print(result)
```

## Where Clause

```python
sql = "SELECT * FROM customers WHERE address = %s"
val = ("Highway 21",)

mycursor.execute(sql, val)
result = mycursor.fetchall()
```

## Order By

```python
sql = "SELECT * FROM customers ORDER BY name"
mycursor.execute(sql)

# Descending
sql = "SELECT * FROM customers ORDER BY name DESC"
```

## Delete

```python
sql = "DELETE FROM customers WHERE address = %s"
val = ("Highway 21",)

mycursor.execute(sql, val)
mydb.commit()
```

## Update

```python
sql = "UPDATE customers SET address = %s WHERE address = %s"
val = ("Valley 345", "Highway 21")

mycursor.execute(sql, val)
mydb.commit()
```

## Limit

```python
sql = "SELECT * FROM customers LIMIT 5"
mycursor.execute(sql)

# Offset
sql = "SELECT * FROM customers LIMIT 5 OFFSET 2"
```

## Join

```python
sql = """
SELECT users.name, products.name
FROM users
INNER JOIN products ON users.id = products.user_id
"""

mycursor.execute(sql)
result = mycursor.fetchall()
```

---

**Related:** [[File and Database Handling]] | [[Python MongoDB]] | [[Python JSON]]
