---
title: tempdb 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b1265d3ef58f6ef0946937b15411b0cb79a3c20
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59240705"
---
# <a name="tempdb-database"></a>tempdb 数据库
  **tempdb** 系统数据库是一个全局资源，可供连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的所有用户使用，并可用于保存下列各项：  
  
-   显式创建的临时用户对象，例如全局或局部临时表、临时存储过程、表变量或游标。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]创建的内部对象，例如，用于存储假脱机或排序的中间结果的工作表。  
  
-   由使用已提交读（使用行版本控制隔离或快照隔离事务）的数据库中数据修改事务生成的行版本。  
  
-   由数据修改事务为实现联机索引操作、多个活动的结果集 (MARS) 以及 AFTER 触发器等功能而生成的行版本。  
  
 **tempdb** 中的操作是最小日志记录操作。 这将使事务产生回滚。 每次启动**时都会重新创建** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，从而在系统启动时总是具有一个干净的数据库副本。 在断开联接时会自动删除临时表和存储过程，并且在系统关闭后没有活动连接。 因此 **tempdb** 中不会有什么内容从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话保存到另一个会话。 不允许对 **tempdb**进行备份和还原操作。  
  
## <a name="physical-properties-of-tempdb"></a>tempdb 的物理属性  
 下表列出了 **tempdb** 数据和日志文件的初始配置值。 对于不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这些文件的大小可能略有不同。  
  
|文件|逻辑名称|物理名称|文件增长|  
|----------|------------------|-------------------|-----------------|  
|主数据|tempdev|tempdb.mdf|按 10% 自动增长，直到磁盘已满|  
|日志|templog|templog.ldf|以 10% 的速度自动增长到最大 2 TB|  
  
 大小**tempdb**可能会影响系统的性能。 例如，如果**tempdb**大小太小，可能是系统处理，而不使用自动增长的数据库以支持工作负荷要求每次启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以通过增加的大小来避免此开销**tempdb**。  
  
## <a name="performance-improvements-in-tempdb"></a>tempdb 的性能提高  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中， **tempdb** 性能以下列方式进行提高：  
  
-   可能缓存临时表和表变量。 缓存允许删除和创建临时对象的操作非常快速地执行，并减少页分配的争用问题。  
  
-   分配页闩锁协议得到改善。 从而减少使用的 UP（更新）闩锁数。  
  
-   减少了 **tempdb** 的日志开销。 从而减少了 **tempdb** 日志文件上的磁盘 I/O 带宽消耗。  
  
-   分配混合的页中的算法**tempdb**得到了改进。  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>移动 tempdb 数据和日志文件  
 若要移动 **tempdb** 数据和日志文件，请参阅 [移动系统数据库](system-databases.md)。  
  
### <a name="database-options"></a>数据库选项  
 下表列出了 **tempdb** 数据库中每个数据库选项的默认值，以及是否可以修改该选项。 若要查看这些选项的当前设置，请使用 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目录视图。  
  
|数据库选项|默认值|是否可修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|是|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|否|  
|AUTO_CREATE_STATISTICS|ON|是|  
|AUTO_SHRINK|OFF|否|  
|AUTO_UPDATE_STATISTICS|ON|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT|GLOBAL|是|  
|数据库可用性选项|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|对于新安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，为 CHECKSUM。<br /><br /> 对于升级的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，为 NONE。|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|否|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 选项|ENABLE_BROKER|是|  
|TRUSTWORTHY|OFF|否|  
  
 有关这些数据库选项的说明，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
## <a name="restrictions"></a>限制  
 不能对 **tempdb** 数据库执行以下操作：  
  
-   添加文件组。  
  
-   备份或还原数据库。  
  
-   更改排序规则。 默认排序规则为服务器排序规则。  
  
-   更改数据库所有者。 **tempdb** 的所有者是 **sa**。  
  
-   创建数据库快照。  
  
-   删除数据库。  
  
-   从数据库中删除 **guest** 用户。  
  
-   启用变更数据捕获。  
  
-   参与数据库镜像。  
  
-   删除主文件组、主数据文件或日志文件。  
  
-   重命名数据库或主文件组。  
  
-   运行 DBCC CHECKALLOC。  
  
-   运行 DBCC CHECKCATALOG。  
  
-   将数据库设置为 OFFLINE。  
  
-   将数据库或主文件组设置为 READ_ONLY。  
  
## <a name="permissions"></a>权限  
 任何用户都可以在 tempdb 中创建临时对象。 用户只能访问自己的对象，除非他们获得更多的权限。 可以撤消对 tempdb 的连接权限以阻止用户使用 tempdb，但是不建议这样做，因为一些例行操作需要使用 tempdb。  
  
## <a name="related-content"></a>相关内容  
 [用于索引的 SORT_IN_TEMPDB 选项](../indexes/indexes.md)  
  
 [系统数据库](system-databases.md)  
  
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [移动数据库文件](move-database-files.md)  
  
## <a name="see-also"></a>请参阅  
 [在 SQL Server 2005 中使用 tempdb](https://chresandro.wordpress.com/2014/09/29/working-with-tempdb-in-sql-server-2005/)  
  
  
