在Ubuntu上安装PostgreSQL并配置其允许其他电脑远程访问数据库服务，可以按照以下步骤进行操作：

### 安装PostgreSQL
1. **更新包列表**：确保系统包列表是最新的，运行以下命令：
   ```bash
   sudo apt update
   ```
2. **安装PostgreSQL**：安装PostgreSQL及其辅助工具包：
   ```bash
   sudo apt install postgresql postgresql-contrib
   ```
3. **启动并启用PostgreSQL服务**：确保PostgreSQL服务在系统启动时自动运行，并立即启动服务：
   ```bash
   sudo systemctl start postgresql
   sudo systemctl enable postgresql
   ```
4. **验证安装**：检查PostgreSQL服务是否正常运行：
   ```bash
   sudo systemctl status postgresql
   ```
   如果服务正常运行，你会看到“active (running)”状态。

### 配置PostgreSQL以允许远程访问
1. **修改`postgresql.conf`文件**：
   - 打开配置文件（假设PostgreSQL版本为17，根据实际情况调整版本号）：
     ```bash
     sudo nano /etc/postgresql/17/main/postgresql.conf
     ```
   - 找到以下行：
     ```plaintext
     #listen_addresses = 'localhost'
     ```
   - 去掉注释符号`#`，并将`localhost`改为`*`，允许从任何IP地址连接：
     ```plaintext
     listen_addresses = '*'
     ```
2. **修改`pg_hba.conf`文件**：
   - 打开文件：
     ```bash
     sudo nano /etc/postgresql/17/main/pg_hba.conf
     ```
   - 添加以下行，允许来自任何IP地址的连接使用MD5密码认证：
     ```plaintext
     host    all             all             0.0.0.0/0               md5
     ```
3. **重启PostgreSQL服务**：使配置生效：
   ```bash
   sudo systemctl restart postgresql
   ```
4. **配置防火墙**：确保防火墙允许通过PostgreSQL的默认端口（5432）进行连接：
   ```bash
   sudo ufw allow 5432/tcp
   ```
   如果你使用的是其他防火墙工具，请确保允许该端口。

### 设置PostgreSQL用户密码
1. **切换到`postgres`用户**：
   ```bash
   sudo -u postgres psql
   ```
2. **为`postgres`用户设置密码**：
   ```sql
   ALTER USER postgres PASSWORD 'your_password';
   ```
   将`your_password`替换为你想要设置的密码。

### 测试远程连接
在其他电脑上，使用PostgreSQL客户端工具（如`psql`、DBeaver或pgAdmin）尝试连接到你的Ubuntu服务器上的PostgreSQL数据库。连接时需要提供以下信息：
- **主机**：你的Ubuntu服务器的IP地址
- **端口**：5432（或你配置的其他端口）
- **用户名**：PostgreSQL用户名（如`postgres`）
- **密码**：你为用户设置的密码
- **数据库**：要连接的数据库名称。

### 安全注意事项
- **使用强密码**：确保所有PostgreSQL用户账户使用强密码。
- **限制IP地址**：在`pg_hba.conf`文件中，限制特定IP地址或范围的访问，而不是允许所有IP地址。
- **启用SSL**：配置PostgreSQL使用SSL进行加密连接。
- **定期更新**：保持PostgreSQL安装及相关包的更新，以确保拥有最新的安全补丁。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjY4MzQwMzRdfQ==
-->