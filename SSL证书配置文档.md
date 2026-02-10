# Amigos Supply 网站 SSL 证书配置文档

## 服务器信息

| 项目 | 信息 |
|------|------|
| 服务器 IP | 121.36.173.141 |
| 操作系统 | Ubuntu 18.04.3 LTS |
| Web 服务器 | Apache 2.4.7 |
| 网站目录 | /var/www/html/ |
| 域名 | amigos-supply.cn / www.amigos-supply.cn |

## SSL 证书信息

| 项目 | 信息 |
|------|------|
| 证书颁发机构 | Let's Encrypt (E7) |
| 申请工具 | acme.sh |
| 覆盖域名 | amigos-supply.cn, www.amigos-supply.cn |
| 首次签发日期 | 2026-02-10 |
| 到期日期 | 2026-05-11 |
| 证书类型 | ECC (椭圆曲线) |
| 自动续期 | 已配置（acme.sh 自动任务） |

## 证书文件路径

```
# acme.sh 原始证书（自动续期更新此处）
/root/.acme.sh/amigos-supply.cn_ecc/amigos-supply.cn.cer   # 证书
/root/.acme.sh/amigos-supply.cn_ecc/amigos-supply.cn.key   # 私钥
/root/.acme.sh/amigos-supply.cn_ecc/fullchain.cer           # 完整证书链
/root/.acme.sh/amigos-supply.cn_ecc/ca.cer                  # CA 中间证书

# Apache 使用的证书（由 acme.sh --install-cert 复制）
/etc/apache2/ssl/cert.pem        # 证书
/etc/apache2/ssl/key.pem         # 私钥
/etc/apache2/ssl/fullchain.pem   # 完整证书链
```

## Apache 配置文件

### HTTP 虚拟主机（自动跳转 HTTPS）

文件路径：`/etc/apache2/sites-available/000-default.conf`

```apache
<VirtualHost *:80>
    ServerName amigos-supply.cn
    ServerAlias www.amigos-supply.cn
    DocumentRoot /var/www/html

    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</VirtualHost>
```

### HTTPS 虚拟主机

文件路径：`/etc/apache2/sites-available/default-ssl.conf`

```apache
<VirtualHost *:443>
    ServerName amigos-supply.cn
    ServerAlias www.amigos-supply.cn
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/cert.pem
    SSLCertificateKeyFile /etc/apache2/ssl/key.pem
    SSLCertificateChainFile /etc/apache2/ssl/fullchain.pem

    <Directory /var/www/html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

## 常用运维命令

### 证书管理

```bash
# 查看证书信息
/root/.acme.sh/acme.sh --list

# 手动续期证书
/root/.acme.sh/acme.sh --renew -d amigos-supply.cn --force

# 续期后重新安装到 Apache 目录
/root/.acme.sh/acme.sh --install-cert -d amigos-supply.cn \
  --cert-file /etc/apache2/ssl/cert.pem \
  --key-file /etc/apache2/ssl/key.pem \
  --fullchain-file /etc/apache2/ssl/fullchain.pem

# 查看证书到期时间
openssl x509 -in /etc/apache2/ssl/cert.pem -noout -dates
```

### Apache 管理

```bash
# 测试配置是否正确
apache2ctl configtest

# 重启 Apache
service apache2 restart

# 重新加载配置（不中断连接）
service apache2 reload

# 查看已启用的模块
apache2ctl -M

# 查看虚拟主机配置
apache2ctl -S

# 查看错误日志
tail -f /var/log/apache2/error.log
```

### 连接测试

```bash
# 测试 HTTPS 是否正常
curl -I https://amigos-supply.cn
curl -I https://www.amigos-supply.cn

# 测试 HTTP 是否自动跳转
curl -I http://amigos-supply.cn

# 查看证书详情
openssl s_client -connect amigos-supply.cn:443 -servername amigos-supply.cn
```

## 故障排查

### 证书过期

acme.sh 会自动续期，如果续期失败：

1. 检查 acme.sh 日志：`/root/.acme.sh/acme.sh --renew -d amigos-supply.cn --debug`
2. 确认 80 端口可正常访问（Let's Encrypt 验证需要）
3. 手动强制续期：`/root/.acme.sh/acme.sh --renew -d amigos-supply.cn --force`
4. 续期后重启 Apache：`service apache2 restart`

### HTTPS 无法访问

1. 检查 Apache 是否运行：`service apache2 status`
2. 检查 443 端口是否监听：`netstat -tlnp | grep 443`
3. 检查防火墙是否放行 443 端口：`iptables -L -n | grep 443`
4. 检查配置语法：`apache2ctl configtest`
5. 查看错误日志：`tail -50 /var/log/apache2/error.log`

### Apache 启动失败

1. 检查配置语法：`apache2ctl configtest`
2. 确认证书文件存在：`ls -la /etc/apache2/ssl/`
3. 确认 SSL 模块已启用：`a2enmod ssl`
4. 确认站点已启用：`a2ensite default-ssl.conf`
