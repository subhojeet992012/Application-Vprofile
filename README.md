---

# Application-Vprofile

This repository contains Docker files to create an application that utilizes a complete tech stack: **Web Server** → **App Server (Tomcat)** → **Memcached** → **Database (MySQL)** → **RabbitMQ**.

The following steps describe how to set up the application and modify configuration files for internal communication.

---

## Configuration Steps

### 1. **Edit the `application.properties` File**

The **`application.properties`** file is used to configure the connections for the database, Memcached, and RabbitMQ servers. You'll need to update the internal IP addresses for these services to ensure proper communication.

**Path:** `webapps/ROOT/WEB-INF/classes/application.properties`

Here are the changes you need to make:

#### **JDBC Configuration (Database Connection)**

- **Update the JDBC URL**: Change the IP address to the internal IP address of your database.
- Example:
  ```properties
  jdbc.url=jdbc:mysql://<DB_INTERNAL_IP>:3306/accounts?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull
  ```

#### **Memcached Configuration (Active and Standby Hosts)**

- **Update the Memcached server's IP**: Set the internal IP for the Memcached active and standby servers.
- Example:
  ```properties
  memcached.active.host=<MEMCACHED_INTERNAL_IP>
  memcached.standBy.host=<MEMCACHED_INTERNAL_IP>
  ```

#### **RabbitMQ Configuration**

- **Update the RabbitMQ server's IP**: Set the internal IP for the RabbitMQ server.
- Example:
  ```properties
  rabbitmq.address=<RABBITMQ_INTERNAL_IP>
  ```

---

### 2. **Update the NGINX Configuration**

To ensure that NGINX is correctly routing traffic to your Tomcat server, you'll need to update the IP address of the Tomcat server in the NGINX configuration file.

**Path:** `nginvproapp.conf`

Replace the IP address of the Tomcat server with its internal IP.

#### **Example Configuration:**

```nginx
upstream vproapp {
  server <TOMCAT_INTERNAL_IP>:8080;
}

server {
  listen 80;
  
  location / {
    proxy_pass http://<TOMCAT_INTERNAL_IP>:8080;
  }
}
```

---

## Docker Stack Overview

This setup leverages Docker to containerize the following services:

1. **Web Server (NGINX)** – Acts as a reverse proxy, routing traffic to the Tomcat server.
2. **App Server (Tomcat)** – Hosts the web application and connects to the MySQL database, Memcached, and RabbitMQ.
3. **Memcached** – Used for caching and session management.
4. **MySQL Database** – Stores the application data.
5. **RabbitMQ** – Handles message queuing for communication between application components.

---

## Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/Application-Vprofile.git
   cd Application-Vprofile
   ```

2. **Build and start the Docker containers:**
   ```bash
   
   ```

3. **Access the application:**
   Once the containers are up and running, you can access the application via the configured NGINX server on port 80

---

## Contributing

We welcome contributions! Please feel free to fork this repository, open an issue, or submit a pull request.

---

### **License**

This project is licensed under the MIT License.

---

This version is designed to make it easier for users to understand the necessary steps, and it uses clear headings, descriptions, and examples to guide them through the process. You can copy this markdown and paste it directly into your GitHub README file.
