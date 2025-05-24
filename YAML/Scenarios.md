# 🔧 Advanced YAML Use Cases in Industry-Level DevOps Projects

This section extends your YAML knowledge with real-world, advanced scenarios used in **production environments**, covering tools like **Kubernetes**, **Helm**, **GitHub Actions**, **Ansible**, **Docker Compose**, and **CI/CD workflows**.

---

## 🚢 1. Kubernetes: Multi-Resource Configuration

### 🧩 Deployment + Service + ConfigMap + Secret

```yaml
# configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_MODE: production
  APP_TIMEOUT: "30"

---

# secret.yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  DB_PASSWORD: c3VwZXJzZWNyZXQ=  # base64 encoded

---

# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
        - name: app-container
          image: myapp:v1
          envFrom:
            - configMapRef:
                name: app-config
            - secretRef:
                name: app-secret
          ports:
            - containerPort: 80

---

# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: web-app-service
spec:
  type: LoadBalancer
  selector:
    app: web
  ports:
    - port: 80
      targetPort: 80
```

---

## ⚓ 2. Helm Chart: Templated YAML for Kubernetes

`values.yaml`
```yaml
replicaCount: 2

image:
  repository: myapp
  tag: v1

service:
  type: ClusterIP
  port: 80
```

`deployment.yaml` (Helm template)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "mychart.fullname" . }}
spec:
  replicas: {{ .Values.replicaCount }}
  template:
    spec:
      containers:
        - name: myapp
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
```

---

## 🐳 3. Docker Compose: Multi-Service App with Networks & Volumes

```yaml
version: "3.8"

services:
  db:
    image: postgres:14
    environment:
      POSTGRES_PASSWORD: example
    volumes:
      - db_data:/var/lib/postgresql/data

  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
    environment:
      DATABASE_URL: postgres://postgres:example@db:5432/mydb

volumes:
  db_data:
```

---

## ⚙️ 4. Ansible Playbook with Variables, Handlers, and Loops

```yaml
- name: Configure Web Servers
  hosts: web
  vars:
    nginx_ports:
      - 80
      - 443
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Create custom index.html
      copy:
        content: "<h1>Welcome!</h1>"
        dest: /var/www/html/index.html
      notify: Restart Nginx

    - name: Open ports
      ufw:
        rule: allow
        port: "{{ item }}"
      loop: "{{ nginx_ports }}"

  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
```

---

## ⚙️ 5. GitHub Actions: Matrix Build, Conditional Jobs, and Environments

```yaml
name: Build and Test

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14, 16, 18]
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm test

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Deploy to Production
        run: ./deploy.sh
```

---

## 📦 6. CI/CD: GitLab CI Example

```yaml
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - echo "Building project"

test:
  stage: test
  script:
    - echo "Running tests"

deploy:
  stage: deploy
  only:
    - main
  script:
    - echo "Deploying to production"
```

---

## 📊 7. Monitoring Stack: Prometheus Config in YAML

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
```

---

## 🧠 Final Thoughts

Mastering YAML syntax is essential for modern DevOps workflows. These examples reflect **real production use cases**, helping you deploy, monitor, and manage infrastructure and applications effectively.

---

👉 Next Step: Use these examples to build your own environments, or integrate them into CI/CD pipelines or cloud-native deployments.