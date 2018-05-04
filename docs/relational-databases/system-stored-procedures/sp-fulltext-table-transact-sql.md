---
title: sp_fulltext_table (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a8daa2b463054d8dd33db156f85190223ab7a2e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spfulltexttable-transact-sql"></a>sp_fulltext_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  标记或取消标记要编制全文索引的表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md)， [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)，和[DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_fulltext_table   
   [ @tabname= ] 'qualified_table_name'           
   , [ @action= ] 'action'   
   [   
   , [ @ftcat= ] 'fulltext_catalog_name'           
   , [ @keyname= ] 'unique_index_name'   
   ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@tabname=**] **'***qualified_table_name***'**  
 由一部分或两部分组成的表的名称。 表必须在当前数据库中。 *qualified_table_name*是**nvarchar(517)**，无默认值。  
  
 [  **@action=**] *****操作*****  
 要执行的操作。 *操作*是**nvarchar(50)**，无默认值，并且可为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**创建**|创建引用的表的全文索引的元数据*qualified_table_name* ，并指定此表的全文索引数据应驻留在*fulltext_catalog_name*。 此操作还指定使用*unique_index_name*作为全文键列。 这个唯一的索引必须已经存在，并且必须已在表的某个列上定义。<br /><br /> 完成了全文目录填充后，才能对该表执行全文检索。|  
|**Drop**|将元数据删除的全文索引上*qualified_table_name*。 如果全文索引是活动的，则将自动停用该全文索引，然后将其删除。 在删除全文索引之前，不必删除列。|  
|**Activate**|激活的收集到的全文索引数据的能力*qualified_table_name*之后它已被停用。 在激活全文索引之前，应该至少有一列参与了全文索引。<br /><br /> 只要添加了第一个要编制索引的列，便会自动激活全文索引（进行填充）。 如果从索引中删除最后一个列，该索引便成为非活动索引。 如果启用了更改跟踪，则激活非活动索引时将启动一个新填充。<br /><br /> 请注意，这不会实际填充的全文索引，但只需表中的全文目录中注册的文件系统以便各行从*qualified_table_name*可以在下一步的全文索引中检索填充。|  
|**停用**|停用的全文索引*qualified_table_name*以便不再可用于收集的全文索引数据*qualified_table_name*。 全文索引元数据依然保留，该表可以被重新激活。<br /><br /> 如果启用了更改跟踪，停用一个活动索引将冻结索引的状态：停止正在进行的所有填充，不再向索引传播更改。|  
|**start_change_tracking**|启动全文索引的增量填充。 如果表没有时间戳，则启动全文索引的完全填充。 开始跟踪对表所做的更改。<br /><br /> 全文更改跟踪不会跟踪任何对全文索引列的类型执行的 WRITETEXT 或 UPDATETEXT 操作**映像**，**文本**，或**ntext**。|  
|**stop_change_tracking**|停止对表更改的跟踪。|  
|**update_index**|将当前的一组跟踪的更改传播给全文索引。|  
|**start_background_updateindex**|一旦发生更改，就启动将被跟踪的更改传播给全文索引。|  
|**stop_background_updateindex**|一旦发生更改，就停止将被跟踪的更改传播给全文索引。|  
|**start_full**|启动表的全文索引的完全填充。|  
|**start_incremental**|启动表的全文索引的增量填充。|  
|**停止**|停止完全填充或增量填充。|  
  
 [ **@ftcat=**] **'***fulltext_catalog_name***'**  
 是的有效，现有的全文目录名称**创建**操作。 对于其他所有操作，此参数必须为 NULL。 *fulltext_catalog_name*是**sysname**，默认值为 NULL。  
  
 [ **@keyname=**] **'***unique_index_name***'**  
 位于有效的单列的键、 唯一主键索引*qualified_table_name*为**创建**操作。 对于其他所有操作，此参数必须为 NULL。 *unique_index_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 为特定表的全文索引停用后，现有的全文索引将保持原样直到下一步的完全填充;但是，此索引因为不用于[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]阻止已停用表的查询。  
  
 如果重新激活该表，但不重新填充索引，则仍可使用旧索引对剩余的启用了全文索引的非新列进行查询。 在指定了完全全文列搜索的查询中，将匹配已删除的列中的数据。  
  
 表后已定义的全文索引，切换全文唯一键列从一个数据类型到另一个，通过更改该列的数据类型或某一列中的全文唯一键更改到另一个，而无需重新执行完全填充可能会导致故障发生期间的后续查询并返回错误消息:"转换为类型*data_type*失败的全文搜索的键值*key_value*。" 若要防止此情况，请删除此表使用的全文索引定义**删除**操作**sp_fulltext_table**和对其使用重新定义**sp_fulltext_table**和**sp_fulltext_column**。  
  
 必须将全文键列定义为 900 字节或更少。 考虑到性能原因，建议尽量使用较小的键列。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定服务器角色、 **db_owner**和**db_ddladmin**引用上使用的权限的全文目录可以固定数据库角色或用户执行**sp_fulltext_table**。  
  
## <a name="examples"></a>示例  
  
### <a name="a-enabling-a-table-for-full-text-indexing"></a>A. 启用要进行全文索引的表  
 以下示例将为 `Document` 数据库的 `AdventureWorks` 表创建全文索引元数据。 `Cat_Desc` 是一个全文目录。 `PK_Document_DocumentID` 是针对 `Document` 的唯一单列索引。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'create', 'Cat_Desc', 'PK_Document_DocumentID';  
--Add some columns  
EXEC sp_fulltext_column 'Production.Document','DocumentSummary','add';  
-- Activate the full-text index  
EXEC sp_fulltext_table 'Production.Document','activate';  
GO  
```  
  
### <a name="b-activating-and-propagating-track-changes"></a>B. 激活并传播跟踪更改  
 下例将在更改发生时激活跟踪更改并开始将跟踪的更改传播给全文索引。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'Start_change_tracking';  
EXEC sp_fulltext_table 'Production.Document', 'Start_background_updateindex';  
GO  
```  
  
### <a name="c-removing-a-full-text-index"></a>C. 删除全文索引  
 以下示例将删除 `Document` 数据库的 `AdventureWorks` 表的全文索引元数据。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'drop';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [INDEXPROPERTY (Transact-SQL)](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY (Transact-SQL)](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文搜索和语义搜索存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
