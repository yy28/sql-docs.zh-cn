## <a name="prerequisites"></a>先决条件

创建可用性组前，需要：

- 设置环境，以便所有托管可用性副本的服务器能够通信。
- 安装 SQL Server。

>[!NOTE]
>在 Linux 上，必须先创建可用性组，然后再将其添加为群集管理的群集资源。 本文档举例说明了如何创建可用性组。 有关在各种发行版中创建群集并将可用性组添加为群集资源的特定说明，请参阅“后续步骤”中的链接。

1. 更新每个主机的计算机名。

   每个 SQL Server 名称必须：
   
   - 不超过 15 个字符。
   - 在网络中唯一。
   
   若要设置计算机名，请编辑 `/etc/hostname`。 以下脚本可使用 `vi` 编辑 `/etc/hostname`：

   ```bash
   sudo vi /etc/hostname
   ```

2. 配置主机文件。

    >[!NOTE]
    >如果在 DNS 服务器中使用主机 IP 注册主机名，则无需执行以下步骤。 验证要作为可用性组配置的一部分的所有节点是否可以互相通信。 （对主机名的 ping 应使用相应的 IP 地址进行回复。）此外，请确保 /etc/hosts 文件不包含将节点主机名映射到本地主机 IP 地址 127.0.0.1 的记录。
    >

   每个服务器上的主机文件包含将加入可用性组的所有服务器的 IP 地址和名称。 

   以下命令将返回当前服务器的 IP 地址：

   ```bash
   sudo ip addr show
   ```

   更新 `/etc/hosts`。 以下脚本可使用 `vi` 编辑 `/etc/hosts`：

   ```bash
   sudo vi /etc/hosts
   ```

   下面的示例演示了 node1 上的 `/etc/hosts`，并补充了 node1、node2 和 node3     。 在本文档中，node1 指托管主要副本的服务器  。 node2 和 node3 指托管次要副本的服务器   。

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>安装 SQL Server

安装 SQL Server。 以下链接指向适用于各种分发的 SQL Server 安装说明： 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>启用 AlwaysOn 可用性组，并重启 mssql-server

在托管 SQL Server 实例的每个节点上启用 AlwaysOn 可用性组。 然后重新启动 `mssql-server`。 运行以下脚本：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwayson_health-event-session"></a>启用 AlwaysOn_health 事件会话 

可选择性地启用 AlwaysOn 可用性组的扩展事件，以便在对可用性组进行故障排除时帮助诊断根本原因。 在每个 SQL Server 实例上运行以下命令： 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

有关此 XE 会话的详细信息，请参阅 [AlwaysOn 扩展事件](https://msdn.microsoft.com/library/dn135324.aspx)。

## <a name="create-a-certificate"></a>创建证书

Linux 上的 SQL Server 服务使用证书验证镜像终结点之间的通信。 

以下 Transact-SQL 脚本创建主密钥和证书。 然后备份证书，并使用私钥保护文件。 使用强密码更新脚本。 连接到主要 SQL Server 实例。 若要创建证书，请运行以下 Transact-SQL 脚本：

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

现在主 SQL Server 副本的证书位于 `/var/opt/mssql/data/dbm_certificate.cer`，私钥位于 `var/opt/mssql/data/dbm_certificate.pvk`。 将这两个文件复制到所有要托管可用性副本的服务器上的同一位置。 使用 mssql 用户或为 mssql 用户授予访问这些文件的权限。 

例如，在源服务器上，以下命令可将文件复制到目标计算机。 将 `**<node2>**` 值替换为要托管副本的 SQL Server 实例的名称。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

在每个目标服务器上，为 mssql 用户授予访问证书的权限。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>在辅助服务器上创建证书

以下 Transact-SQL 脚本根据在主 SQL Server 副本上创建的备份创建主密钥和证书。 使用强密码更新脚本。 解密密码与在此前的步骤中创建 .pvk 文件使用的密码相同。 若要创建证书，请在所有辅助服务器上运行以下脚本：

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>在所有副本上创建数据库镜像终结点

数据库镜像端点使用传输控制协议 (TCP) 在参与数据库镜像会话或承载可用性副本的服务器实例之间发送和接收消息。 数据库镜像端点在唯一的 TCP 端口号上进行侦听。 

以下 Transact-SQL 脚本为可用性组创建名为 `Hadr_endpoint` 的侦听终结点。 它启动终结点，并向创建的证书授予连接权限。 在运行该脚本之前，替换 `**< ... >**` 之内的值。 （可选）可以包含 IP 地址 `LISTENER_IP = (0.0.0.0)`。 侦听器 IP 地址必须是 IPv4 地址。 还可以使用 `0.0.0.0`。 

为所有 SQL Server 实例上的环境更新以下 Transact-SQL 脚本： 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

>[!NOTE]
>如果在一个节点上使用 SQL Server Express Edition 托管仅限配置的副本，则 `ROLE` 的唯一有效值为 `WITNESS`。 在 SQL Server Express Edition 上运行以下脚本：

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

防火墙上的 TCP 端口必须对侦听器端口打开。



>[!IMPORTANT]
>对于 SQL Server 2017 版本，数据库镜像终结点支持的唯一身份验证方法是 `CERTIFICATE`。 未来的版本中将启用 `WINDOWS` 选项。

有关详细信息，请参阅 [数据库镜像端点 (SQL Server)](https://msdn.microsoft.com/library/ms179511.aspx)。


