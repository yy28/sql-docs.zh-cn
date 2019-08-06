---
title: Tempdb 数据库-并行数据仓库 |Microsoft Docs
description: 并行数据仓库中的 Tempdb 数据库。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6bdba302778224ab2615018d6c5dec0740328d93
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810937"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>并行数据仓库中的 tempdb 数据库
**tempdb**是一个 SQL Server PDW 系统数据库, 用于存储用户数据库的本地临时表。 临时表通常用于提高查询性能。 例如, 可以使用临时表模块化脚本, 并重复使用计算的数据。  
  
有关系统数据库的详细信息, 请参阅[系统数据库](system-databases.md)。  
  
## <a name="Basics"></a>关键术语和概念  
*本地临时表*  
*本地临时表*在表名称前使用 # 前缀, 并且是由本地用户会话创建的临时表。 每个会话仅可访问本地临时表中的数据以供其自己的会话使用。  
  
每个会话都可以在所有会话中查看本地临时表的元数据。 例如, 所有会话都可以通过`SELECT * FROM tempdb.sys.tables`查询查看所有本地临时表的元数据。  
  
全局临时表  
此版本的 SQL Server PDW 不支持在具有 # # 语法的 SQL Server 中支持的*全局临时表*。  
  
pdwtempdb  
**pdwtempdb**是存储本地临时表的数据库。  
  
PDW 不使用 SQL Server**tempdb**数据库来实现临时表。 PDW 会将它们存储在名为 pdwtempdb 的数据库中。 此数据库存在于每个计算节点上, 并通过 PDW 接口对用户不可见。 在管理控制台中的 "存储" 页上, 你将在名为 " **tempdb-sql**" 的 PDW 系统数据库中看到这些项。  
  
tempdb  
**tempdb**是 SQL Server tempdb 数据库。 它使用最小日志记录。 SQL Server 使用计算节点上的 tempdb 来存储在执行 SQL Server 操作过程中所需的临时表。  
  
当以下情况时, SQL Server PDW 从**tempdb**中删除表:  
  
-   执行 DROP TABLE 语句。  
  
-   会话已断开连接。 仅删除会话的临时表。  
  
-   设备已关闭。  
  
-   控制节点具有群集故障转移。  
  
## <a name="general-remarks"></a>一般备注  
除非明确声明, 否则 SQL Server PDW 对临时表和永久表执行相同的操作。 例如, 本地临时表中的数据与永久表一样, 都是在计算节点之间进行分布或复制。  
  
## <a name="LimitationsRestrictions"></a>限制和局限  
SQL Server PDW**tempdb**数据库的限制和限制。 *不能:*  
  
-   创建一个以 # # 开头的全局临时表。  
  
-   执行**tempdb**的备份或还原。  
  
-   用**GRANT**、 **DENY**或**REVOKE**语句修改对**tempdb**的权限。  
  
-   为**tempdb**Tempdb 执行**DBCC SHRINKLOG** 。  
  
-   对**tempdb**执行 DDL 操作。 这也有一些例外。 有关详细信息, 请参阅下面的限制和对本地临时表的限制列表。  
  
对本地临时表的限制和限制。 *不能:*  
  
-   重命名临时表  
  
-   在临时表上创建分区、视图或非聚集索引。 **ALTER index**可用于为使用一个创建的表重新生成聚集索引。  
  
-   用 GRANT、DENY 或 REVOKE 语句修改临时表的权限。  
  
-   在临时表上运行数据库控制台命令。  
  
-   在同一批处理中为两个或多个临时表使用相同的名称。 如果批处理中使用多个本地临时表，每个临时表都必须具有唯一的名称。 如果多个会话运行相同的批处理并创建相同的本地临时表, SQL Server PDW 会在内部向本地临时表名追加一个数字后缀, 以维护每个本地临时表的唯一名称。  
  
> [!NOTE]  
> *可以*在临时表上创建和更新统计信息。**ALTER index**可用于重新生成聚集索引。  
  
## <a name="permissions"></a>权限  
任何用户都可以在 tempdb 中创建临时对象。 用户只能访问自己的对象，除非他们获得更多的权限。 可以撤消对 tempdb 的连接权限以阻止用户使用 tempdb，但是不建议这样做，因为一些例行操作需要使用 tempdb。  
  
## <a name="RelatedTasks"></a>相关任务  
  
|“任务”|描述|  
|---------|---------------|  
|在**tempdb**中创建表。|您可以使用 "CREATE TABLE" 和 "CREATE TABLE" 作为 SELECT 语句来创建用户临时表。 有关详细信息, 请参阅[CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)和[CREATE TABLE 选择](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)。|  
|查看**tempdb**中现有表的列表。|`SELECT * FROM tempdb.sys.tables;`|  
|查看**tempdb**中现有列的列表。|`SELECT * FROM tempdb.sys.columns;`|  
|查看**tempdb**中现有对象的列表。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
