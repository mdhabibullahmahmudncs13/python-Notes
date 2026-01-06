# Python MongoDB

Work with MongoDB databases using Python.

## Installation

```bash
pip install pymongo
```

## Connect to MongoDB

```python
import pymongo

client = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = client["mydatabase"]
```

## Create Database

```python
# Database created when first document inserted
mydb = client["mydatabase"]
```

## Create Collection

```python
mycol = mydb["customers"]
```

## Insert Document

```python
# Insert one
doc = {"name": "John", "address": "Highway 37"}
result = mycol.insert_one(doc)
print(result.inserted_id)

# Insert many
docs = [
    {"name": "Amy", "address": "Apple st 652"},
    {"name": "Hannah", "address": "Mountain 21"}
]
result = mycol.insert_many(docs)
print(result.inserted_ids)
```

## Find Documents

```python
# Find one
result = mycol.find_one()
print(result)

# Find all
for doc in mycol.find():
    print(doc)

# Find with filter
query = {"address": "Highway 37"}
results = mycol.find(query)

for doc in results:
    print(doc)
```

## Query with Operators

```python
# Greater than
query = {"age": {"$gt": 18}}
results = mycol.find(query)

# Regex
query = {"name": {"$regex": "^J"}}
results = mycol.find(query)

# Multiple conditions
query = {"$and": [
    {"age": {"$gt": 18}},
    {"city": "New York"}
]}
```

## Sort

```python
# Ascending
results = mycol.find().sort("name")

# Descending
results = mycol.find().sort("name", -1)
```

## Delete

```python
# Delete one
query = {"address": "Highway 37"}
mycol.delete_one(query)

# Delete many
query = {"address": {"$regex": "^S"}}
result = mycol.delete_many(query)
print(result.deleted_count)

# Delete all
result = mycol.delete_many({})
```

## Update

```python
# Update one
query = {"address": "Highway 37"}
newvalues = {"$set": {"address": "Canyon 123"}}
mycol.update_one(query, newvalues)

# Update many
query = {"address": {"$regex": "^S"}}
newvalues = {"$set": {"address": "Updated"}}
result = mycol.update_many(query, newvalues)
print(result.modified_count)
```

## Limit

```python
# Limit results
results = mycol.find().limit(5)

for doc in results:
    print(doc)
```

---

**Related:** [[File and Database Handling]] | [[Python MySQL]] | [[Python JSON]]
