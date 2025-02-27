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
composer create-project m1n64/laravel-12-docker-startup laravel-12-docker
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

  Inside `docker-compose.yml`, rename `l12-` to your project name:
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

  In `docker-compose.yml`:
```yaml
networks:
   myproject-network:
```

---

## 🚀 Start Containers
### 🔹 Using Docker
```sh
docker-compose up -d
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
docker-compose exec -u www-data app composer install
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
| Run `php artisan`   | `docker-compose exec -u www-data app php artisan <cmd>`                    | `make artisan <cmd>`  |
| Run `composer`      | `docker-compose exec -u www-data app composer <cmd>`                       | `make composer <cmd>` |
| Run `npm`           | `docker-compose exec -u www-data app npm <cmd>`                            | `make npm <cmd>`      |
| Open Bash           | `docker-compose exec -u www-data app bash`                                 | `make bash`           | 
| View Logs           | `docker-compose logs -f app`                                               | `make logs app`       | 
| Open PostgreSQL CLI | `docker-compose exec -e PGPASSWORD=<pass> postgres psql -U <user> -d <db>` | `make psql`           | 
| Open Redis CLI      | `docker-compose exec redis redis-cli`                                      | `make redis`          | 

---

## 🛑 Managing Containers
### 🔄 Restart & Stop
| Action      | Docker Command                     | Makefile Shortcut                         |
|-------------|------------------------------------|-------------------------------------------|
| Restart all | `docker-compose restart`           | `make restart`                            |
| Restart one | `docker-compose restart <service>` | `make restart-container CONTAINER=<name>` | 
| Stop all    | `docker-compose stop`              | `make stop`                               |
| Stop one    | `docker-compose stop <service>`    | `make stop-container CONTAINER=<name>`    |
| Start all   | `docker-compose up -d`             | `make up`                                 |
| Remove all  | `docker-compose down -v`           | `make down`                               |


For list of **all makefile commands**, run `make help`. 

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

