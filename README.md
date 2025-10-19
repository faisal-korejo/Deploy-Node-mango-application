# 🗄️ Node.js + MongoDB CRUD App (Docker + Kubernetes)

This is a simple **Node.js + Express + MongoDB** CRUD (Create, Read, Update, Delete) application demonstrating:
- Connecting a Node.js API to MongoDB
- Containerizing the app with **Docker**
- Deploying both app and database with **Docker Compose** or **Kubernetes (Minikube)**

---

## 🚀 Features

- RESTful API built with **Express.js**
- MongoDB integration using **Mongoose**
- Fully containerized with Docker
- Works on:
  - Local environment (Node)
  - Docker network
  - Kubernetes cluster (Minikube)

---

## 🧩 Project Structure

```
.
├── app.js               # Main server file
├── package.json         # Node.js dependencies
├── Dockerfile           # App container definition
├── app.yml              # Kubernetes deployment and service manifest
└── README.md            # Project documentation
```

---

## ⚙️ Prerequisites

Before running the project, make sure you have:

- [Node.js](https://nodejs.org/) v18+ (optional if you run via Docker)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/) (optional)
- [Minikube](https://minikube.sigs.k8s.io/docs/) (for Kubernetes deployment)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

---

## 🐳 Run with Docker

### 1️⃣ Build and Run the MongoDB container
```bash
docker network create my-net

docker run -d   --name my-mongo   --network my-net   -p 27017:27017   mongo:6
```

### 2️⃣ Build and Run the Node.js app container
```bash
docker build -t node-mongo-app:1.0 .
```

Then run:
```bash
docker run -d   --name myapp   --network my-net   -p 3000:3000   node-mongo-app:1.0
```

The app will be available at 👉 [http://localhost:3000](http://localhost:3000)

---

## 🧱 Run with Docker Compose (optional)

If you have a `docker-compose.yml`, you can start everything with one command:
```bash
docker-compose up --build
```

---

## ☸️ Run with Kubernetes (Minikube)

### 1️⃣ Start Minikube
```bash
minikube start
```

### 2️⃣ Apply Kubernetes manifest
```bash
kubectl apply -f app.yml
```

### 3️⃣ Verify deployment
```bash
kubectl get pods
kubectl get svc
```

### 4️⃣ Access the app
If you exposed the service as `NodePort`, run:
```bash
minikube service myapp-service
```

---

## 🔗 Example MongoDB Connection

In your Node.js app (`app.js`), the connection typically looks like:
```js
mongoose.connect('mongodb://my-mongo:27017/mydb', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

> Note: When running in Docker or Kubernetes, **don’t use `localhost`** — use the **service name or container name** (`my-mongo`) as the MongoDB hostname.

---

## 🧠 Common Issues

| Issue | Cause | Fix |
|-------|--------|-----|
| `ECONNREFUSED 127.0.0.1:27017` | App trying to connect to MongoDB on localhost | Use `my-mongo` as hostname instead of `localhost` |
| `Container name already in use` | Old container still running | `docker rm -f $(docker ps -aq)` |
| `Kubernetes openapi timeout` | Minikube not started | Run `minikube start` again |

---

## 🧰 Tech Stack

- **Node.js** – Backend runtime
- **Express.js** – Web framework
- **MongoDB + Mongoose** – Database and ORM
- **Docker** – Containerization
- **Kubernetes (Minikube)** – Orchestration

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

## 👨‍💻 Author

**Faisal Zama**  
📧 [your-email@example.com]  
💼 [GitHub Profile](https://github.com/yourusername)

---
