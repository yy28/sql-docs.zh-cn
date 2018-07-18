---
title: Tempdb 数据库-并行数据仓库 |Microsoft 文档
description: 并行数据仓库中的 Tempdb 数据库。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538857"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>并行数据仓库中的 tempdb 数据库
**tempdb**是存储的用户数据库的本地临时表的 SQL Server PDW 系统数据库。 临时表通常用于提高查询性能。 例如，你可以使用临时表来将模块化脚本，并重复使用计算的数据。  
  
有关系统数据库的详细信息，请参阅[系统数据库](system-databases.md)。  
  
## <a name="Basics"></a>关键术语和概念  
*本地临时表*  
A*本地临时表*使用表名称前面的 # 前缀，并且是临时表创建的本地用户会话。 每个会话只能为其自己的会话访问本地临时表中的数据。  
  
每个会话可以在所有会话中查看本地临时表的元数据。 例如，所有会话可以都查看使用的所有本地临时表的元数据`SELECT * FROM tempdb.sys.tables`查询。  
  
全局临时表  
*全局临时表*，支持使用 SQL Server 中 # # 语法，此版本的 SQL Server PDW 中不支持。  
  
pdwtempdb  
**pdwtempdb**是存储本地临时表的数据库。  
  
PDW 不实施临时表，使用 SQL Server**tempdb**数据库。 相反，PDW 将其存储在名为 pdwtempdb 的数据库。 此数据库每个计算节点上存在，并对通过 PDW 接口用户不可见。 在管理员控制台中，在存储页上，你将看到这些占为一个名为 PDW 系统数据库中**tempdb sql**。  
  
tempdb  
**tempdb**是 SQL Server tempdb 数据库。 它使用最小日志记录。 SQL Server 在计算节点上使用 tempdb 来存储它在执行 SQL Server 操作的过程中需要的临时表。  
  
SQL Server PDW 删除来自表**tempdb**时：  
  
-   执行 DROP TABLE 语句。  
  
-   会话已断开连接。 只有会话临时表被删除。  
  
-   设备已关闭。  
  
-   控制节点具有群集故障转移。  
  
## <a name="general-remarks"></a>一般备注  
SQL Server PDW 执行临时表和永久表上的相同操作，除非有其他显式声明。 例如，本地临时表，就像永久表中的数据是分布式或在计算节点之间复制。  
  
## <a name="LimitationsRestrictions"></a>限制和局限  
限制和局限在 SQL Server PDW 上的**tempdb**数据库。 你*不能：*  
  
-   创建一个开头的全局临时表 # #。  
  
-   执行备份或还原**tempdb**。  
  
-   修改权限**tempdb**与**授予**，**拒绝**，或**撤消**语句。  
  
-   执行**DBCC SHRINKLOG**为**tempdb**tempdb。  
  
-   执行 DDL 操作**tempdb**。 有几个例外。 有关详细信息，请参阅局部临时表上的以下限制和局限的列表。  
  
限制和对本地临时表的限制。 你*不能：*  
  
-   重命名临时表  
  
-   创建临时表分区、 视图或非聚集索引。 **ALTER INDEX**可用来重新生成聚集的索引具有一个为创建表。  
  
-   修改临时表权限使用 GRANT、 DENY 或 REVOKE 语句。  
  
-   临时表上运行数据库控制台命令。  
  
-   使用相同的批中的两个或多个临时表的相同名称。 如果批处理中使用多个本地临时表，每个临时表都必须具有唯一的名称。 如果多个会话运行同一个批处理和创建同一个本地临时表，则 SQL Server PDW 内部将数字后缀追加到本地临时表名称，以维护每个本地临时表的唯一名称。  
  
> [!NOTE]  
> 你*可以*创建和更新临时表的统计信息。**ALTER INDEX**可用来重新生成聚集的索引。  
  
## <a name="permissions"></a>权限  
任何用户都可以在 tempdb 中创建临时对象。 用户只能访问自己的对象，除非他们获得更多的权限。 可以撤消对 tempdb 的连接权限以阻止用户使用 tempdb，但是不建议这样做，因为一些例行操作需要使用 tempdb。  
  
## <a name="RelatedTasks"></a>相关的任务  
  
|“任务”|Description|  
|---------|---------------|  
|创建一个表**tempdb**。|你可以使用 CREATE TABLE 和 CREATE TABLE AS SELECT 语句创建用户的临时表。 有关详细信息，请参阅[CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)和[CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)。|  
|查看列表中的现有表**tempdb**。|`SELECT * FROM tempdb.sys.tables;`|  
|查看中的现有列的列表**tempdb**。|`SELECT * FROM tempdb.sys.columns;`|  
|查看中的现有对象的列表**tempdb**。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
