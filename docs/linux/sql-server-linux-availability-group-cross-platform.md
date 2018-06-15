---
title: 配置 SQL Server Always On Windows 和 Linux 上的可用性组 |Microsoft 文档
description: 配置 SQL Server 可用性组在 Windows 和 Linux 上的副本。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/31/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 9ccd5cb5fdc7d5c5bc6ff62b203bee0bbce6e5e8
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34322758"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>配置 SQL Server Always On 可用性组在 Windows 和 Linux （跨平台） 上

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

此文章介绍了创建具有 Windows server 上的一个副本和 Linux 服务器上的其他副本始终在可用性组 (AG) 的步骤。 此配置是跨平台，因为副本均在不同操作系统上。 迁移到另一个平台或灾难恢复 (DR) 使用此配置。 此配置不支持高可用性，因为没有任何群集解决方案来管理跨平台配置。 

![混合无](./media/sql-server-linux-availability-group-overview/image1.png)

在继续之前，应熟悉安装和配置 Windows 和 Linux 上的 SQL Server 实例。 

## <a name="scenario"></a>应用场景

在此方案中，两个服务器是在不同操作系统上。 名为 Windows Server 2016`WinSQLInstance`承载主副本。 一个名为的 Linux 服务器`LinuxSQLInstance`承载辅助副本。

## <a name="configure-the-ag"></a>配置可用性组 

创建可用性组的步骤是创建适用于读取规模工作负荷的可用性组的步骤相同。 可用性组群集类型为 NONE，因为没有任何群集管理器。 

   >[!NOTE]
   >对于本文中的脚本，尖括号`<`和`>`确定你需要更换为您的环境的值。 命令的尖括号本身不需要的脚本。 

1. 在 Windows Server 2016 上安装 SQL Server 自 2017 年，启用 Alwayson 可用性组从 SQL Server 配置管理器中，并设置混合的模式身份验证。 

   >[!TIP]
   >如果您要验证此解决方案在 Azure 中的，将这两个服务器放在同一可用性集中，以确保它们在数据中心中隔开。 

   **启用可用性组**

   有关说明，请参阅[启用和禁用 Alwayson 可用性组 (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。

   ![启用可用性组](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server 配置管理器说明计算机不是故障转移群集中的节点。 

   启用可用性组后，重新启动 SQL Server。

   **设置混合的模式身份验证**

   有关说明，请参阅[更改服务器身份验证模式](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure)。

1. 在 Linux 上安装 SQL Server 自 2017 年。 有关说明，请参阅[安装 SQL Sever](sql-server-linux-setup.md)。 启用`hadr`通过 mssql 联赛

   若要启用`hadr`从外壳提示符 mssql conf，通过发出以下命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   启用后`hadr`，重新启动 SQL Server 实例。  

   下图显示此完成的步骤。

   ![启用可用性组 Linux](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. 配置两个服务器上的主机文件或向 DNS 注册的服务器名称。

1. 打开防火墙端口 TPC 1433 和 5022 在 Windows 和 Linux 上。

1. 在主副本上创建数据库登录名和密码。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. 在主副本上，创建主密钥和证书，然后将证书备份的私钥。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. 在复制到 Linux 服务器 （辅助副本） 的证书和私钥`/var/opt/mssql/data`。 你可以使用`pscp`将文件复制到 Linux 服务器。 

1. 设置的组和所有权的私钥和证书到`mssql:mssql`。

   以下脚本将设置的组和文件的所有权。 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   在下图中，所有权和组设置是正确的证书和密钥。

   ![启用可用性组 Linux](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. 在辅助副本上，创建数据库登录名和密码并创建主密钥。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. 在辅助副本上还原的证书复制到`/var/opt/mssql/data`。 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. 在主副本上创建一个终结点。

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >防火墙必须打开 TCP 端口的侦听器。 在前面的脚本中，端口为 5022。 使用任何可用 TCP 端口。 

1. 在辅助副本上创建终结点。 重复上述脚本创建的终结点在辅助副本上。 

1. 在主副本上创建可用性组与`CLUSTER_TYPE = NONE`。 示例脚本使用`SEEDING_MODE = AUTOMATIC`创建可用性组。 

   >[!NOTE]
   >当 SQL Server 的 Windows 实例数据和日志文件，自动种子设定到 SQL Server 的 Linux 实例失败，因为这些路径不存在辅助副本上使用不同的路径。 若要使用跨平台可用性组的以下脚本，数据库，请要求 Windows server 上的数据和日志文件的相同的路径。 或者，你可以更新脚本以设置`SEEDING_MODE = MANUAL`，然后备份和还原的数据库`NORECOVERY`植入到数据库。 
   >
   >此行为适用于 Azure 应用商店映像。 
   >
   >有关自动种子设定的详细信息，请参阅[自动种子设定的磁盘布局](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout)。 

   运行该脚本之前，你承载个可用性组的更新的值。

      * 替换`<WinSQLInstance>`与主要副本 SQL Server 实例的服务器名称。

      * 替换`<LinuxSQLInstance>`与辅助副本的 SQL Server 实例的服务器名称。 

   若要创建可用性组，更新的值，并在主副本上运行脚本。  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   有关详细信息，请参阅[CREATE AVAILABILITY GROUP (TRANSACT-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)。

1. 在辅助副本上加入可用性组。

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. 为可用性组创建数据库。 示例步骤使用名为的数据库`<TestDB>`。 如果你使用自动种子设定，设置数据和日志文件的相同路径。 

   运行该脚本之前，更新你的数据库的值。

      * 替换`<TestDB>`替换为你的数据库的名称。

      * 替换`<F:\Path>`你的数据库和日志文件的路径。 为数据库和日志文件使用相同的路径。 

      你还可以使用的默认路径。 

    若要创建你的数据库，运行脚本。 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. 进行完整备份的数据库。 

1. 如果你未使用自动种子设定，还原辅助副本 (Linux) 服务器上的数据库。 [从 Windows 的 SQL Server 数据库迁移到使用备份和还原 Linux](sql-server-linux-migrate-restore-database.md)。 还原数据库`WITH NORECOVERY`辅助副本上。 

1. 将数据库添加到可用性组。 更新的示例脚本。 替换`<TestDB>`替换为你的数据库的名称。 在主副本上，运行 SQL 查询，以将数据库添加到可用性组。

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. 验证数据库将辅助副本上获取填充。 

## <a name="fail-over-the-primary-replica"></a>故障转移的主副本

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

这篇文章评审创建跨平台可用性组中，以支持迁移或读取规模工作负荷的步骤。 它可以用于手动灾难恢复。 它还说明了如何故障转移可用性组。 跨平台可用性组使用群集类型`NONE`和不支持高可用性，因为没有任何群集工具跨-平台。 

## <a name="next-steps"></a>后续步骤

[Always On 可用性组概述](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[SQL Server 可用性 Linux 部署的基础知识](sql-server-linux-ha-basics.md)
