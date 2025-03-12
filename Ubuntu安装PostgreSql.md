在 Ubuntu 上安装并使用 PostgreSQL 的步骤如下：

### 1. 安装 PostgreSQL
#### 添加 PostgreSQL 官方仓库并更新
```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt update
```

#### 安装 PostgreSQL
```bash
sudo apt install postgresql-15
```

#### 验证服务状态
```bash
sudo systemctl status postgresql
```
如果显示 `active (running)`，则表示服务已成功启动。

### 2. 配置 PostgreSQL
#### 修改配置文件
- **主配置文件**：`postgresql.conf`（路径示例：`/etc/postgresql/15/main/postgresql.conf`）
- **客户端认证文件**：`pg_hba.conf`

#### 关键配置项
- **允许远程访问**：修改 `postgresql.conf` 文件，将 `listen_addresses` 设置为 `'*'`，允许所有 IP 连接，并确认端口号为 `5432`。
  ```bash
  listen_addresses = '*'
  port = 5432
  ```
- **设置最大连接数**：根据硬件配置调整 `max_connections` 参数。
  ```bash
  max_connections = 100
  ```
- **修改认证方式**：修改 `pg_hba.conf` 文件，允许所有 IP 通过密码访问。
  ```bash
  host    all             all             0.0.0.0/0               scram-sha-256
  ```

#### 重启服务生效
```bash
sudo systemctl restart postgresql
```

### 3. 创建新用户与数据库
#### 登录默认账户
```bash
sudo -u postgres psql
```

#### 创建新用户
```sql
CREATE USER myuser WITH PASSWORD 'user123';
```

#### 创建数据库并授权
```sql
CREATE DATABASE mydb OWNER myuser;
GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;
```

### 4. 使用 PostgreSQL
#### 连接到 PostgreSQL 数据库
```bash
psql -U myuser -d mydb
```

#### 执行 SQL 语句
- 创建表：
  ```sql
  CREATE TABLE mytable (
      id SERIAL PRIMARY KEY,
      name VARCHAR(100) NOT NULL,
      age INT
  );
  ```
- 插入数据：
  ```sql
  INSERT INTO mytable (name, age) VALUES ('Alice', 30);
  ```
- 查询数据：
  ```sql
  SELECT * FROM mytable;
  ```

### 5. 常见问题与解决方案
#### 连接被拒绝
- 检查 `pg_hba.conf` 中是否允许用户连接。
- 确认密码是否正确：
  ```sql
  ALTER USER myuser WITH PASSWORD 'new_password';
  ```

#### 端口冲突
- 检查 PostgreSQL 服务是否运行：
  ```bash
  sudo systemctl status postgresql
  ```
- 查看端口占用：
  ```bash
  netstat -tuln | grep 5432
  ```

#### 忘记 `postgres` 用户密码
- 停止 PostgreSQL 服务：
  ```bash
  sudo systemctl stop postgresql
  ```
- 以单用户模式启动：
  ```bash
  sudo -u postgres postgres --single -D /var/lib/postgresql/15/main
  ```
- 执行密码修改：
  ```sql
  ALTER USER postgres WITH PASSWORD 'new_password';
  ```

通过以上步骤，你可以在 Ubuntu 上安装并使用 PostgreSQL，完成数据库的基本操作。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcyNzQzNjYyN119
-->