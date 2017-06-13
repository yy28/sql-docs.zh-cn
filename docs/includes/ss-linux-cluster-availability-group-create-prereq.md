## <a name="prerequisites"></a>先决条件

创建可用性组前，需要：

- 设置环境，以便所有托管可用性副本的服务器能够通信
- 安装 SQL Server

>[!NOTE]
>在Linux上，必须先创建可用性组，然后再将其添加为群集管理的群集资源。 本文档举例说明了如何创建可用性组。 有关分发特别说明，创建群集并将可用性组添加为群集资源，请参阅下面的链接[下一步行动](#next-steps)。

1. **更新每个主机的计算机名称**

   每个 SQL Server 名称必须：
   
   - 不超过 15 个字符
   - 在网络中唯一
   
   若要设置计算机名称，请编辑`/etc/hostname`。 以下脚本，可以编辑`/etc/hostname`与`vi`。

   ```bash
   sudo vi /etc/hostname
   ```

1. **配置的主机文件**

>[!NOTE]
>如果在 DNS 服务器中使用主机 IP 注册主机名，则无需执行以下步骤。 验证将属于可用性组配置的所有节点是否可以彼此通信（Ping 主机名应使用对应的 IP 地址答复）。 此外，请确保 /etc/hosts 文件不包含节点主机名映射到本地主机 IP 地址 127.0.0.1 的记录。


   每个服务器上的主机文件包含将加入可用性组的所有服务器的 IP 地址和名称。 

   以下命令将返回当前服务器的 IP 地址：

   ```bash
   sudo ip addr show
   ```

   更新`/etc/hosts`。 以下脚本，可以编辑`/etc/hosts`与`vi`。

   ```bash
   sudo vi /etc/hosts
   ```

   下面的示例演示`/etc/hosts`上**node1**添加为**node1**和**node2**。 本文档中**node1**指主 SQL Server 副本。 **node2**指辅助 SQL Server。;


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 node1
   10.128.16.77 node2
   ```

### <a name="install-sql-server"></a>安装 SQL Server

安装 SQL Server。 以下链接指向适用于各种分发的 SQL Server 安装说明。 

- [Red Hat Enterprise Linux](..\linux\sql-server-linux-setup-red-hat.md)

- [SUSE Linux Enterprise Server](..\linux\sql-server-linux-setup-suse-linux-enterprise-server.md)

- [Ubuntu](..\linux\sql-server-linux-setup-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>启用 AlwaysOn 可用性组，然后重新启动 sqlserver

启用 Alwayson 可用性组承载 SQL Server 服务，每个节点上的，然后重新启动`mssql-server`。  运行以下脚本：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##    <a name="enable-alwaysonhealth-event-session"></a>启用 AlwaysOn_health 事件会话 

可选择性地启用特定于 AlwaysOn 可用性组的扩展事件，在故障排查可用性组时帮助诊断根本原因。

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

有关此 XE 会话的详细信息，请参阅[始终在扩展事件](http://msdn.microsoft.com/library/dn135324.aspx)。

## <a name="create-db-mirroring-endpoint-user"></a>创建数据库镜像终结点用户

以下 TRANSACT-SQL 脚本创建一个登录名`dbm_login`，和一个名为用户`dbm_user`。 使用强密码更新脚本。 在所有 SQL Server 上运行以下命令，创建数据库镜像终结点用户。

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>创建证书

Linux 上的 SQL Server 服务使用证书验证镜像终结点之间的通信。 

以下 Transact-SQL 脚本将创建主密钥和证书。 然后备份证书，并使用私钥保护文件。 使用强密码更新脚本。 连接到主 SQL Server，并运行以下 Transact-SQL 创建证书：

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

此时你主 SQL Server 副本具有在证书`/var/opt/mssql/data/dbm_certificate.cer`和私有密钥 at `var/opt/mssql/data/dbm_certificate.pvk`。 将这两个文件复制到所有要托管可用性副本的服务器上的同一位置。 使用 mssql 用户或为 mssql 用户授予权限，访问这些文件。 

例如在源服务器上，以下命令将文件复制到目标计算机。 替换 **<node2>** 值替换为将承载副本的 SQL Server 实例的名称。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

在目标服务器上，为 mssql 用户授予访问证书的权限。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>在辅助服务器上创建证书

以下 Transact-SQL 脚本根据在主 SQL Server 副本上创建的备份创建主密钥和证书。 该命令还会为用户授予访问证书的权限。 使用强密码更新脚本。 解密密码与上一步中创建 .pvk 文件使用的密码相同。 在所有辅助服务器上运行以下脚本创建证书。

```Transact-SQL
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

以下 TRANSACT-SQL 创建名为的侦听终结点`Hadr_endpoint`为可用性组。 它启动终结点，并向创建的用户授予连接权限。 在运行该脚本之前，将之间的值`**< ... >**`。


>[!NOTE]
>对于此版本，请不要为侦听器 IP 使用不同的 IP 地址。 我们正在修复此问题，当前唯一可接受的值是“0.0.0.0”。

更新所有 SQL Server 实例上有关您环境以下 TRANSACT-SQL: 

```Transact-SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!IMPORTANT]
>防火墙上的 TCP 端口需对侦听器端口打开。

有关完整信息，请参阅[数据库镜像终结点 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)。
