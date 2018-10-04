---
title: sp_fulltext_column (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_column_TSQL
- sp_fulltext_column
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_column
ms.assetid: a84cc45d-1b50-44af-85df-2ea033b8a6a9
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0173c89273d208824bd945fa7c073ddd7940067e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615001"
---
# <a name="spfulltextcolumn-transact-sql"></a>sp_fulltext_column (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  指定表的某个特定列是否参与全文索引。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_fulltext_column [ @tabname= ] 'qualified_table_name' ,   
     [ @colname= ] 'column_name' ,   
     [ @action= ] 'action'   
     [ , [ @language= ] 'language_term' ]   
     [ , [ @type_colname= ] 'type_column_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@tabname=** ] **'***qualified_table_name***'**  
 由一部分或两部分组成的表的名称。 表必须在当前数据库中。 表必须具有全文索引。 *qualified_table_name*是**nvarchar(517)**，无默认值。  
  
 [ **@colname=** ] **'***column_name***'**  
 中的列的名称*qualified_table_name*。 该列必须为字符**varbinary （max)** 或**映像**列且不能为计算的列。 *column_name*是**sysname**，无默认值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以创建全文索引的文本数据存储中的列**varbinary （max)** 或**映像**数据类型。 不对图像和图片进行索引。  
  
 [  **@action=** ] **'***操作*****  
 要执行的操作。 *操作*是**varchar （20)**，无默认值可以是以下值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**add**|将添加*column_name*的*qualified_table_name*到表的非活动的全文索引。 此操作可启用列以进行全文索引。|  
|**删除**|移除*column_name*的*qualified_table_name*从表的非活动的全文索引。|  
  
 [ **@language=** ] **'***language_term***'**  
 存储在列中的数据的语言。 有关列表中包括的语言[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。  
  
> [!NOTE]  
>  如果列包含的数据使用了多种语言或不支持的语言，则使用“非特定语言”。 默认值通过配置选项“默认全文语言”指定。  
  
 [ **@type_colname =** ] **'***type_column_name***'**  
 中的列的名称*qualified_table_name*保存的文档类型的*column_name*。 此列必须是**char**， **nchar**， **varchar**，或者**nvarchar**。 数据类型时才使用*column_name*属于类型**varbinary （max)** 或**图像**。 *type_column_name*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 如果全文索引处于活动状态，则将停止所有正在进行的填充。 而且，如果一个具有活动全文索引的表启用了更改跟踪，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会确保索引是当前索引。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止对表的所有当前填充，删除现有索引，并启动新填充。  
  
 如果启用了更改跟踪，并且需要在保留索引的同时从全文索引中添加或删除列，则应停用表并添加或删除所需的列。 这些操作将冻结索引。 如果以后可以开始进行填充了，则可以重新激活表。  
  
## <a name="permissions"></a>Permissions  
 用户必须是属于**db_ddladmin**固定数据库角色的成员或**db_owner**固定数据库角色或表的所有者。  
  
## <a name="examples"></a>示例  
 以下示例将 `DocumentSummary` 表的 `Document` 列添加到表的全文索引中。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_column 'Production.Document', DocumentSummary, 'add';  
GO  
```  
  
 以下示例假定已对名为 `spanishTbl` 的表创建了一个全文索引。 若要将 `spanishCol` 列添加到全文索引，可执行以下存储过程：  
  
```  
EXEC sp_fulltext_column 'spanishTbl', 'spanishCol', 'add', 0xC0A;  
GO  
```  
  
 运行此查询时：  
  
```  
SELECT *   
FROM spanishTbl   
WHERE CONTAINS(spanishCol, 'formsof(inflectional, trabajar)')  
```  
  
 结果集将包括内含不同形态的 `trabajar` 一词的行，如 `trabajo`、`trabajamos` 和 `trabajan`。  
  
> [!NOTE]  
>  在单个全文查询函数子句中列出的所有列都必须使用相同的语言。  
  
## <a name="see-also"></a>请参阅  
 [OBJECTPROPERTY (Transact-SQL)](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [sp_help_fulltext_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文搜索和语义搜索存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
