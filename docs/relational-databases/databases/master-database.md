---
title: master 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ef7392b4e41271bacd91b5e1a9244bbfe1c1139
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558634"
---
# <a name="master-database"></a>master 数据库
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **master** 数据库记录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统的所有系统级信息。 这包括实例范围的元数据（例如登录帐户）、端点、链接服务器和系统配置设置。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，系统对象不再存储在 **master** 数据库中，而是存储在 [Resource 数据库](../../relational-databases/databases/resource-database.md)中。 此外， **master** 数据库还记录了所有其他数据库的存在、数据库文件的位置以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的初始化信息。 因此，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] master **数据库不可用，则** 无法启动。  

> [!IMPORTANT]
> 对于 Azure SQL 数据库逻辑服务器，仅 master 数据库和 tempdb 数据库适用。 有关逻辑服务器和逻辑 master 数据库的相关概念，请参阅[什么是 Azure SQL 逻辑服务器？](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-logical-server)。 有关 Azure SQL 数据库上下文中关于 tempdb 的讨论，请参阅 [Azure SQL 数据库中的 tempdb 数据库](tempdb-database.md#tempdb-database-in-sql-database)。 对于 Azure SQL 数据库托管实例，所有系统数据库都适用。 若要详细了解 Azure SQL 数据库托管实例，请参阅[什么是托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
  
## <a name="physical-properties-of-master"></a>master 数据库的物理属性  
下表列出了 SQL Server 和 Azure SQL 数据库托管实例的 master 数据和日志文件的初始配置值。 对于不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这些文件的大小可能略有不同。  
  
|文件|逻辑名称|物理名称|文件增长|  
|----------|------------------|-------------------|-----------------|  
|主数据|master|master.mdf|以 10% 的速度自动增长到磁盘充满为止。|  
|日志|mastlog|mastlog.ldf|以 10% 的速度自动增长到最大 2 TB。|  
  
有关如何移动 **master** 数据和日志文件的信息，请参阅 [移动系统数据库](../../relational-databases/databases/move-system-databases.md)。  

> [!IMPORTANT]
> 对于 Azure SQL 数据库逻辑服务器，用户无法控制 master数据库的大小。
  
### <a name="database-options"></a>数据库选项  
下表列出了 SQL Server 和 Azure SQL 数据库托管实例的 master 数据库中每个数据库选项的默认值，以及该选项是否可以修改。 若要查看这些选项的当前设置，请使用 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目录视图。  
  
> [!IMPORTANT]
> 对于 Azure SQL 数据库逻辑服务器，用户无法控制这些数据库选项。

|数据库选项|默认值|是否可修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|否|  
|ANSI_NULL_DEFAULT|OFF|用户帐户控制|  
|ANSI_NULLS|OFF|用户帐户控制|  
|ANSI_PADDING|OFF|用户帐户控制|  
|ANSI_WARNINGS|OFF|用户帐户控制|  
|ARITHABORT|OFF|用户帐户控制|  
|AUTO_CLOSE|OFF|否|  
|AUTO_CREATE_STATISTICS|ON|用户帐户控制|  
|AUTO_SHRINK|OFF|否|  
|AUTO_UPDATE_STATISTICS|ON|用户帐户控制|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|用户帐户控制|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|用户帐户控制|  
|CURSOR_CLOSE_ON_COMMIT|OFF|用户帐户控制|  
|CURSOR_DEFAULT|GLOBAL|用户帐户控制|  
|数据库可用性选项|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|用户帐户控制|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|MIXED_PAGE_ALLOCATION|ON|否|  
|NUMERIC_ROUNDABORT|OFF|用户帐户控制|  
|PAGE_VERIFY|CHECKSUM|用户帐户控制|  
|PARAMETERIZATION|SIMPLE|用户帐户控制|  
|QUOTED_IDENTIFIER|OFF|用户帐户控制|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|用户帐户控制|  
|RECURSIVE_TRIGGERS|OFF|用户帐户控制|  
|Service Broker 选项|DISABLE_BROKER|否|  
|TRUSTWORTHY|OFF|用户帐户控制|  
  
有关这些数据库选项的说明，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="restrictions"></a>限制  
不能在 **master** 数据库中执行下列操作：  
  
- 添加文件或文件组。  
- 更改排序规则。 默认排序规则为服务器排序规则。  
- 更改数据库所有者。 **master** 的所有者是 **sa**。  
- 创建全文目录或全文索引。  
- 在数据库的系统表上创建触发器。  
- 删除数据库。  
- 从数据库中删除 **guest** 用户。  
- 启用变更数据捕获。  
- 参与数据库镜像。  
- 删除主文件组、主数据文件或日志文件。  
- 重命名数据库或主文件组。  
- 将数据库设置为 OFFLINE。  
- 将数据库或主文件组设置为 READ_ONLY。  
  
## <a name="recommendations"></a>建议  
使用 **master** 数据库时，请考虑下列建议：  
  
- 始终有一个 **master** 数据库的当前备份可用。  
- 执行下列操作后，尽快备份 **master** 数据库：  
  
  - 创建、修改或删除任意数据库  
  - 更改服务器或数据库的配置值  
  - 修改或添加登录帐户  
  
- 不要在 **master**中创建用户对象。 否则，必须更频繁地备份 **master** 。  
- 不要针对 **master** 数据库将 TRUSTWORTHY 选项设置为 ON。  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>当 master 不可用时怎么办  
 如果 **master** 数据库不可用，则可以通过下列两种方式之一将该数据库返回到可用状态：  
  
- 从当前数据库备份还原 **master** 。  
  
  如果你可以启动服务器实例，则应该能够从完整数据库备份还原 **master** 。 有关详细信息，请参阅[还原 master 数据库 (Transact-SQL)](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)。  
  
- 完全重新生成 **master** 。  
  
  如果由于 **master** 严重损坏而无法启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则必须重新生成 **master**。 有关详细信息，请参阅 [重新生成系统数据库](../../relational-databases/databases/rebuild-system-databases.md)。  
  
  > [!IMPORTANT]  
  >  重新生成 **master** 将重新生成所有系统数据库。  
  
## <a name="related-content"></a>相关内容  
- [重新生成系统数据库](../../relational-databases/databases/rebuild-system-databases.md)  
- [系统数据库](../../relational-databases/databases/system-databases.md)  
- [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [移动数据库文件](../../relational-databases/databases/move-database-files.md)  
