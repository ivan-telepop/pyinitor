# pyinitor
**pyinitor** script that initiates default python project with files and venv then opens project in vscode - `pyinitor 3.12 ~/projects/my_app`

**pyinitor** скрипт для инициации Python проекта c дефолтным набором файлов, виртуальным окружением, + открывается в VS Code - `pyinitor 3.12 ~/projects/my_app`

---

Howto:

- create script `pyinitor` put these steps to run in it 

```bash
#!/bin/bash

if [ "$#" -ne 2 ]; then
    echo "Running script: pyinitor <python_version> <project_path>"
    exit 1
fi

PY_VERSION="$1"
PROJECT_PATH="$2"

# Creates project
mkdir -p "$PROJECT_PATH"
cd "$PROJECT_PATH" || exit 1

# creates virtualenv
virtualenv -p python$PY_VERSION venv

# Files in project
echo "# Environment variables" > .env
echo "# $(basename "$PROJECT_PATH")" > README.md

cat > .gitignore <<EOL
__pycache__/
*.pyc
venv/
.env
.DS_Store
EOL

cat > .dockerignore <<EOL
__pycache__/
*.pyc
venv/
.env
.DS_Store
EOL

touch requirements.txt

cat > main.py <<EOL
def main():
    print("Hello, world!")


if __name__ == "__main__":
    main()
EOL

echo "✅ Python project is created $PROJECT_PATH"

cd "$PROJECT_PATH"

# opening in vscode
code .

```


- move it in `sudo mv pyinitor /usr/local/bin/`
  
- change access mode, run `chmod +x pyinitor`

- run it `pyinitor 3.12 ~/projects/my_app`

Result will be like:

```bash
.env
README.md
.gitignore
.dockerignore
requirements.txt
main.py
venv/
```
---
simple & comfort !



