# MultiContainer_Bakery
A containerized full-stack application simulating a bakery ordering system using Docker, PostgreSQL, Flask, HTML/CSS/JS, Redis, and RabbitMQ. Built as part of an academic assignment to demonstrate multi-component orchestration with Docker Compose.

---

## 🔧 System Architecture Overview

![image](https://github.com/user-attachments/assets/beec305d-54db-4b1b-bad3-531862fa36e4)

---

## 🚀 Setup Instructions

### ✅ Prerequisites
- Docker Desktop (WSL2 enabled for Windows users)

### 📁 Folder Structure

![image](https://github.com/user-attachments/assets/68723fe5-8c84-4873-bab0-a65e8be557fa)


```

### 🧱 Build and Run

```bash
cd bakery-system
docker compose up --build
```

### 🌐 Access Points

- 🌍 Website: [http://localhost:8080](http://localhost:8080)
- 🔗 Backend API: [http://localhost:5000](http://localhost:5000)
- 📨 RabbitMQ UI: [http://localhost:15672](http://localhost:15672) (guest/guest)

---

## 🔌 API Documentation

### `GET /products`
- **Returns**: List of available bakery items
- **Note**: Redis is used to cache results for performance boost

### `POST /order`
- **Payload**: Array of products  
  Example:  
  ```json
  [ { "name": "Gulab Jamun", "price": 50 }, { "name": "Rasgulla", "price": 40 } ]
  ```
- **Response**:
  ```json
  { "message": "Order placed successfully", "order_id": 1 }
  ```
- **Note**: Sends order info to RabbitMQ (demo integration)

### `GET /status/<order_id>`
- **Returns**:
  ```json
  { "order_id": 1, "status": "confirmed" }
  ```

### `PUT /status/<order_id>`
- **Payload**:
  ```json
  { "status": "confirmed" }
  ```
- **Function**: Updates order status manually

### `GET /health`
- **Checks**: PostgreSQL, Redis, and RabbitMQ connectivity
- **Used for**: Container health checks in Docker Compose

---

## 📸 Screenshot Placeholders

### 🖼️ Home Page - Product List
![image](https://github.com/user-attachments/assets/b232c458-576c-471c-8fa7-14069869f84e)

### 🖼️ Order Placement
![image](https://github.com/user-attachments/assets/cd24a1e4-1fb2-4c60-bcb7-d35b2ddebeef)

### 🖼️ Order Status
![image](https://github.com/user-attachments/assets/12bd345d-5c68-41fb-a7f0-fdc0a8489558)
![image](https://github.com/user-attachments/assets/b52f700b-d43c-4797-8e0d-433564c623c5)

### 🖼️ Docker Dashboard
![image](https://github.com/user-attachments/assets/c7ebe11d-bb1d-4e7d-b82d-022f38ec31c8)

### 🖼️ RabbitMQ Queue
![image](https://github.com/user-attachments/assets/50bbcc4d-c480-4007-8b8c-bc5413facd23)
![image](https://github.com/user-attachments/assets/8b36c6b5-4753-45c4-ac97-8d9fbfc6e262)


---

## 🧠 Design Decisions (Brief Report)

- ✅ **PostgreSQL**: Chosen as a reliable SQL-based transactional DB for order tracking.
- ✅ **Flask (Python)**: Selected for simplicity and RESTful API design.
- ✅ **Redis**: Integrated to reduce DB hits and improve `/products` response time.
- ✅ **RabbitMQ**: Added to simulate scalable, event-driven background task architecture.
- ✅ **Docker Compose**: Used to isolate and orchestrate all services across networks/volumes.
- ✅ **Health Checks**: Implemented for backend, frontend, DB, Redis, and RabbitMQ to monitor service health.
- ✅ **Logging**: Handled using Python's `logging` module (backend) and container stdout (worker).

---

## 📦 Notes

Use the following commands to inspect and verify the database:

```bash
docker ps
docker exec -it <db-container-name> psql -U ayush -d bakery_db
```

Run inside the container:
```sql
SELECT * FROM orders;
```

---



 
