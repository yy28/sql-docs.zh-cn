## <a name="prerequisites"></a>必备条件

创建可用性组前，需要：

- 设置环境，以便所有托管可用性副本的服务器能够通信。
- 安装 SQL Server。 有关详细信息，请参阅[安装 SQL Server](../database-engine/install-windows/install-sql-server.md)。

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>启用 AlwaysOn 可用性组，并重启 mssql-server

>[!NOTE]
>下面使用的命令利用 PowerShell 库上发布的 sqlserver 模块中的 cmdlet。 可以使用 Install-Module 命令安装此模块。

在托管 SQL Server 实例的每个副本上启用 AlwaysOn 可用性组。 然后重启 SQL Server 服务。 运行以下命令，启用并重启 SQL Server 服务：

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwaysonhealth-event-session"></a>启用 AlwaysOn_health 事件会话

可选择性地启用 AlwaysOn 可用性组扩展事件 (XE) 会话，在对可用性组进行故障排除时帮助诊断根本原因。 在每个 SQL Server 实例上运行以下命令：

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

有关此 XE 会话的详细信息，请参阅 [Always On 可用性组扩展事件](../database-engine/availability-groups/windows/always-on-extended-events.md)。

## <a name="database-mirroring-endpoint-authentication"></a>数据库镜像端点身份验证

读取缩放可用性组中涉及的副本将需要通过端点进行身份验证，使同步正常运行。 下面介绍两种可用于此类身份验证的主要方案。

### <a name="service-account"></a>服务帐户

在所有次要副本加入同一个域的 Active Directory 环境中，SQL Server可以使用该服务帐户进行身份验证。 将需要显式创建服务帐户在所有 SQL Server 实例上的登录名：

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>SQL 登录身份验证

在次要副本可能未连接到 Active Directory 域的环境中，将需要使用 SQL 身份验证。 以下 Transact-SQL 脚本创建名为 `dbm_login` 的登录名和名为 `dbm_user` 的用户。 使用强密码更新脚本。 要创建数据库镜像端点用户，在所有 SQL Server 实例上运行以下命令：

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>证书身份验证

如果利用要求使用 SQL 身份验证进行身份验证的次要副本，请使用证书在镜像端点之间进行身份验证。

以下 Transact-SQL 脚本创建主密钥和证书。 然后备份证书，并使用私钥保护文件。 使用强密码更新脚本。 在主 SQL Server 实例上运行以下脚本，创建证书：

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

现在主 SQL Server 副本的证书位于 `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer`，私钥位于 `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk`。 将这两个文件复制到所有要托管可用性副本的服务器上的同一位置。

确保在每个次要副本上，SQL Server 的服务帐户有权访问该证书。

#### <a name="create-the-certificate-on-secondary-servers"></a>在辅助服务器上创建证书

以下 Transact-SQL 脚本根据在主 SQL Server 副本上创建的备份创建主密钥和证书。 该命令还会为用户授予访问证书的权限。 使用强密码更新脚本。 解密密码与在此前的步骤中创建 `.pvk` 文件使用的密码相同。 要创建证书，在所有次要副本上运行以下脚本：

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>在所有副本上创建数据库镜像终结点

数据库镜像端点使用传输控制协议 (TCP) 在参与数据库镜像会话或承载可用性副本的服务器实例之间发送和接收消息。 数据库镜像端点在唯一的 TCP 端口号上进行侦听。

以下 Transact-SQL 脚本为可用性组创建名为 `Hadr_endpoint` 的侦听终结点。 该脚本启动终结点，并将连接权限授予在上一步中创建的服务帐户或 SQL 登录名。 在运行该脚本之前，替换 `**< ... >**` 之内的值。 （可选）可以包含 IP 地址 `LISTENER_IP = (0.0.0.0)`。 侦听器 IP 地址必须是 IPv4 地址。 还可以使用 `0.0.0.0`。

为所有 SQL Server 实例上的环境更新以下 Transact-SQL 脚本：

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

防火墙上的 TCP 端口必须对侦听器端口打开。

有关详细信息，请参阅 [数据库镜像端点 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)。
