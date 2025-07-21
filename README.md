# 🚀 Laravel 12 Docker Startup

This is a **Docker-based template** for **Laravel 12**, built with:
- **PHP 8.4** (FPM on Alpine)
- **PostgreSQL 16**
- **Redis (Alpine)**
- **Node.js 22 + NPM**
- **Supervisor for Queue & Scheduler**
- **Makefile for easy commands (like Laravel Sail)**
- **Nginx**
- **Composer**
- **XDebug in Dev Mode**

And useful **libraries**:
- **[Telescope](https://laravel.com/docs/12.x/telescope)**
- **[Horizon](https://laravel.com/docs/11.x/horizon)**
- **[Log Viewer](https://log-viewer.opcodes.io/docs/3.x/install)**
- **[Scramble DeDoc](https://scramble.dedoc.co/installation)**

---

## **🛠 Setup Instructions**
### 1️⃣ Clone the Repository
```sh
git clone git@github.com:paldeflex/laravel-12-docker-startup.git
cd laravel-12-docker
```
### 2️⃣ Copy `.env` and Update Configuration
```sh
cp .env.example .env
```
- Open `.env` file and change it:
```yaml
DB_DATABASE=<your-db> # Change DB name
```
- Change the container name prefix:

  Inside `compose.yml`, rename `l12-` to your project name:
```yaml
services:
    app:
        container_name: myproject-app
    nginx:
        container_name: myproject-nginx
    postgres:
        container_name: myproject-postgres
    redis:
        container_name: myproject-redis
```
- Change the Docker network

  In `compose.yml`:
```yaml
networks:
   myproject-network:
```

---

## 🚀 Start Containers
### 🔹 Using Docker
```sh
docker compose up -d
```
### 🔹 Using Makefile
```sh
make up    # For development
make prod  # For production
```

--- 

## 📦 Install Dependencies
### 🛠 Install PHP Dependencies

Run inside the container:
```sh
docker compose exec -u www-data app composer install
```

Or using Makefile:
```sh
make composer install
```

### 🎸 Install Node.js & NPM Dependencies
```sh
make npm install
make npm run dev   # Run Vite for development
```

### 🔑 Generate App Key
```sh
make artisan key:generate
```

### 📜 Run Migrations
```sh
make artisan migrate
```

### 🔗 Create Storage Symlink
```sh
make artisan storage:link
```

---

## 💻 Available Commands
### 🛠 Running Laravel Commands

| Action              | Docker Command                                                             | Makefile Shortcut     |
|---------------------|----------------------------------------------------------------------------|-----------------------|
| Run `php artisan`   | `docker compose exec -u www-data app php artisan <cmd>`                    | `make artisan <cmd>`  |
| Run `composer`      | `docker compose exec -u www-data app composer <cmd>`                       | `make composer <cmd>` |
| Run `npm`           | `docker compose exec -u www-data app npm <cmd>`                            | `make npm <cmd>`      |
| Open Bash           | `docker compose exec -u www-data app bash`                                 | `make bash`           | 
| View Logs           | `docker compose logs -f app`                                               | `make logs app`       | 
| Open PostgreSQL CLI | `docker compose exec -e PGPASSWORD=<pass> postgres psql -U <user> -d <db>` | `make psql`           | 
| Open Redis CLI      | `docker compose exec redis redis-cli`                                      | `make redis`          | 
| Run Tests           | `docker compose exec -u www-data app php artisan test`                     | `make test`           | 

---

## 🛑 Managing Containers
### 🔄 Restart & Stop
| Action      | Docker Command                     | Makefile Shortcut                         |
|-------------|------------------------------------|-------------------------------------------|
| Restart all | `docker compose restart`           | `make restart`                            |
| Restart one | `docker compose restart <service>` | `make restart-container CONTAINER=<name>` | 
| Stop all    | `docker compose stop`              | `make stop`                               |
| Stop one    | `docker compose stop <service>`    | `make stop-container CONTAINER=<name>`    |
| Start all   | `docker compose up -d`             | `make up`                                 |
| Remove all  | `docker compose down -v`           | `make down`                               |


For list of **all makefile commands**, run `make help`. 

---

## **💡 PHPStorm Setup**

### PHP Interpreter

![image](https://github.com/user-attachments/assets/c19edc0a-e5ce-4905-8324-be4c7adbdbc1)
![image](https://github.com/user-attachments/assets/53cdc2a1-c878-4818-b0c2-ed04afb18c61) or ![image](https://github.com/user-attachments/assets/2c59cadb-b74e-4e53-9fc7-e759016dd9d7)
![image](https://github.com/user-attachments/assets/804cbdc4-058c-4e04-ad8c-a8304b090a8e)
![image](https://github.com/user-attachments/assets/bfd327e3-06f3-4f3c-9475-45bb58392cf1)

### If you use Laravel IDEA

![image](https://github.com/user-attachments/assets/50c0f082-58d4-496d-8439-5b549e04e056)

### XDebug

![image](https://github.com/user-attachments/assets/d14ff2fb-359c-4a5e-8739-be4a63ecfe9b)
![image](https://github.com/user-attachments/assets/718cde26-37ac-42e4-91b7-319b6402a6e3)
![image](https://github.com/user-attachments/assets/2469193b-cd63-4f43-99fb-04616c3dbd8d)

---

## **🧪 Run Tests**
```shell
make test
```
or, 
```shell
docker compose exec -u www-data app php artisan test
```

---

## 📜 Additional Notes
- This setup **supports Laravel Queues & Scheduler** via **Supervisor**. 
- **PostgreSQL, Redis & Supervisor** are configured out of the box.
- Uses **Node.js 22** for Vite & frontend dependencies.
- All **Docker volumes** persist data between container restarts.

---

## 🔥 Now your Laravel 12 project is fully containerized! 
Use **Makefile** commands just like **Laravel Sail**, and enjoy seamless **Docker development**! 🚀

---


## 🤖 Authors
- [**m1n64**](https://github.com/m1n64)

