---
title: Tempdb 数据库-并行数据仓库 |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63156959"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>并行数据仓库中的 tempdb 数据库
**tempdb**是用于存储用户数据库的本地临时表的 SQL Server PDW 系统数据库。 临时表通常用于提高查询性能。 例如，可以使用临时表来模块化脚本，并重复使用计算的数据。  
  
系统数据库的详细信息，请参阅[系统数据库](system-databases.md)。  
  
## <a name="Basics"></a>关键术语和概念  
*本地临时表*  
一个*本地临时表*使用表名称的前面的 # 前缀，并且是由本地用户会话创建的临时表。 每个会话只能为其自己的会话中访问本地临时表中的数据。  
  
每个会话可以在所有会话中查看本地临时表的元数据。 例如，所有会话可以都查看使用的所有本地临时表的元数据`SELECT * FROM tempdb.sys.tables`查询。  
  
全局临时表  
*全局临时表*的、 与 SQL Server 中支持 # # 语法中，不支持在此版本的 SQL Server PDW。  
  
pdwtempdb  
**pdwtempdb**是用于存储本地临时表的数据库。  
  
PDW 不实现通过使用 SQL Server 的临时表**tempdb**数据库。 相反，PDW 将其存储在名为 pdwtempdb 的数据库。 此数据库在每个计算节点上存在并且是通过 PDW 接口用户看不到。 在管理员控制台中，在存储页上，您将看到这些占中名为的 PDW 系统数据库**tempdb sql**。  
  
tempdb  
**tempdb**是 SQL Server tempdb 数据库。 它使用最小日志记录。 SQL Server 计算节点上使用 tempdb 来存储所需在执行 SQL Server 操作的过程中的临时表。  
  
SQL Server PDW 删除中的表**tempdb**时：  
  
-   执行 DROP TABLE 语句。  
  
-   会话已断开连接。 临时表仅为该会话将被删除。  
  
-   在设备处于关闭状态。  
  
-   控制节点具有群集故障转移。  
  
## <a name="general-remarks"></a>一般备注  
SQL Server PDW 执行临时表和永久表相同的操作，除非明确声明。 例如，本地临时表，就像永久表中的数据是分布式或在计算节点之间复制。  
  
## <a name="LimitationsRestrictions"></a>限制和局限  
限制和局限在 SQL Server PDW**tempdb**数据库。 您*不能：*  
  
-   创建开头的全局临时表 # #。  
  
-   执行备份或还原**tempdb**。  
  
-   修改权限**tempdb**与**授予**，**拒绝**，或者**撤消**语句。  
  
-   执行**DBCC SHRINKLOG**有关**tempdb**tempdb。  
  
-   在执行 DDL 操作**tempdb**。 有几个例外情况。 有关详细信息，请参阅本地临时表上的以下限制和局限的列表。  
  
限制和对本地临时表的限制。 您*不能：*  
  
-   重命名的临时表  
  
-   临时表上创建分区、 视图或非聚集索引。 **ALTER INDEX**可用于重新生成其中一个创建的表的聚集的索引。  
  
-   修改权限到临时表使用 GRANT、 DENY 或 REVOKE 语句。  
  
-   在临时表上运行数据库控制台命令。  
  
-   使用同一批中的两个或多个临时表相同的名称。 如果批处理中使用多个本地临时表，每个临时表都必须具有唯一的名称。 如果多个会话运行在同一个批处理并创建同一个本地临时表，SQL Server PDW 在内部将一个数字后缀追加到本地临时表名以维护每个本地临时表的唯一名称。  
  
> [!NOTE]  
> 您*可以*创建和更新临时表的统计信息。**ALTER INDEX**可用于重新生成聚集的索引。  
  
## <a name="permissions"></a>权限  
任何用户都可以在 tempdb 中创建临时对象。 用户只能访问自己的对象，除非他们获得更多的权限。 可以撤消对 tempdb 的连接权限以阻止用户使用 tempdb，但是不建议这样做，因为一些例行操作需要使用 tempdb。  
  
## <a name="RelatedTasks"></a>相关的任务  
  
|“任务”|Description|  
|---------|---------------|  
|将在创建表**tempdb**。|可以使用 CREATE TABLE 和 CREATE TABLE AS SELECT 语句创建一个用户的临时表。 有关详细信息，请参阅[CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)并[CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)。|  
|查看列表中的现有表**tempdb**。|`SELECT * FROM tempdb.sys.tables;`|  
|查看中的现有列的列表**tempdb**。|`SELECT * FROM tempdb.sys.columns;`|  
|查看中的现有对象的列表**tempdb**。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
