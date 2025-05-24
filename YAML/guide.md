# Complete YAML Guide

YAML (YAML Ain’t Markup Language) is a human-readable data serialization format, designed to be easy to write and understand. It’s widely used for configuration files, data exchange, and is a staple in DevOps tooling (Kubernetes, Ansible, Docker Compose, CI/CD pipelines, etc.)

# Basic Syntax and Formatting

YAML’s syntax is defined by a few simple rules:

Indentation: Use spaces (not tabs) to denote nesting. Two spaces per level is common. For example, the keys under person: are indented to show they belong to that mapping.

Key–Value Pairs: Write mappings as key: value. Keys are usually alphanumeric (use quotes only if needed).

Lists: Start list items with a hyphen (-). Each - begins a new element in the sequence.

Comments: Precede comments with #. Anything on a line after # is ignored by YAML parsers.


```yaml
# Basic YAML example
Book:
  name: Unstoppable
  author: Sk-publication
  language:
    - English
    - Hindi
```
# Core Data Types
YAML natively supports several core data types:

Scalars: These include strings, integers, floats, booleans, and nulls. YAML usually auto-detects types:

Strings: Plain (unquoted) strings (e.g. title: Hello), or quoted with " or ' for special characters. Escape sequences (like \n) work in double-quoted strings.

Numbers: Integers (age: 42) and floats (pi: 3.14159) are written without quotes.

Booleans: Represented as true/false (lowercase).

Null: Use null or ~ to denote a null value.

Sequences (Lists): Ordered collections denoted by - entries. E.g.:

```yaml
#Sample Code
app:
  name: MyApp
  version: 1.0
  active: true
  description: "A sample YAML file"
  nullable_field: ~
  tags:
    - backend
    - production
  limits:
    cpu: 2
    memory: 512
```
### 🔹 Key-Value Pair
```yaml
name: John
age: 30
```
### 🔹 Nested Values (Maps inside maps)
```yaml
person:
  name: Alice
  age: 28
```
### 🔹 Lists
```yaml
colors:
  - red
  - green
  - blue
```
### 🔹 List of Maps
```yaml
employees:
  - name: John
    role: Developer
  - name: Jane
    role: Manager
```
# Advanced Features

### 🔁 1. Anchors (&) and Aliases (*) — Reuse Code Without Rewriting

YAML lets you **reuse parts of your configuration** to avoid repeating the same data again and again.

```yaml
defaults: &default_settings
  retries: 3
  timeout: 30

service1:
  <<: *default_settings
  host: example.com
```

- `&default_settings`: Creates an **anchor** named `default_settings`.
- `*default_settings`: **References** the anchor.
- `<<: *default_settings`: **Merges** the key-values into `service1`.

**Why use this?**  
To keep your YAML DRY (**Don't Repeat Yourself**) and more maintainable.

---

### 🧾 2. Multi-line Strings — Write Big Text Blocks

If you need to include logs, descriptions, or other long texts, YAML supports two styles:

#### Literal Style (`|`) — Keeps New Lines
```yaml
note: |
  This is a multiline
  string in literal style.
```
Output keeps line breaks **as written**.

#### Folded Style (`>`) — Joins Lines with Spaces
```yaml
summary: >
  This is a folded
  style multiline string.
```
Output becomes: `This is a folded style multiline string.`

**When to use:**
- Use `|` when formatting matters (e.g., logs)
- Use `>` for paragraphs or messages

---

### 🧩 3. Complex/Nested Structures — Real-World Format

YAML supports nested data like lists inside maps and vice versa.

```yaml
services:
  - name: web
    replicas: 2
    ports:
      - containerPort: 80

  - name: db
    replicas: 1
    ports:
      - containerPort: 5432
```

- `services` is a **list**.
- Each item is a **map** with its own keys.
- Inside each service, you can **nest deeper** (e.g., ports).

**Use Case:** Common in Kubernetes, Docker Compose, and Ansible.

---

### 🧱 4. Block vs Flow Style — Two Ways to Write the Same Thing

#### Block Style (preferred):
```yaml
colors:
  - red
  - green
  - blue

user:
  name: Alice
  age: 30
```

#### Flow Style (compact):
```yaml
colors: [red, green, blue]
user: { name: "Alice", age: 30 }
```

- Block style is easier to read.
- Flow style is shorter, useful for small/inline data.

---

### 📄 5. Multiple YAML Documents in One File

You can include more than one YAML document in a single file using `---` to separate them.

```yaml
# Document 1
---
name: Document1
value: 123

# Document 2
---
name: Document2
value: 456
...
```

- `---` starts a new document
- `...` ends a document (optional)

**Use Case:** Kubernetes multi-resource files, CI/CD workflows

---
## 🚀 5. Industry usage

### 🔧 Kubernetes
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

### 🐳 Docker Compose
```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  app:
    build: .
    volumes:
      - .:/app
```

### 🤖 GitHub Actions
```yaml
name: CI Pipeline
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: npm test
```

### ⚙️ Ansible Playbook
```yaml
- hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

---

## 📌 Tips for Writing YAML

- Always use **2 spaces** for indentation.
- Don’t use **tabs** — YAML will fail.
- Validate with linters or CI before deploying.

---
Happy YAMLing! 🎉
