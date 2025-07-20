
# 🐳 Docker Build and Push with GitHub Actions

This project demonstrates how to **automatically build and push a Docker image** to Docker Hub using **GitHub Actions**.

Every time you push changes to the `main` branch, GitHub Actions will:

1. Build your Docker image from the included `Dockerfile`
2. Log in to Docker Hub
3. Push the image to your Docker Hub repository

---

## 📁 Project Structure

```

docker-build-and-push/
├── .github/workflows/docker.yml   # GitHub Actions workflow
├── Dockerfile                     # Docker build file
├── app.py                         # Simple Flask app
└── README.md

````

---

## 🚀 How It Works

### GitHub Workflow Triggers:

- ✅ On every `push` to the `main` branch

### Workflow Steps:

1. **Checkout** the code
2. **Log in** to Docker Hub using secrets
3. **Build** the Docker image
4. **Push** the image to your Docker Hub account

---

## 🐍 Python App (Flask)

`app.py` is a minimal Flask app that returns a greeting:

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "👋 Hello from Docker and GitHub Actions!"
````

---

## 🐳 Dockerfile

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY app.py .

RUN pip install flask

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## 🔐 GitHub Secrets Setup

Before the workflow can push to Docker Hub, add these **repository secrets** in:

**Settings → Secrets and Variables → Actions → New repository secret**

| Name              | Description                    |
| ----------------- | ------------------------------ |
| `DOCKER_USERNAME` | Your Docker Hub username       |
| `DOCKER_PASSWORD` | Your Docker Hub password/token |

---

## ⚙️ Run Locally (Optional)

If you want to test locally before pushing:

```bash
# Build
docker build -t yourname/myapp .

# Run
docker run -p 5000:5000 yourname/myapp
```

Then visit: [http://localhost:5000](http://localhost:5000)

---

## 📦 Docker Hub Output

Once successful, your image will be available at:

```
docker.io/<your-docker-username>/myapp:latest
```

You can pull and run it anywhere using:

```bash
docker pull <your-docker-username>/myapp:latest
docker run -p 5000:5000 <your-docker-username>/myapp
```

---

## 💡 Ideas to Extend

* Add version tags using Git tags (`v1.0.0`, etc.)
* Push to **GitHub Container Registry (GHCR)** instead of Docker Hub
* Deploy the image to a VPS, Kubernetes, or AWS
* Add automated tests before building

---

✅ This is a great first step to automate your container delivery pipeline.

Happy building & shipping! 🚢

```

---

Let me know if you want a version for **Node.js**, **multi-stage builds**, or **automated deployments** next!
```
