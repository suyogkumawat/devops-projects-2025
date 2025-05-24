# 🌟 Complete YAML Guide for DevOps Engineers

YAML (YAML Ain’t Markup Language) is a **human-readable data format** commonly used for configuration files. It's widely used in **DevOps tools** like **Kubernetes**, **Docker Compose**, **Ansible**, and **GitHub Actions**.

This guide walks you from **YAML basics to advanced use cases** in real-world DevOps scenarios.

---

## 📘 What is YAML?

YAML is a **data serialization format** like JSON or XML, but it's more human-friendly and readable.

### ✅ Why YAML?
- Clean and readable
- Easy to write and edit manually
- Widely adopted in DevOps tools

---

## 🟦 1. YAML Basics

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

> 🔸 **Indentation is critical in YAML. Use 2 spaces. Never use tabs.**

---

## 🧰 2. Advanced YAML Features

### 🔁 Anchors (&) and Aliases (*) — Reuse blocks
```yaml
defaults: &default_settings
  retries: 3
  timeout: 30

service1:
  <<: *default_settings
  host: example.com
```

### 🧾 Multi-line Strings
- **Literal style (`|`)** keeps line breaks:
```yaml
note: |
  This is a line.
  This is another line.
```
- **Folded style (`>`)** converts newlines to spaces:
```yaml
summary: >
  This is folded.
  It becomes one line.
```

### 🧩 Complex Nesting Example
```yaml
services:
  - name: frontend
    image: nginx
    ports:
      - 80
  - name: backend
    image: node
    ports:
      - 3000
```

---

## 🔃 3. Block vs Flow Style

### Block Style (easy to read)
```yaml
fruits:
  - apple
  - banana
  - orange
```
### Flow Style (compact)
```yaml
fruits: [apple, banana, orange]
```

---

## 📄 4. Multiple YAML Documents

Useful in Kubernetes and CI/CD:

```yaml
# Document 1
---
apiVersion: v1
kind: Service
metadata:
  name: my-service

# Document 2
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
```

Use `---` to separate documents.

---

## 🚀 5. YAML in Real Projects

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

## ✅ Summary Table

| Feature               | Purpose                             | Syntax Example                      |
|----------------------|-------------------------------------|-------------------------------------|
| Key-Value             | Basic config                        | `name: John`                        |
| List                 | Sequence of values                  | `- red`                             |
| Map of Maps           | Nesting                            | `person:
  name: Alice`            |
| Anchors & Aliases     | Reuse sections                     | `&anchor`, `*alias`                 |
| Block/Flow Style      | Readable or compact syntax         | `- apple` vs `[apple, banana]`      |
| Multiline Strings     | Long text or logs                  | `|` and `>`                         |
| Multi-doc YAML        | Multiple resources in one file     | `---` separator                     |
| Real Project Example  | Use in Kubernetes, Ansible, etc.   | `kind: Pod`, `version: "3"`         |

---

## 📌 Tips for Writing YAML

- Always use **2 spaces** for indentation.
- Don’t use **tabs** — YAML will fail.
- Validate with linters or CI before deploying.

---

## 🙌 Final Thoughts

YAML is a simple yet powerful language for defining infrastructure and configurations. Mastering YAML helps you become more effective with tools like Kubernetes, Ansible, Docker, and GitHub Actions.

---

🔗 Need examples from your projects or want to practice? Fork this README and start customizing!

Happy YAMLing! 🎉