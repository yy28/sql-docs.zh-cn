---
title: 创建和配置 Linux 上的 SQL Server 可用性组 |Microsoft Docs
description: 本教程演示如何创建和配置 Linux 上的 SQL Server 的可用性组。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 9a9a3d18f1850b563882a2303db8dd28b2916ac4
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542227"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>创建和配置 Linux 上的 SQL Server 可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何创建和配置可用性组 (AG) 用于[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上。 与不同[!INCLUDE[sssql15-md](../includes/sssql15-md.md)]并且前面上 Windows，你可以启用 Ag 或而无需首先创建基础的 Pacemaker 群集。 群集后，必要时，不进行集成到更高版本。

本教程包括以下任务：
 
> [!div class="checklist"]
> * 启用可用性组。
> * 创建可用性组终结点和证书。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 创建可用性组。
> * 创建[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登录名和 Pacemaker 的权限。
> * Pacemaker 群集 （仅适用于外部类型） 中创建可用性组资源。

## <a name="prerequisite"></a>先决条件
- 部署 Pacemaker 实现高可用性群集中所述[Linux 上的 SQL Server 部署 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md)。


## <a name="enable-the-availability-groups-feature"></a>启用可用性组功能

不同于上 Windows，您无法使用 PowerShell 或[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]配置管理器启用可用性组 (AG) 功能。 在 Linux，则必须使用`mssql-conf`以启用该功能。 有两种方法来启用可用性组功能： 使用`mssql-conf`实用程序或编辑`mssql.conf`手动文件。

> [!IMPORTANT]
> 必须仅配置副本，甚至上启用可用性组功能[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。

### <a name="use-the-mssql-conf-utility"></a>使用 mssql-conf 实用工具

在提示符下发出以下：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>编辑 mssql.conf 文件

您还可以修改`mssql.conf`文件，位于下`/var/opt/mssql`文件夹中，添加以下行：

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>重新启动 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
启用可用性组，如上 Windows，则必须重新启动后[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 可以通过以下方法：

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>创建可用性组终结点和证书

可用性组使用 TCP 终结点进行通信。 在 Linux 中，如果使用证书进行身份验证仅支持 AG 的终结点。 这意味着，必须将参与同一个可用性组副本的所有其他实例上还原一个实例中的证书。 即使对于仅配置副本需要证书的过程。 

仅可以通过 TRANSACT-SQL 完成创建终结点和还原证书。 您可以使用非[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-生成的证书以及。 您还需要一个过程来管理和替换任何过期的证书。

> [!IMPORTANT]
> 如果你打算使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]向导创建可用性组，您仍需要创建并在 Linux 上使用 TRANSACT-SQL 还原证书。

有关可用于各种不同的命令 （如其他安全） 的选项的完整语法，请参阅：

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [创建证书](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 虽然您将创建可用性组，但使用终结点的类型*FOR DATABASE_MIRRORING*，这是因为某些基础方面一次共享了该现已弃用的功能。

此示例将创建三节点配置的证书。 实例名称是 LinAGN1、 LinAGN2 和 LinAGN3。

1.  执行以下操作在 LinAGN1 创建主密钥、 证书和终结点，以及备份证书。 对于此示例中，典型的 TCP 端口 5022 用于终结点。
    
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
    
3.  最后，LinAGN3 上执行相同的序列：
    
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
    
4.  使用`scp`或另一个实用程序，将证书的备份复制到每个节点都将成为可用性组的一部分。
    
    对于此示例：
    
    - 将 LinAGN1_Cert.cer 复制到 LinAGN2 和 LinAGN3
    - 复制到 LinAGN1 和 LinAGN3 LinAGN2_Cert.cer。
    - 复制到 LinAGN1 和 LinAGN2 LinAGN3_Cert.cer。
    
5.  更改所有权和与复制的证书文件关联的组`mssql`。
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  创建实例级登录名和用户与 LinAGN2 和 LinAGN3 LinAGN1 上的相关联。
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  还原 LinAGN2_Cert 和 LinAGN3_Cert LinAGN1 上。 其他副本的证书是可用性组通信和安全的一个重要方面。
    
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
    
9.  创建实例级登录名和用户与 LinAGN1 和 LinAGN3 LinAGN2 上的相关联。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. 还原 LinAGN1_Cert 和 LinAGN3_Cert LinAGN2 上。
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. 授予与连接到的终结点上 LinAGN2 LinAG1 和 LinAGN3 权限相关联的登录名。
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. 创建实例级登录名和用户与 LinAGN1 和 LinAGN2 LinAGN3 上的相关联。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. 还原 LinAGN1_Cert 和 LinAGN2_Cert LinAGN3 上。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. 授予与连接到的终结点上 LinAGN3 LinAG1 和 LinAGN2 权限相关联的登录名。
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>创建可用性组

本部分介绍了如何使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 创建的可用性组的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>使用 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

本部分演示如何创建具有外部群集类型 AG 在使用新建可用性组向导使用 SSMS。

1.  在 SSMS 中，展开**Always On 高可用性**，右键单击**可用性组**，然后选择**新建可用性组向导**。

2.  在简介对话框中，单击**下一步**。

3.  在指定可用性组选项对话框中，输入可用性组的名称并选择群集类型为 EXTERNAL 或 NONE 下拉列表中。 将部署 Pacemaker 时，应使用外部。 没有为专用方案，例如读取横向扩展。选择的数据库级别运行状况检测选项是可选的。 此选项的详细信息，请参阅[可用性组数据库级别运行状况检测故障转移选项](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)。 单击“下一步” 。

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  在选择数据库对话框中，选择将参与可用性组的数据库。 可以将它添加到可用性组之前，每个数据库必须具有完整备份。 单击“下一步” 。

5.  在指定副本对话框中，单击**将副本添加**。

6.  在连接到服务器对话框中，输入 Linux 实例的名称[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]将辅助副本，以及要连接的凭据。 单击 **“连接”**。

7.  重复前两个步骤将包含仅配置副本或另一个辅助副本的实例。

8.  在指定副本对话框现在应列出所有三个实例。 如果使用的外部，群集类型为将为 true 的辅助数据库的辅助副本，请确保的可用性模式与匹配的主副本和故障转移模式设置为 External。 仅配置副本，选择仅限的配置的可用性模式。

    下面的示例演示两个副本、 群集类型的外部，与仅配置副本 AG。

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    下面的示例演示具有两个副本 AG、 None、 和仅配置副本的群集类型。

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  如果你想要更改的备份首选项，请单击备份首选项选项卡上。使用 Ag 的备份首选项的详细信息，请参阅[可用性副本上的配置备份](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。

10. 如果使用可读辅助数据库或与群集一起创建 AG 的读取缩放未使用任何类型，您可以通过选择侦听器选项卡创建侦听器。也可以稍后添加侦听器。 若要创建一个侦听器，请选择选项**创建可用性组侦听器**并输入一个名称、 TCP/IP 端口，以及是否使用静态或自动分配 DHCP IP 地址。 请记住，对于群集类型为 None 的 AG，IP 应为静态，并且已设置到的主 IP 地址。

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 如果可读的情况下创建一个侦听器，则 SSMS 17.3 或更高版本允许在只读路由向导中的创建。 它还可以添加更高版本通过 SSMS 或 TRANSACT-SQL。 若要添加只读路由现在：

    a.  选择只读路由选项卡。

    b.  输入只读副本的 Url。 这些 Url 是实例的终结点，类似，只不过它们使用，不终结点的端口。

    c.  选择每个 URL，然后从底部，选择可读副本。 进行多选，按住 shift 键或单击拖动。

12. 单击“下一步” 。

13. 选择如何将初始化辅助副本。 默认值是使用[自动种子设定](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)，这要求在参与可用性组的所有服务器上的同一路径。 您还可以让该向导进行备份、 复制和还原 （第二个选项）;将其加入如果手动备份、 复制和还原数据库副本上的 （第三个选项）;或更高版本将数据库添加 （最后一个选项）。 通过使用证书，如果您手动进行备份并将其复制，需要设置其他副本上备份文件的权限。 单击“下一步” 。

14. 在验证对话框中，如果所有内容不会无法恢复为成功，调查。 一些警告，是可接受和不严重错误，例如如果你没有创建侦听器。 单击“下一步” 。

15. 在摘要对话框中，单击**完成**。 现在将开始创建可用性组的过程。

16. 可用性组创建完成后，单击**关闭**的结果。 现在可以对副本中的动态管理视图以及在 SSMS 中的 Always On 高可用性文件夹下看到可用性组。

### <a name="use-transact-sql"></a>使用 Transact-SQL

本部分介绍创建使用 Transact SQL AG 的示例。 创建可用性组后，可以配置侦听器和只读路由。 可以通过修改可用性组本身`ALTER AVAILABILITY GROUP`，但不能完成的群集类型的更改[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您不打算使用的外部群集类型创建一个 AG，必须将其删除并重新创建该群集类型为 None。 可以在以下链接中找到详细信息和其他选项：

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)（创建可用性组 (Transact-SQL)）
-   [更改可用性组 (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [配置只读路由的可用性组 (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [创建或配置可用性组侦听器 (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>与仅配置副本 （外部群集类型） 的示例一两个副本

此示例演示如何创建使用仅配置副本的两个副本 AG。

1.  将包含数据库的完全读/写副本的主副本在节点上执行。 此示例使用自动种子设定。

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
    
2.  在查询窗口中连接到另一个副本，执行以下命令将副本联接到可用性组，并启动到辅助副本从主种子设定过程。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. 在查询窗口中连接到仅配置副本，请将其联接到可用性组。
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>示例 2-3 个副本的只读路由 （外部群集类型）

此示例显示三个完整副本和如何只读路由可配置为在初始的可用性组创建的过程。

1.  将包含数据库的完全读/写副本的主副本在节点上执行。 此示例使用自动种子设定。

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
    
    需要注意此配置的几个事项：
    
    - *AGName*是可用性组的名称。
    - *DBName*是将使用与该可用性组的数据库的名称。 它可以是一系列由逗号分隔的名称。
    - *ListenerName*是不同于任何基础服务器节点的名称。 它将在与 DNS 中注册*IPAddress*。
    - *IPAddress*是与之关联的 IP 地址*ListenerName*。 它也是唯一并不完全相同的任何服务器节点。 应用程序和最终用户将使用两种*ListenerName*或*IPAddress*连接到可用性组。
    - *子网掩码*是的子网掩码*IPAddress*; 例如，255.255.255.0。

2.  在查询窗口中连接到另一个副本，执行以下命令将副本联接到可用性组，并启动到辅助副本从主种子设定过程。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  重复步骤 2 的第三个副本。

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>示例三两个副本的只读路由 （无群集类型）

此示例演示如何创建一个使用群集类型为 None 的两个副本配置。 它用于读取的缩放方案的地方不会故障转移。 这将创建的侦听器是实际的主副本，以及只读路由，使用轮循机制功能。

1.  将包含数据库的完全读/写副本的主副本在节点上执行。 此示例使用自动种子设定。

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
    - *DBName*是将使用与该可用性组的数据库的名称。 它可以是一系列由逗号分隔的名称。
    - *PortOfEndpoint*是由创建的终结点的端口号。
    - *PortOfInstance*是由的实例使用的端口号[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。
    - *ListenerName*是不同于任何基础的副本，但实际上不会使用的名称。
    - *PrimaryReplicaIPAddress*是主副本的 IP 地址。
    - *子网掩码*是的子网掩码*IPAddress*。 例如，255.255.255.0。
    
2.  将辅助副本联接到可用性组并执行自动种子设定操作。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>创建[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登录名和 Pacemaker 的权限

Pacemaker 实现高可用性群集基础[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上需要有权[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]实例，以及对可用性组本身的权限。 这些步骤创建登录名和关联的权限，以及文件，告知如何登录到的 Pacemaker [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

1.  在查询窗口中连接到第一个副本，执行以下脚本：

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
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
    
3.  编辑器中输入以下两行：

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  按住 CTRL 键，然后按 X，然后 C，退出并保存该文件。

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    若要锁定该文件。

6.  重复步骤 1-5 将作为副本的其他服务器上。

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Pacemaker 群集 （仅适用于外部） 中创建可用性组资源

后一个可用性组创建在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，指定外部群集类型时必须在 Pacemaker，创建相应的资源。 有两个与可用性组相关联的资源： 可用性组本身和一个 IP 地址。 如果未使用的侦听器功能，但建议使用配置的 IP 地址资源是可选的。

创建可用性组资源是资源的一种特殊的名为克隆。 可用性组资源实质上是每个节点上有副本，并且没有一个名为 master 的控制资源。 在主机都使用承载主副本的服务器相关联。 辅助副本 （定期或仅配置） 都被认为是从属服务和可以提升为 master 中故障转移。

1.  使用以下语法创建可用性组资源：

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >在 RHEL 7.4，可能会遇到与使用-master 警告。 若要避免此问题，请使用 `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
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
    
    其中*NameForAGResource*是为可用性组，提供给该群集资源的唯一名称和*AGName*创建可用性组的名称。
 
2.  创建可用性组侦听器功能相关联的 IP 地址资源。

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
    
    其中*NameForIPResource*是 IP 资源的唯一名称和*IPAddress*是分配给该资源的静态 IP 地址。 在 SLES，还需要提供子网掩码。 例如，255.255.255.0 将具有值为 24 的*子网掩码。*
    
3.  若要确保在同一节点上运行的 IP 地址和可用性组资源，必须配置的主机托管约束。

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
    
    其中*NameForIPResource*是为 IP 资源名称*NameForAGResource*该名称对于可用性组资源，并在 SLES， *NameForConstraint*的名称约束。

4.  创建一个排序约束以确保可用性组资源已启动并运行之前的 IP 地址。 主机托管约束意味着排序约束，虽然这强制执行它。

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
    
    其中*NameForIPResource*是为 IP 资源名称*NameForAGResource*该名称对于可用性组资源，并在 SLES， *NameForConstraint*的名称约束。

## <a name="next-steps"></a>后续步骤

在本教程中，您学习了如何创建和配置的可用性组[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上。 你将了解到：
> [!div class="checklist"]
> * 启用可用性组。
> * 创建可用性组终结点和证书。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 创建可用性组。
> * 创建[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登录名和 Pacemaker 的权限。
> * Pacemaker 群集中创建可用性组资源。

对于大多数 AG 管理任务，包括升级和故障转移，请参阅：

> [!div class="nextstepaction"]
> [Linux 上的 SQL Server 运行 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)

