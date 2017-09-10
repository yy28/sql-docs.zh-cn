---
title: "DBCC UPDATEUSAGE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
caps.latest.revision: 56
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e99240896bb1192a742ad2b614080e5325acc1f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

报告目录视图中的页数和行数错误并进行更正。 这些错误可能导致 sp_spaceused 系统存储过程返回不正确的空间使用报告。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>参数  
*database_name* | *database_id* | 0  
要对其空间使用统计信息进行报告和更正的数据库的名称或 ID。 如果指定 0，则使用当前数据库。 数据库名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
*table_name* | *针对 table_id 所* | *view_name* | *view_id*  
要对其空间使用统计信息进行报告和更正的表或索引视图的名称或 ID。 表和视图的名称必须符合有关标识符的规则。  
  
*index_id* | *index_name*  
要使用的索引的 ID 或名称。 如果未指定，语句将对指定的表或视图的所有索引进行处理。  
  
替换为  
允许指定选项。  
  
NO_INFOMSGS  
取消显示所有信息性消息。  
  
COUNT_ROWS  
指定使用表或视图中的行数的当前计数更新 row count 列。  
  
## <a name="remarks"></a>注释  
DBCC UPDATEUSAGE 将针对表或索引中的每个分区更正行、已用页、保留页、叶级页和数据页的计数。 如果系统表中没有错误，则 DBCC UPDATEUSAGE 不返回数据。 如果发现错误，并对其进行了更正，同时没有使用 WITH NO_INFOMSGS，DBCC UPDATEUSAGE 将返回系统表中更新的行和列。
  
DBCC CHECKDB 已得到增强，可以检测页计数或行计数变为负值的情况。 检测到上述问题后，DBCC CHECKDB 的输出会包含一个警告和一个建议，建议运行 DBCC UPDATEUSAGE 解决该问题。
  
## <a name="best-practices"></a>最佳实践  
我们的建议如下：
-   请不要定期运行 DBCC UPDATEUSAGE。 由于对大型表或数据库运行 DBCC UPDATEUSAGE 会耗费一定的时间，因此不应使用此语句，除非您怀疑 sp_spaceused 返回了不正确的值。
-   只有数据库的 CREATE、ALTER 或 DROP 语句等数据定义语言 (DDL) 经常受到修改时，才应考虑定期运行 DBCC UPDATEUSAGE（例如，每周运行一次）。  
  
## <a name="result-sets"></a>结果集  
DBCC UPDATEUSAGE 返回（值可能有所不同）：
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。
  
## <a name="examples"></a>示例  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. 为当前数据库中的所有对象更新页计数或行计数，或同时更新这两者  
下面的示例将数据库名称指定为 `0`，且 `DBCC UPDATEUSAGE` 报告当前数据库的已更新页计数或行计数信息。
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. 为 AdventureWorks 更新页计数或行计数，或同时更新这两者，并禁止显示信息性消息。  
下面的示例将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 指定为数据库名称，并禁止显示所有信息性消息。
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. 为 Employee 表更新页计数或行计数，或同时更新这两者  
以下示例将报告更新的页或行计数信息`Employee`表中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. 为表中的特定索引更新页计数或行计数，或同时更新这两者  
 下面的示例将 `IX_Employee_ManagerID` 指定为索引名称。  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[更新统计信息 (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)
  
  

