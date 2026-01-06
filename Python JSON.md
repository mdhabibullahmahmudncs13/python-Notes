# Python JSON

Work with JSON data in Python.

## Import JSON Module

```python
import json
```

## Parse JSON (Deserialize)

Convert JSON string to Python object:

```python
import json

# JSON string
json_string = '{"name": "John", "age": 30, "city": "New York"}'

# Parse to dict
data = json.loads(json_string)

print(data["name"])  # John
print(type(data))    # <class 'dict'>
```

## Convert to JSON (Serialize)

Convert Python object to JSON string:

```python
import json

# Python dict
data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

# Convert to JSON
json_string = json.dumps(data)
print(json_string)
```

## Format JSON

```python
import json

data = {"name": "John", "age": 30}

# Pretty print
json_string = json.dumps(data, indent=4)
print(json_string)

# Sort keys
json_string = json.dumps(data, indent=4, sort_keys=True)
```

## Read JSON File

```python
import json

with open("data.json", "r") as file:
    data = json.load(file)
    print(data)
```

## Write JSON File

```python
import json

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

with open("data.json", "w") as file:
    json.dump(data, file, indent=4)
```

## Python to JSON Conversion

```python
dict -> JSON object
list -> JSON array
tuple -> JSON array
str -> JSON string
int -> JSON number
float -> JSON number
True -> true
False -> false
None -> null
```

---

**Related:** [[Python Dictionaries]] | [[Python File Handling]] | [[Python]]
