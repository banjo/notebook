# Using Virtual Environments with Python

## Gettings started
Create a folder for a virtual environment inside your project:

```bash
python3 -m venv venv
```

The last `venv` could be anything, it will be the name of the folder that is created for the virtual environment.

## Activate
Virtual environments are activated differently.

```bash
# Bash
source venv/bin/activate

# CMD
venv\Scripts\activate.bat

# Powershell
venv\Scripts\Activate.ps1
```

## Deactivate
```bash
deactivate
```

## Requirements
Use `requirements.txt` to handle dependencies.

```bash
# Save packages to file
pip freeze > requirements.txt

# Install from file
pip install -r requirements.txt
```
