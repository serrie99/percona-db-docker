
# 🐬 Percona MySQL Docker Setup

This project provides a lightweight and persistent **Percona Server for MySQL 8.0** containerized environment using Docker Compose. It's ideal for development and staging environments.

---

## 📦 Features

- ✅ Based on [Percona Server for MySQL 8.0](https://www.percona.com/software/mysql-database/percona-server)
- 🗃️ Auto-initializes with environment variables
- 🔐 Custom root/user password setup
- 🌐 Accessible from any IP address (`0.0.0.0`)
- 💾 Persistent data via Docker Volume

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://your-repo-url
cd your-project-directory
```

### 2. Copy and configure environment variables

```bash
cp .env.example .env
```

Edit `.env` and set your desired MySQL config:

```env
PORT=3306
MYSQL_ROOT_PASSWORD=your_root_password
MYSQL_DATABASE=your_database_name
MYSQL_USER=your_user_name
MYSQL_PASSWORD=your_user_password
```

### 3. Start the container

```bash
docker-compose --env-file .env up -d
```

> 📦 The database will be available at `localhost:3306`  
> 🔑 You can connect with MySQL tools using the credentials you defined.

---

## 🔐 MySQL Access Example

```bash
mysql -h 127.0.0.1 -P 3306 -u your_user_name -p
```

---

## 🧠 Optional: Grant Full Privileges for Remote User

If you want the user to be able to create/drop databases or access from any IP:

```sql
GRANT ALL PRIVILEGES ON *.* TO 'your_user_name'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

---

## 🗑️ Stop and Remove

```bash
docker-compose down
```

To remove volumes (⚠️ delete all data):

```bash
docker-compose down -v
```

---

## 📁 Volume Info

MySQL data is persisted in a named volume:

```
percona_data:/var/lib/mysql
```

---

## 🧩 Troubleshooting

- **Connection refused**  
  → Make sure port `3306` is not already in use.

- **Access denied**  
  → Ensure you granted proper privileges (`GRANT ALL PRIVILEGES`...)

- **Firewall block**  
  → Allow port in `ufw`: `sudo ufw allow 3306`

---

## 📘 License

This configuration is provided as-is for development and educational purposes.  
Percona Server is licensed under the GNU GPL v2.
