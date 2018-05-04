---
title: sp_help_fulltext_columns_cursor (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns_cursor
- sp_help_fulltext_columns_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns_cursor
ms.assetid: 26054e76-53b7-4004-8d48-92ba3435e9d7
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 68f4ea3cb7acbdfaf698475f8e2bc9e3cc95fa86
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfulltextcolumnscursor-transact-sql"></a>sp_help_fulltext_columns_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用游标返回为全文索引指派的列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)改用目录视图。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@cursor_return =**] *@cursor_variable*输出  
 是类型的输出变量**光标**。 结果游标是只读的可滚动动态游标。  
  
 [ **@table_name =**] **'***table_name***'**  
 为其请求全文索引信息的表的名称，由一部分或两部分组成。 *table_name*是**nvarchar(517)**，默认值为 NULL。 如果*table_name*省略，则为每个全文索引表检索的全文检索列信息。  
  
 [ **@column_name =**] **'***column_name***'**  
 需要全文索引元数据的列的名称。 *column_name*是**sysname**默认值为 NULL。 如果*column_name*省略或为 NULL，为每个全文索引列返回全文列信息*table_name*。 如果*table_name*还省略或为 NULL，在数据库中的所有表每个全文索引列返回的全文检索列信息。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|表所有者。 这是创建该表的数据库用户的名称。|  
|**针对 TABLE_ID 所**|**int**|表的 ID。|  
|**TABLE_NAME**|**sysname**|表名。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|为索引指定的全文索引表中的列。|  
|**FULLTEXT_COLID**|**int**|全文索引列的列 ID。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|全文索引表中指定全文索引列文档类型的列。 全文索引的列时，此值才适用**varbinary （max)** 或**映像**列。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|文档类型列的列 ID。 全文索引的列时，此值才适用**varbinary （max)** 或**映像**列。|  
|**FULLTEXT_LANGUAGE**|**sysname**|用于对列进行全文索引的语言。|  
  
## <a name="permissions"></a>权限  
 执行权限默认授予的成员**公共**角色。  
  
## <a name="examples"></a>示例  
 以下示例将返回有关列的信息，这些列已指派给数据库的所有表中的全文索引。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_columns_cursor @mycursor OUTPUT  
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
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
