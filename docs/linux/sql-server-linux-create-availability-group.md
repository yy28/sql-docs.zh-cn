---
title: "创建和配置 Linux 上的 SQL Server 的可用性组 |Microsoft 文档"
description: "本教程演示如何创建和配置可用性组在 Linux 上的 SQL server。"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 8c055558b2a1e8287272835a0a1c0d2e2dc94f02
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>创建和配置 Linux 上的 SQL Server 的可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何创建和配置可用性组 (AG) 用于[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上。 与不同[!INCLUDE[sssql15-md](../includes/sssql15-md.md)]和更早版本在 Windows 上，你可以启用承载个可用性组或而无需首先创建基础 Pacemaker 群集。 群集后，如果需要不进行集成之前更高版本。

本教程包括以下任务：
 
> [!div class="checklist"]
> * 启用可用性组。
> * 创建可用性组终结点和证书。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 创建可用性组。
> * 创建[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登录名和 Pacemaker 的权限。
> * 在 Pacemaker 群集 （仅适用于外部类型） 中创建可用性组资源。

## <a name="prerequisite"></a>前提条件
- 部署 Pacemaker 高可用性群集中所述[为在 Linux 上的 SQL Server 部署 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md)。


## <a name="enable-the-availability-groups-feature"></a>启用可用性组功能

与在 Windows 上，您无法使用 PowerShell 或[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Configuration Manager 以启用可用性组 (AG) 功能。 在 Linux，则必须使用`mssql-conf`启用的功能。 若要启用的可用性组功能使用两种方式： 使用`mssql-conf`实用程序或编辑`mssql.conf`手动文件。

> [!IMPORTANT]
> 可用性组功能必须启用对于仅配置副本，即使在[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。

### <a name="use-the-mssql-conf-utility"></a>使用 mssql conf 实用程序

在提示符下发出以下：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>编辑 mssql.conf 文件

你还可以修改`mssql.conf`文件，位于`/var/opt/mssql`文件夹中，添加以下行：

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>重新启动[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
启用可用性组，如在 Windows 上，你必须重新启动后[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 可以通过以下：

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>创建可用性组终结点和证书

可用性组使用的 TCP 终结点进行通信。 在 Linux，如果使用证书进行身份验证仅支持可用性组的终结点。 这意味着，必须将参与同一个可用性组的副本的所有其他实例上还原一个实例中的证书。 即使对于仅配置副本需要证书过程。 

创建终结点和还原证书仅可以通过 TRANSACT-SQL 来完成。 你可以使用非[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-生成以及证书。 你还需要一个过程来管理，并将任何过期的证书。

> [!IMPORTANT]
> 如果你打算使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]向导以创建可用性组，您仍需要创建并在 Linux 上使用 TRANSACT-SQL 还原证书。

有关可用于各种不同的命令 （如其他安全） 的选项的完整语法，请参阅：

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [创建证书](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 尽管你将创建可用性组，将终结点的类型使用*FOR DATABASE_MIRRORING*，这是因为某些基础方面一次共享与该现在已弃用的功能。

此示例将创建三个节点配置的证书。 实例名是 LinAGN1、 LinAGN2 和 LinAGN3。

1.  执行以下操作在 LinAGN1 创建主密钥、 证书和终结点，以及备份证书。 对于此示例，典型的 TCP 端口 5022 用于终结点。
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  执行 LinAGN2 相同操作：
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  最后，在 LinAGN3 上执行相同的序列：
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  使用`scp`或另一个实用工具，将该证书的备份复制到将成为可用性组的一部分的每个节点。
    
    对于此示例中：
    
    - 将 LinAGN1_Cert.cer 复制到 LinAGN2 和 LinAGN3
    - 复制到 LinAGN1 和 LinAGN3 LinAGN2_Cert.cer。
    - 复制到 LinAGN1 和 LinAGN2 LinAGN3_Cert.cer。
    
5.  更改所有权和与复制的证书文件关联的组`mssql`。
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  创建实例级登录名和与 LinAGN2 和 LinAGN3 LinAGN1 上的相关联的用户。
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  还原 LinAGN2_Cert 和 LinAGN3_Cert LinAGN1 上。 无其他副本的证书是可用性组通信和安全的一个重要方面。
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  创建实例级登录名和与 LinAGN1 和 LinAGN3 LinAGN2 上的相关联的用户。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10.  还原 LinAGN1_Cert 和 LinAGN3_Cert LinAGN2 上。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
11.  Grant the logins associated with LinAG1 and LinAGN3 permission to connect to the endpoint on LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12.  创建实例级登录名和与 LinAGN1 和 LinAGN2 LinAGN3 上的相关联的用户。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13.  还原 LinAGN1_Cert 和 LinAGN2_Cert LinAGN3 上。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
14.  Grant the logins associated with LinAG1 and LinAGN2 permission to connect to the endpoint on LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>创建可用性组

本部分介绍如何使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 创建的可用性组[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

本部分演示如何创建可用性组的外部群集类型 SSMS 使用新建可用性组向导。

1.  在 SSMS 中，展开**Always On 高可用性**，右键单击**可用性组**，然后选择**新建可用性组向导**。

2.  在简介对话框中，单击**下一步**。

3.  在指定可用性组选项对话框中，输入可用性组的名称并选择外部或 NONE 下拉列表中的群集类型。 将部署 Pacemaker 时，应使用外部。 没有专用的情况下，如读取横向扩展。选择数据库级别的运行状况检测的选项是可选的。 此选项的详细信息，请参阅[可用性组数据库级别的运行状况检测故障转移选项](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)。 单击“下一步” 。

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  在选择数据库对话框中，选择将参与可用性组的数据库。 每个数据库必须具有完整备份，然后将它添加到可用性组。 单击“下一步” 。

5.  在指定副本对话框中，单击**将副本添加**。

6.  在连接到服务器对话框中，输入 Linux 实例的名称[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]将辅助副本，以及要连接的凭据。 单击 **“连接”**。

7.  重复前面的两个步骤将包含仅配置副本或另一个辅助副本的实例。

8.  现在，所有三个实例应列出在指定副本对话框。 如果将为 true 的辅助数据库的辅助副本使用外部，群集类型，请确保可用性模式匹配的主副本和故障转移模式设置为外部。 对于仅配置副本中，选择仅限的配置的可用性模式。

    下面的示例演示两个副本、 一种群集类型的外部，与仅配置副本的可用性组。

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    下面的示例演示使用两个副本 AG、 None、 和仅配置副本的群集类型。

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  如果你想要更改的备份首选项，请单击备份首选项选项卡。与承载个可用性组的备份首选项的详细信息，请参阅[配置可用性副本备份](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。

10. 如果使用可读辅助数据库或与群集一起创建可用性组类型都不用于读取缩放，你可以通过选择侦听器选项卡创建侦听器。也可以稍后添加侦听器。 若要创建一个侦听器，请选择选项**创建可用性组侦听器**并输入一个名称、 TCP/IP 端口，以及是否使用静态或自动分配 DHCP IP 地址。 请记住，对于群集类型为一个可用性组，IP 应为静态，并且已设置到的主 IP 地址。

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 如果可读的方案创建了一个侦听器，17.3 或更高版本的 SSMS 将允许只读路由在向导中的创建。 它也可以添加更高版本通过 SSMS 或 TRANSACT-SQL。 若要添加只读路由现在：

    a.  选择只读路由选项卡。

    b.  输入只读副本的 Url。 这些 Url 是实例的类似于终结点，，只不过它们使用，不的终结点的端口。

    c.  选择每个 URL，然后从底部，选择可读副本。 选择多个按下 SHIFT 或单击拖动。

12. 单击“下一步” 。

13. 选择如何将初始化辅助副本。 默认值是使用[自动种子设定](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)，这需要参与可用性组的所有服务器上的同一路径。 此外可以让向导执行备份、 复制和还原 （第二个选项）;其加入如果手动备份、 复制和还原副本上的数据库 （第三个选项）;或更高版本添加数据库 （在最后选项）。 通过使用证书，如果您是手动进行备份，并将其复制，备份文件的权限将需要在其他副本上设置。 单击“下一步” 。

14. 在验证对话框中，如果所有内容将不起返回为成功，调查。 一些警告是可以接受且不致命的例如如果你不创建侦听器。 单击“下一步” 。

15. 在摘要对话框中，单击**完成**。 现在将开始创建可用性组的过程。

16. 可用性组创建完成后，单击**关闭**的结果。 你现在可以看到对中的动态管理视图以及在 SSMS 中的 Always On 高可用性文件夹下的副本的可用性组。

### <a name="use-transact-sql"></a>使用 TRANSACT-SQL

本部分说明了创建使用 Transact SQL 可用性组的示例。 创建可用性组后，可以配置的侦听器和只读路由。 可用性组本身可以修改与`ALTER AVAILABILITY GROUP`，但更改群集类型中无法执行[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您不打算使用的外部群集类型创建可用性组，必须将其删除并重新创建该群集类型为 None。 可以通过以下链接找到详细信息和其他选项：

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)（创建可用性组 (Transact-SQL)）
-   [更改可用性组 (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [配置只读路由的可用性组 (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [创建或配置可用性组侦听器 (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one--two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>示例 1 – 2 个副本配置只读副本 （外部群集类型）

此示例演示如何创建使用仅配置副本 2 副本可用性组。

1.  在将包含数据库的完全读/写副本的主副本的节点上执行。 此示例使用自动种子设定。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  在查询窗口中连接到另一个副本，执行以下操作来将副本联接到可用性组和启动到辅助副本从主种子设定过程。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  在查询窗口中连接到配置唯一的副本，请将其联接到可用性组。
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    ```

#### <a name="example-two--three-replicas-with-read-only-routing-external-cluster-type"></a>示例 2 – 3 个副本使用只读路由 （外部群集类型）

此示例显示三个完整副本和如何只读路由可以配置为在初始的可用性组创建的过程。

1.  在将包含数据库的完全读/写副本的主副本的节点上执行。 此示例使用自动种子设定。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    有关此配置，需要注意的几件事：
    
    - *AGName*是可用性组的名称。
    - *DBName*是将使用与该可用性组的数据库的名称。 这也可以是用逗号分隔的名称的列表。
    - *ListenerName*是不同于任何基础服务器节点的名称。 它将在一起的 DNS 中注册*IPAddress*。
    - *IPAddress*是与关联的 IP 地址*ListenerName*。 它也是唯一和不与任何服务器/节点相同。 应用程序和最终用户将使用两种*ListenerName*或*IPAddress*连接到可用性组。
    - *子网掩码*是子网掩码为*IPAddress*; 例如，255.255.255.0。

2.  在查询窗口中连接到另一个副本，执行以下操作来将副本联接到可用性组和启动到辅助副本从主种子设定过程。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  第三个副本，重复操作步骤 2。

#### <a name="example-three--two-replicas-with-read-only-routing-none-cluster-type"></a>示例 3 – 两个副本使用只读路由 （无群集类型）

此示例演示如何创建一个使用为无群集类型的两个副本配置。 它用于读取的缩放方案的地方没有故障转移。 这将创建为实际的主副本，以及只读路由，使用的轮循机制功能的侦听器。

1.  在将包含数据库的完全读/写副本的主副本的节点上执行。 此示例使用自动种子设定。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    位置
    - *AGName*是可用性组的名称。
    - *DBName*是将使用与该可用性组的数据库的名称。 这也可以是用逗号分隔的名称的列表。
    - *PortOfEndpoint*是通过创建的终结点使用的端口号。
    - *PortOfInstance*是实例所使用的端口号[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。
    - *ListenerName*是不同的任何基础的副本，但实际上不会使用的名称。
    - *PrimaryReplicaIPAddress*是主副本的 IP 地址。
    - *子网掩码*是子网掩码为*IPAddress*。 例如，255.255.255.0。
    
2.  将辅助副本联接到可用性组并执行自动种子设定操作。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>创建[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登录名和 Pacemaker 的权限

Pacemaker 高可用性群集基础[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上需要访问[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]实例，以及其自身的可用性组上的权限。 这些步骤创建登录名和关联的权限，以及一个文件，告知如何登录到的 Pacemaker [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

1.  在查询窗口中连接到第一个副本，执行下列语句：

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD '<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  在节点 1 上，输入命令 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    这将打开 Emacs 编辑器。
    
3.  在编辑器中输入以下两行：

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  按住 CTRL 键，然后按 X，然后 C 中，若要退出并保存该文件。

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    若要锁定的文件。

6.  重复步骤 1-5 将充当副本的其他服务器上。

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>在 Pacemaker 群集 （仅适用于外部） 中创建可用性组资源

在可用性组创建中[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，相应的资源必须创建 Pacemaker，在指定的外部群集类型。 有两个与可用性组关联的资源： 可用性组本身和 IP 地址。 配置 IP 地址资源是可选的如果你未使用与侦听器的功能，但建议。

创建可用性组资源是资源的一种特殊的称为克隆。 可用性组资源实质上是每个节点上具有副本，并且没有一个控制的资源名 master。 主都使用承载主副本的服务器相关联。 辅助副本 （正则或仅配置） 被视为从属服务和可以提升为 master 的故障转移。

1.  使用以下语法创建可用性组资源：

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> --master meta notify=true
    ```

    >[!NOTE]
    >RHEL 7.4 上可能会遇到与使用-master 警告。 若要避免此问题，请使用`sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    其中*NameForAGResource*是为可用性组中，提供对此群集资源的唯一名称和*AGName*是创建可用性组的名称。
 
2.  创建可用性组具有侦听器功能相关联的 IP 地址资源。

    **RHEL 和 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    其中*NameForIPResource*是为 IP 资源的唯一名称和*IPAddress*是分配给该资源的静态 IP 地址。 在 SLES，你还需要提供子网掩码。 例如，255.255.255.0 将具有值为 24*子网掩码。*
    
3.  若要确保在同一个节点上运行的 IP 地址和可用性组资源，必须配置归置约束。

    **RHEL 和 Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    其中*NameForIPResource*是为 IP 资源的名称*NameForAGResource*是名称的可用性组资源，然后在 SLES， *NameForConstraint*是的名称约束。

4.  创建一个排序约束来确保可用性组资源已启动并运行之前的 IP 地址。 归置约束意味着排序约束，虽然这强制执行它。

    **RHEL 和 Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    其中*NameForIPResource*是为 IP 资源的名称*NameForAGResource*是名称的可用性组资源，然后在 SLES， *NameForConstraint*是的名称约束。

## <a name="next-steps"></a>后续步骤

在本教程中，您学习了如何创建和配置的可用性组[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上。 你应该了解一下如何到：
> [!div class="checklist"]
> * 启用可用性组。
> * 创建可用性组终结点和证书。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 创建可用性组。
> * 创建[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登录名和 Pacemaker 的权限。
> * 在 Pacemaker 群集中创建可用性组资源。

对于大多数可用性组管理任务，包括升级和故障转移，请参阅：

> [!div class="nextstepaction"]
> [运行的 Linux 上的 SQL Server 的 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)

