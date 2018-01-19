---
title: "UPDATETEXT (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2561f089f8982bfed4e0b48c673dea17be22de89
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新现有**文本**， **ntext**，或**映像**字段。 使用 UPDATETEXT 更改仅的一部分**文本**， **ntext**，或**映像**位置中的列。 使用 WRITETEXT 更新并替换整个**文本**， **ntext**，或**映像**字段。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用大值数据类型和**。**写入子句[更新](../../t-sql/queries/update-transact-sql.md)语句相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>参数  
 BULK  
 启用上载工具来上载二进制数据流。 该数据流必须由该工具在 TDS 协议级别提供。 在数据流不存在时，查询处理器将忽略 BULK 选项。  
  
> [!IMPORTANT]  
>  我们建议不要在基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的应用程序中使用 BULK 选项。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中可能会更改或删除该选项。  
  
 *table_name* **。** *dest_column_name*  
 是表名称和**文本**， **ntext**，或**映像**更新的列。 表名称和列名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 可以选择是否指定数据库名和所有者名。  
  
 *dest_text_ptr*  
 为文本指针指向的值 （由 TEXTPTR 函数返回）**文本**， **ntext**，或**映像**要更新的数据。 *dest_text_ptr*必须**二进制 (**16**)**。  
  
 *insert_offset*  
 以零为基的更新起始位置。 有关**文本**或**映像**列， *insert_offset*是要在插入新数据之前跳过从开始处的现有列的字节数。 有关**ntext**列， *insert_offset*字符数 (每个**ntext**字符使用 2 个字节)。 现有**文本**， **ntext**，或**映像**此从零开始的起始位置开始的数据移动到右侧，以便腾出空间供新的数据。 值为 0 表示将新数据插入现有数据的开始处。 值为 NULL 则将新数据追加到现有数据值后。  
  
 *delete_length*  
 是要删除现有的数据的长度**文本**， **ntext**，或**映像**开始，列*insert_offset*位置。 *Delete_length*以字节为单位的指定值**文本**和**映像**列并以字符为**ntext**列。 每个**ntext**字符使用 2 个字节。 值为 0 表示不删除数据。 值为 NULL 删除中的所有数据*insert_offset*位置到末尾的现有**文本**或**映像**列。  
  
 WITH LOG  
 日志记录由数据库的当前恢复模式决定。  
  
 *inserted_data*  
 是要插入到现有的数据**文本**， **ntext**，或**映像**处列*insert_offset*位置。 这是单个**char**， **nchar**， **varchar**， **nvarchar**，**二进制**， **varbinary**，**文本**， **ntext**，或**映像**值。 *inserted_data*可以是文本或变量。  
  
 *table_name.src_column_name*  
 是表名称和**文本**， **ntext**，或**映像**用作插入的数据源的列。 表名和列名必须符合标识符规则。  
  
 *src_text_ptr*  
 为文本指针指向的值 （由 TEXTPTR 函数返回）**文本**， **ntext**，或**映像**用作插入的数据源的列。  
  
> [!NOTE]  
>  *scr_text_ptr*值不能与相同*dest_text_ptr*值。  
  
## <a name="remarks"></a>注释  
 新插入的数据可以是单个*inserted_data*常量、 表名称、 列名称或文本指针。  
  
|Update 操作|UPDATETEXT 参数|  
|-------------------|---------------------------|  
|替换现有数据|指定非空*insert_offset*值，则为非 0 *delete_length*值，并将新的数据要插入。|  
|删除现有数据|指定非空*insert_offset*值、 非零*delete_length*。 不指定要插入的新数据。|  
|插入新数据|指定*insert_offset*值， *delete_length* 0，并将新的数据要插入。|  
  
 为了获得最佳性能，建议**文本**， **ntext**和**映像**数据要插入或更新 8,040 字节的倍数的区块大小。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，行内文本指针到**文本**， **ntext**，或**映像**数据可能存在，但可能不会有效。 有关 text in row 选项的信息，请参阅[sp_tableoption &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 有关使文本指针无效的信息，请参阅[sp_invalidate_textptr &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 若要初始化**文本**为 NULL，列使用 WRITETEXT;UPDATETEXT 初始化**文本**为空字符串的列。  
  
## <a name="permissions"></a>权限  
 需要对指定表的 UPDATE 权限。  
  
## <a name="examples"></a>示例  
 以下示例将文本指针放入局部变量 `@ptrval` 中，然后使用 `UPDATETEXT` 更新拼写错误。  
  
> [!NOTE]  
>  若要运行此示例，必须安装 pubs 数据库。  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr, publishers p  
      WHERE p.pub_id = pr.pub_id   
      AND p.pub_name = 'New Moon Books'  
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [READTEXT &#40;Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40;Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  
