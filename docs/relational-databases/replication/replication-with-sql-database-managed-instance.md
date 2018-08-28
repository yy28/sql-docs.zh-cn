---
title: 使用 SQL 数据库托管实例进行复制 | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c0c104db9ce5bbd27fa1fb5f0e125ee940c48d28
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43092343"
---
# <a name="replication-with-sql-database-managed-instance"></a>使用 SQL 数据库托管实例进行复制

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Azure SQL 数据库托管实例（预览版）支持事务复制。 托管实例可以托管发布服务器、分发服务器和订阅服务器数据库。

## <a name="common-configurations"></a>常用配置

一般情况下，发布服务器和分发服务器必须同时位于云中或本地环境中。 支持使用以下配置：

- **发布服务器与本地分发服务器在托管实例上**

   ![Replication-with-azure-sql-db-single-managed-instance-publisher-distributor](./media/replication-with-sql-database-managed-instance/01-single-instance-asdbmi-pubdist.png)

   在一个托管实例上配置发布服务器和分发服务器数据库。

- **发布服务器与远程分发服务器在托管实例上**

   ![Replication-with-azure-sql-db-separate-managed-instances-publisher-distributor](./media/replication-with-sql-database-managed-instance/02-separate-instances-asdbmi-pubdist.png)

   在两个托管实例上配置发布服务器和分发服务器。 在这种配置中：

  - 两个托管实例位于同一 vNet 中。

  - 两个托管实例位于同一位置。

- **发布服务器和分发服务器在本地，订阅服务器在托管实例上**

   ![Replication-from-on-premises-to-azure-sql-db-subscriber](./media/replication-with-sql-database-managed-instance/03-azure-sql-db-subscriber.png)

   在这种配置中，Azure SQL 数据库是订阅服务器。 这种配置支持从本地迁移到 Azure。 在订阅服务器角色中，SQL 数据库不需要托管实例，但可以在从本地迁移到 Azure 过程中的一步使用 SQL 数据库托管实例。 若要详细了解 Azure SQL 数据库订阅服务器，请参阅[复制到 SQL 数据库](replication-to-sql-database.md)。

## <a name="requirements"></a>要求

Azure SQL 数据库发布服务器和分发服务器都要求：

- 使用 Azure SQL 数据库托管实例。

   >[!NOTE]
   >未配置托管实例的 Azure SQL 数据库只能是订阅服务器。

- 所有 SQL Server 实例都必须位于同一 vNet 上。

- 在复制参与者之间使用 SQL 身份验证进行连接。

- 共享 Azure 存储帐户，以用于复制工作目录。

## <a name="features"></a>功能

支持：

- 对本地实例和 Azure SQL 数据库托管实例混用事务复制和快照复制。

- 订阅服务器可以位于本地、Azure SQL 数据库或弹性池中。

- 单向或双向复制

## <a name="configure-publishing-and-distribution-example"></a>配置发布和分发示例

1. 在门户中，[创建 Azure SQL 数据库托管实例](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal)。

1. [创建 Azure 存储帐户](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#create-a-storage-account)，以用于工作目录。 请务必复制存储密钥。 请参阅[查看和复制存储访问密钥](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys)。

1. 创建发布服务器数据库。

   在下面的示例脚本中，将 `<Publishing_DB>` 替换为此数据库的名称。

1. 创建对分发服务器使用 SQL 身份验证的数据库用户。 请参阅[创建数据库用户](http://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial#creating-database-users)。 使用安全密码。

   在下面的示例脚本中，将 `<SQL_USER>` 和 `<PASSWORD>` 替换为此 SQL Server 帐户数据库用户名和密码。

1. [连接到 SQL 数据库托管实例](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ssms)。

1. 运行下面的查询，以添加分发服务器和分发数据库。

   ```sql
   USE [master]
   GO
   EXEC sp_adddistributor @distributor = @@ServerName;
   EXEC sp_adddistributiondb @database = N'distribution';
   ```

1. 若要将发布服务器配置为使用指定分发数据库，请更新并运行下面的查询。

   将 `<SQL_USER>` 和 `<PASSWORD>` 替换为 SQL Server 帐户名和密码。

   将 `\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>` 替换为存储帐户对应的值。 

   将 `<STORAGE_CONNECTION_STRING>` 替换为访问密钥对应的值。

   更新下面的查询后，运行它。 

   ```sql
   USE [master]
   EXEC sp_adddistpublisher @publisher = @@ServerName,
                @distribution_db = N'distribution',
                @security_mode = 0,
                @login = N'<SQL_USER>',
                @password = N'<PASSWORD>',
                @working_directory = N'\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>',
                @storage_connection_string = N'<STORAGE_CONNECTION_STRING>';
   GO
   ```

1. 配置发布服务器，以用于复制。 

    在下面的查询中，将 `<Publishing_DB>` 替换为发布服务器数据库的名称。

    将 `<Publication_Name>` 替换为发布名称。

    将 `<SQL_USER>` 和 `<PASSWORD>` 替换为 SQL Server 帐户名和密码。

    运行更新后的查询，以创建发布。

   ```sql
   USE [<Publishing_DB>]
   EXEC sp_replicationdboption @dbname = N'<Publishing_DB>',
                @optname = N'publish',
                @value = N'true';

   EXEC sp_addpublication @publication = N'<Publication_Name>',
                @status = N'active';

   EXEC sp_changelogreader_agent @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>';

   EXEC sp_addpublication_snapshot @publication = N'<Publication_Name>',
                @frequency_type = 1,
                @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>'
   ```

1. 添加项目、订阅和推送订阅代理。 

   若要添加这些对象，请更新以下脚本。

   将 `<Object_Name>` 替换为发布对象名称。

   将 `<Object_Schema>` 替换为源架构名称。 

   替换尖括号 `<>` 中的其他参数，与前面脚本中的值保持一致。 

   ```sql
   EXEC sp_addarticle @publication = N'<Publication_Name>',
                @type = N'logbased',
                @article = N'<Object_Name>',
                @source_object = N'<Object_Name>',
                @source_owner = N'<Object_Schema>'

   EXEC sp_addsubscription @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @destination_db = N'<Subscribing_DB>',
                @subscription_type = N'Push'

   EXEC sp_addpushsubscription_agent @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @subscriber_db = N'<Subscribing_DB>',
                @subscriber_security_mode = 0,
                @subscriber_login = N'<SQL_USER>',
                @subscriber_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>', 
                @job_password = N'<PASSWORD>'
   GO
   ```

## <a name="limitations"></a>限制

不支持以下功能：

- 可更新的订阅

- 活动异地复制

## <a name="see-also"></a>另请参阅

- [什么是托管实例（预览版）？](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
