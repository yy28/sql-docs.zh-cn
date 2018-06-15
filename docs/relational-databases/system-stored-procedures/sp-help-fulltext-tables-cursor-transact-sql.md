---
title: sp_help_fulltext_tables_cursor (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0e188636c3152c6ba7e1daa941f01c5766ad4320
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33254869"
---
# <a name="sphelpfulltexttablescursor-transact-sql"></a>sp_help_fulltext_tables_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  使用游标返回为全文索引注册的表的列表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用新**sys.fulltext_indexes**改用目录视图。 有关详细信息，请参阅[sys.fulltext_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@cursor_return=** ] *@cursor_variable*输出  
 是类型的输出变量**光标**。 游标是只读的可滚动动态游标。  
  
 [ **@fulltext_catalog_name=** ] **'***fulltext_catalog_name***'**  
 全文目录名称。 *fulltext_catalog_name*是**sysname**，默认值为 NULL。 如果*fulltext_catalog_name*省略或为 NULL，返回所有与数据库关联的全文索引的表。 如果*fulltext_catalog_name*指定，但*table_name*省略或为 NULL，与此目录相关联的每个全文索引表检索的全文索引信息。 如果这两个*fulltext_catalog_name*和*table_name*指定，如果返回一行*table_name*与关联*fulltext_catalog_name*;否则，将引发错误。  
  
 [ **@table_name=**] **'***table_name***'**  
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
  
## <a name="permissions"></a>权限  
 执行权限默认授予的成员**公共**角色。  
  
## <a name="examples"></a>示例  
 以下示例返回与 `Cat_Desc` 全文目录相关联的全文索引表的名称。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_tables_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>另请参阅  
 [INDEXPROPERTY (Transact-SQL)](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY (Transact-SQL)](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
