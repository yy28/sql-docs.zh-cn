---
title: master 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
caps.latest.revision: 46
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 88cbd58a75ff8b7ceaaf93843bb685cdcb8dc11b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124584"
---
# <a name="master-database"></a>master 数据库
  **master** 数据库记录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统的所有系统级信息。 这包括实例范围的元数据（例如登录帐户）、端点、链接服务器和系统配置设置。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，系统对象不再存储在 **master** 数据库中，而是存储在 [Resource 数据库](resource-database.md)中。 此外， **master** 数据库还记录了所有其他数据库的存在、数据库文件的位置以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的初始化信息。 因此，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] master **数据库不可用，则** 无法启动。  
  
## <a name="physical-properties-of-master"></a>master 数据库的物理属性  
 下表列出了 **master** 数据和日志文件的初始配置值。 对于不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这些文件的大小可能略有不同。  
  
|文件|逻辑名称|物理名称|文件增长|  
|----------|------------------|-------------------|-----------------|  
|主数据|master|master.mdf|以 10% 的速度自动增长到磁盘充满为止。|  
|日志|mastlog|mastlog.ldf|以 10% 的速度自动增长到最大 2 TB。|  
  
 有关如何移动 **master** 数据和日志文件的信息，请参阅 [移动系统数据库](system-databases.md)。  
  
### <a name="database-options"></a>数据库选项  
 下表列出了 **master** 数据库中每个数据库选项的默认值以及该选项是否可以修改。 若要查看这些选项的当前设置，请使用 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目录视图。  
  
|数据库选项|默认值|是否可修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|“否”|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|“否”|  
|AUTO_CREATE_STATISTICS|ON|是|  
|AUTO_SHRINK|OFF|“否”|  
|AUTO_UPDATE_STATISTICS|ON|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|“否”|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT|GLOBAL|是|  
|数据库可用性选项|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|“否”<br /><br /> 否<br /><br /> “否”|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|“否”|  
|ENCRYPTION|OFF|“否”|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|CHECKSUM|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|“否”|  
|RECOVERY|SIMPLE|是|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 选项|DISABLE_BROKER|“否”|  
|TRUSTWORTHY|OFF|是|  
  
 有关这些数据库选项的说明，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="restrictions"></a>限制  
 不能在 **master** 数据库中执行下列操作：  
  
-   添加文件或文件组。  
  
-   更改排序规则。 默认排序规则为服务器排序规则。  
  
-   更改数据库所有者。 **master** 的所有者是 **sa**。  
  
-   创建全文目录或全文索引。  
  
-   在数据库的系统表上创建触发器。  
  
-   删除数据库。  
  
-   从数据库中删除 **guest** 用户。  
  
-   启用变更数据捕获。  
  
-   参与数据库镜像。  
  
-   删除主文件组、主数据文件或日志文件。  
  
-   重命名数据库或主文件组。  
  
-   将数据库设置为 OFFLINE。  
  
-   将数据库或主文件组设置为 READ_ONLY。  
  
## <a name="recommendations"></a>建议  
 使用 **master** 数据库时，请考虑下列建议：  
  
-   始终有一个 **master** 数据库的当前备份可用。  
  
-   执行下列操作后，尽快备份 **master** 数据库：  
  
    -   创建、修改或删除任意数据库  
  
    -   更改服务器或数据库的配置值  
  
    -   修改或添加登录帐户  
  
-   不要在 **master**中创建用户对象。 否则，必须更频繁地备份 **master** 。  
  
-   不要针对 **master** 数据库将 TRUSTWORTHY 选项设置为 ON。  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>当 master 不可用时怎么办  
 如果 **master** 数据库不可用，则可以通过下列两种方式之一将该数据库返回到可用状态：  
  
-   从当前数据库备份还原 **master** 。  
  
     如果你可以启动服务器实例，则应该能够从完整数据库备份还原 **master** 。 有关详细信息，请参阅[还原 master 数据库 (Transact-SQL)](../backup-restore/restore-the-master-database-transact-sql.md)。  
  
-   完全重新生成 **master** 。  
  
     如果由于 **master** 严重损坏而无法启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则必须重新生成 **master**。 有关详细信息，请参阅 [重新生成系统数据库](rebuild-system-databases.md)。  
  
    > [!IMPORTANT]  
    >  重新生成 **master** 将重新生成所有系统数据库。  
  
## <a name="related-content"></a>相关内容  
 [重新生成系统数据库](rebuild-system-databases.md)  
  
 [系统数据库](system-databases.md)  
  
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [移动数据库文件](move-database-files.md)  
  
  
