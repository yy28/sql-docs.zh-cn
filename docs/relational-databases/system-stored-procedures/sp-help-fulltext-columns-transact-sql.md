---
title: sp_help_fulltext_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 076a3df69245cb269593e1a2298f18c9266ab217
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980326"
---
# <a name="sphelpfulltextcolumns-transact-sql"></a>sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回为全文索引指定的列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)目录视图。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @table_name = ] 'table\_name'` 是为其请求全文索引信息的一部分或两个表名称。 *table_name*是**nvarchar(517)** ，默认值为 NULL。 如果*table_name*省略，则为每个全文索引表检索全文索引列信息。  
  
`[ @column_name = ] 'column\_name'` 是为其请求全文索引元数据的名称。 *column_name*是**sysname**，默认值为 NULL。 如果*column_name*省略或为 NULL，为每个全文索引列返回全文索引列信息*table_name*。 如果*table_name*也未指定或为 NULL，为数据库中的所有表的每个全文索引列返回全文索引列信息。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|表所有者。 这是创建该表的数据库用户的名称。|  
|**TABLE_ID**|**int**|表的 ID。|  
|**TABLE_NAME**|**sysname**|表的名称。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|为索引指定的全文索引表中的列。|  
|**FULLTEXT_COLID**|**int**|全文索引列的列 ID。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|全文索引表中指定全文索引列文档类型的列。 全文本索引的列时，此值才适用**varbinary （max)** 或**映像**列。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|文档类型列的列 ID。 全文本索引的列时，此值才适用**varbinary （max)** 或**映像**列。|  
|**FULLTEXT_LANGUAGE**|**sysname**|用于对列进行全文索引的语言。|  
  
## <a name="permissions"></a>权限  
 执行权限默认授予的成员**公共**角色。  
  
## <a name="examples"></a>示例  
 以下示例返回在 `Document` 表中为全文索引指定的列的信息。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
