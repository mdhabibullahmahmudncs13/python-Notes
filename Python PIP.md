# Python PIP

PIP is the package installer for Python.

## Check PIP Version

```bash
pip --version
```

## Install Package

```bash
pip install package_name

# Specific version
pip install package_name==1.2.3

# Minimum version
pip install 'package_name>=1.2.3'
```

## Uninstall Package

```bash
pip uninstall package_name
```

## List Installed Packages

```bash
pip list
```

## Show Package Info

```bash
pip show package_name
```

## Upgrade Package

```bash
pip install --upgrade package_name

# Upgrade pip itself
pip install --upgrade pip
```

## Install from requirements.txt

```bash
pip install -r requirements.txt
```

## Create requirements.txt

```bash
pip freeze > requirements.txt
```

## Common Packages

```bash
# Data science
pip install numpy pandas matplotlib

# Web frameworks
pip install django flask

# Database
pip install pymongo mysql-connector-python

# Utilities
pip install requests beautifulsoup4
```

---

**Related:** [[Python Modules]] | [[Python Virtual Environment]] | [[Python]]
