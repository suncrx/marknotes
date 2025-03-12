在 Ubuntu 上安装 MySQL 并设置远程访问的步骤如下：

### 安装 MySQL
1. **更新软件包列表**：
   ```bash
   sudo apt update
   ```
2. **安装 MySQL 服务器**：
   ```bash
   sudo apt install mysql-server
   ```
   安装过程中会提示你设置 MySQL root 用户的密码，请选择一个强密码并记住它。
3. **启动 MySQL 服务**：
   ```bash
   sudo systemctl start mysql
   ```
4. **检查 MySQL 服务状态**：
   ```bash
   sudo systemctl status mysql
   ```
   如果服务正在运行，你会看到 “active (running)” 的状态。
5. **运行安全脚本**：
   ```bash
   sudo mysql_secure_installation
   ```
   按照提示进行操作，包括设置 root 密码、删除匿名用户、禁止 root 远程登录等。

### 设置远程访问
1. **登录 MySQL**：
   ```bash
   sudo mysql -u root -p
   ```
   输入你在安装过程中设置的 root 密码。
2. **创建远程访问用户**：
   ```sql
   CREATE USER 'remote_user'@'%' IDENTIFIED BY 'password';
   ```
   将 `remote_user` 和 `password` 替换为你想要的用户名和密码。
3. **授予远程用户权限**：
   ```sql
   GRANT ALL PRIVILEGES ON *.* TO 'remote_user'@'%';
   FLUSH PRIVILEGES;
   ```
   这将授予远程用户对所有数据库的所有权限。你可以根据需要限制对特定数据库的访问。
4. **修改 MySQL 配置文件**：
   编辑 `/etc/mysql/mysql.conf.d/mysqld.cnf` 文件，将 `bind-address` 设置为 `0.0.0.0`，允许从任何 IP 地址连接：
   ```bash
   sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
   ```
   将以下行：
   ```plaintext
   bind-address = 127.0.0.1
   ```
   修改为：
   ```plaintext
   bind-address = 0.0.0.0
   ```
   保存并退出编辑器。
5. **重启 MySQL 服务**：
   ```bash
   sudo systemctl restart mysql
   ```
   使配置更改生效。
6. **配置防火墙**：
   如果你使用的是 UFW 防火墙，需要允许 MySQL 的默认端口（3306）的流量：
   ```bash
   sudo ufw allow 3306/tcp
   ```
   如果你使用的是其他防火墙，请相应地调整设置。

### 测试远程连接
从远程机器上，使用以下命令尝试连接到 MySQL 服务器：
```bash
mysql -u remote_user -h <your_server_ip> -p
```
将 `<your_server_ip>` 替换为你的 MySQL 服务器的 IP 地址，`remote_user` 替换为你创建的远程用户名。

按照以上步骤操作后，你应该能够从远程位置成功连接到你的 MySQL 数据库。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwMTY3NzEyN119
-->