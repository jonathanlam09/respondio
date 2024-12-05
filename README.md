# Respondio Project

This repository contains the backend (Node.js), frontend (React), and database configuration for the Respondio project. Follow the instructions below to get started.

## Prerequisites

Before you begin, make sure you have the following installed:

- **Docker**: For running MySQL and other services in containers.
- **Git**: To clone the repository.

## Setup Instructions

### 1. Clone the Repository

Clone the repository using the following command:

```bash
git clone https://github.com/jonathanlam09/respondio.git
cd respondio
```

### 2. Build and Start Containers with Docker Compose

Make sure you are in the project root directory where the `docker-compose.yml` file is located. Then, build and run the containers using:

```bash
docker-compose up --build
```

This command will:
- Build the Docker images.
- Start the containers for your Node.js backend, React frontend, MySQL database, and Redis.

### 3. Access MySQL Container

To interact with the MySQL database container, you can run the following command:

```bash
docker exec -it respondio-mysql mysql -u root
```

This will open the MySQL command line interface.

### 4. Create the Database and Tables

Once you are inside the MySQL container, run the following commands to create the `respondio` database and the necessary tables (`users` and `notes`).

```sql
CREATE DATABASE respondio;
USE respondio;

CREATE TABLE users (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    firstName VARCHAR(255),
    lastName VARCHAR(255),
    email VARCHAR(255),
    contact VARCHAR(12),
    password VARCHAR(255),
    active TINYINT(1),
    isFirstLogin TINYINT(1) DEFAULT 1,
    createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updatedAt TIMESTAMP NULL DEFAULT NULL,
    createdBy INT UNSIGNED,
    updatedBy INT UNSIGNED NULL DEFAULT NULL
);

CREATE TABLE notes (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    usersId INT UNSIGNED,
    type INT UNSIGNED,
    remarks TEXT,
    active TINYINT(1) DEFAULT 1,
    createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updatedAt TIMESTAMP NULL DEFAULT NULL,
    createdBy INT UNSIGNED,
    updatedBy INT UNSIGNED NULL DEFAULT NULL,
    FOREIGN KEY (usersId) REFERENCES users(id)
);
```

---

### **Accessing the Application**

- **React (Frontend)**: Access the React app at `http://localhost:3001`.
- **Node.js (Backend)**: The API is available at `http://localhost:3000`.

