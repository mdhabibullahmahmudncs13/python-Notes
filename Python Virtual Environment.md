# Python Virtual Environment

Virtual environments create isolated Python environments for projects.

## Why Use Virtual Environments?

- Isolate project dependencies
- Avoid package conflicts
- Different Python versions per project
- Easy to share project requirements

## Creating Virtual Environment

```bash
# Using venv (Python 3.3+)
python -m venv myenv

# Or
python3 -m venv myenv
```

## Activating Virtual Environment

```bash
# Windows
myenv\Scripts\activate

# macOS/Linux
source myenv/bin/activate

# You'll see (myenv) in your prompt
```

## Deactivating

```bash
deactivate
```

## Installing Packages

```bash
# After activation
pip install package_name

# Install multiple
pip install numpy pandas matplotlib

# From requirements.txt
pip install -r requirements.txt
```

## requirements.txt

```bash
# Generate requirements.txt
pip freeze > requirements.txt

# Install from requirements.txt
pip install -r requirements.txt
```

Example `requirements.txt`:
```
numpy==1.21.0
pandas==1.3.0
matplotlib==3.4.2
```

## Using virtualenv (Alternative)

```bash
# Install virtualenv
pip install virtualenv

# Create environment
virtualenv myenv

# Activate (same as venv)
source myenv/bin/activate  # Linux/Mac
myenv\Scripts\activate     # Windows
```

## Best Practices

```bash
# Create venv in project directory
cd myproject
python -m venv venv

# Add venv to .gitignore
echo "venv/" >> .gitignore

# Always activate before working
source venv/bin/activate

# Install packages
pip install -r requirements.txt

# Work on project
# ...

# Deactivate when done
deactivate
```

## Conda Environments (Alternative)

```bash
# Create
conda create --name myenv python=3.9

# Activate
conda activate myenv

# Install packages
conda install numpy pandas

# Deactivate
conda deactivate

# Export
conda env export > environment.yml

# Import
conda env create -f environment.yml
```

---

**Related:** [[Python PIP]] | [[Python Modules]] | [[Python Get Started]]
