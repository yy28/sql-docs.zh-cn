---
title: "sp_help_fulltext_tables (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 587fb2495e065d00a9031c198704af6ede6e80d5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpfulltexttables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回为全文索引注册的表的列表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用**sys.fulltext_indexes**改用目录视图。 有关详细信息，请参阅[sys.fulltext_indexes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@fulltext_catalog_name=**] *fulltext_catalog_name*  
 全文目录名称。 *fulltext_catalog_name*是**sysname**，默认值为 NULL。 如果*fulltext_catalog_name*省略或为 NULL，返回所有与数据库关联的全文索引的表。 如果*fulltext_catalog_name*指定，但*table_name*省略或为 NULL，与此目录相关联的每个全文索引表检索的全文索引信息。 如果这两个*fulltext_catalog_name*和*table_name*指定，如果返回一行*table_name*与关联*fulltext_catalog_name*;否则，将引发错误。  
  
 [  **@table_name=**] *table_name*  
 请求全文元数据的一段或两段表的名称。 *table_name*是**nvarchar(517)**，默认值为 NULL。 如果仅*table_name*指定，则仅与相关行*table_name*返回。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|表所有者。 这是创建该表的数据库用户的名称。|  
|**TABLE_NAME**|**sysname**|表名。|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|对于指定为唯一键列的列施加 UNIQUE 约束的索引。|  
|**FULLTEXT_KEY_COLID**|**int**|以 FULLTEXT_KEY_NAME 标识的唯一索引的列 ID。|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|指定该表中为全文索引标记的列是否适于查询：<br /><br /> 0 = 非活动<br /><br /> 1 = 活动|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|全文索引数据所在的全文目录。|  
  
## <a name="permissions"></a>Permissions  
 执行权限默认授予的成员**公共**角色。  
  
## <a name="examples"></a>示例  
 以下示例返回与 `Cat_Desc` 全文目录相关联的全文索引表的名称。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [INDEXPROPERTY (Transact-SQL)](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY (Transact-SQL)](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
