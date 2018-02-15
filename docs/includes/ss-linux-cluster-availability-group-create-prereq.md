## <a name="prerequisites"></a>必要條件

创建可用性组前，需要：

- 设置你的环境，以便将承载可用性副本的所有服务器可以进行都通信。
- 安装 SQL Server。

>[!NOTE]
>在 Linux 上，必须创建可用性组，然后将其添加为群集资源将由群集管理。 本文档举例说明了如何创建可用性组。 若要创建群集并为群集资源添加到可用性组的特定于分发的说明，请参阅"后续步骤。"下面的链接

1. 更新每个主机的计算机名称。

   每个 SQL Server 名称必须：
   
   - 15 个字符或更少。
   - 在网络中唯一。
   
   若要设置计算机名，请编辑 `/etc/hostname`。 以下脚本，可以编辑`/etc/hostname`与`vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. 配置的主机文件。

    >[!NOTE]
    >如果向其 IP DNS 服务器中注册的主机名，你不需要执行以下步骤。 验证所有节点用于可用性组配置中可以相互通信。 （为主机名 ping 应答复具有对应的 IP 地址。）此外，请确保 /etc/hosts 文件不包含 localhost IP 地址 127.0.0.1 节点的主机名映射的记录。
    >

   每个服务器上的主机文件包含将加入可用性组的所有服务器的 IP 地址和名称。 

   以下命令将返回当前服务器的 IP 地址：

   ```bash
   sudo ip addr show
   ```

   更新 `/etc/hosts`。 以下脚本，可以编辑`/etc/hosts`与`vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   下面的示例演示了 node1 上的 `/etc/hosts`，并补充了 node1、node2 和 node3。 在此文档中， **node1**指承载主副本的服务器。 和**node2**和**node3**到承载辅助副本的服务器，请参阅。

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>安装 SQL Server

安装 SQL Server。 以下链接指向有关各种分发的 SQL Server 安装说明： 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>启用 AlwaysOn 可用性组并重新启动 mssql 服务器

启用 AlwaysOn 可用性组承载 SQL Server 实例的每个节点上。 然后重新启动`mssql-server`。 运行以下脚本：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwaysonhealth-event-session"></a>启用 AlwaysOn_health 事件会话 

（可选） 可以启用 AlwaysOn 可用性组的扩展的事件来解决问题的可用性组时，帮助进行根本原因诊断。 在每个 SQL Server 实例上运行以下命令： 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

有关此 XE 会话的详细信息，请参阅[扩展事件的 AlwaysOn](http://msdn.microsoft.com/library/dn135324.aspx)。

## <a name="create-a-database-mirroring-endpoint-user"></a>创建数据库镜像终结点的用户

以下 TRANSACT-SQL 脚本创建一个登录名`dbm_login`和名为的用户`dbm_user`。 使用强密码更新脚本。 若要创建数据库镜像终结点的用户，请在所有 SQL Server 实例上运行以下命令：

```SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>创建证书

Linux 上的 SQL Server 服务使用证书验证镜像终结点之间的通信。 

下面的 TRANSACT-SQL 脚本创建一个主密钥和证书。 然后，再备份该证书，并使用私钥保护该文件。 使用强密码更新脚本。 连接到主 SQL Server 实例。 若要创建证书，请运行以下 TRANSACT-SQL 脚本：

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

此时，你的主 SQL Server 副本具有在证书`/var/opt/mssql/data/dbm_certificate.cer`和私有密钥 at `var/opt/mssql/data/dbm_certificate.pvk`。 将这两个文件复制到所有要托管可用性副本的服务器上的同一位置。 使用 mssql 用户，或授予访问 mssql 用户访问这些文件的权限。 

例如，在源服务器上，以下命令将文件复制到目标计算机。 替换`**<node2>**`值替换为将承载副本的 SQL Server 实例的名称。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

在每个目标服务器上，可向 mssql 用户能够访问的证书提供权限。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>在辅助服务器上创建证书

下面的 TRANSACT-SQL 脚本从主 SQL Server 副本创建的备份创建主密钥和证书。 该命令还会为用户授予访问证书的权限。 使用强密码更新脚本。 解密密码与在此前的步骤中创建 .pvk 文件使用的密码相同。 若要创建的证书，所有辅助服务器上运行以下脚本：

```SQL
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

数据库镜像端点使用传输控制协议 (TCP) 发送和接收参与数据库镜像会话或承载可用性副本的服务器实例之间的消息。 数据库镜像端点在唯一的 TCP 端口号上进行侦听。 

下面的 TRANSACT-SQL 脚本创建一个名为的侦听终结点`Hadr_endpoint`为可用性组。 它启动终结点，并为你创建的用户授予连接权限。 在运行该脚本之前，替换 `**< ... >**` 之内的值。 （可选） 可以包含 IP 地址`LISTENER_IP = (0.0.0.0)`。 侦听器 IP 地址必须是 IPv4 地址。 你还可以使用`0.0.0.0`。 

更新你的环境的所有 SQL Server 实例上的以下 TRANSACT-SQL 脚本： 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!NOTE]
>如果你使用 SQL Server Express Edition 在一个节点上承载仅配置副本中，唯一有效的值为`ROLE`是`WITNESS`。 在 SQL Server Express Edition 上运行以下脚本：

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

在防火墙上的 TCP 端口必须打开侦听器端口。



>[!IMPORTANT]
>对于 SQL Server 2017 版本中，支持数据库镜像终结点的唯一身份验证方法是`CERTIFICATE`。 `WINDOWS`选项将在未来版本中启用。

有关详细信息，请参阅[数据库镜像终结点 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)。


