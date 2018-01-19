---
title: "WRITETEXT (TRANSACT-SQL) |Microsoft 文档"
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
- WRITETEXT_TSQL
- WRITETEXT
dev_langs: TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d8c66e4a785fd1d731bd55730a8439f5e796b01f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  允许最小日志记录、 交互式更新现有**文本**， **ntext**，或**映像**列。 WRITETEXT 将覆盖受其影响的列中的所有现有数据。 不能用于 WRITETEXT**文本**， **ntext**，和**映像**视图中的列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用大值数据类型和**。**写入子句[更新](../../t-sql/queries/update-transact-sql.md)语句相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>参数  
 BULK  
 启用上载工具来上载二进制数据流。 该数据流必须由该工具在 TDS 协议级别提供。 在数据流不存在时，查询处理器将忽略 BULK 选项。  
  
> [!IMPORTANT]  
>  我们建议不要在基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的应用程序中使用 BULK 选项。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中可能会更改或删除该选项。  
  
 *table* **.column**  
 是表名称和**文本**， **ntext**，或**映像**列更新。 表和列名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 可以选择是否指定数据库名和所有者名。  
  
 *text_ptr*  
 是一个值，用于存储指向**文本**， **ntext**，或**映像**数据。 *text_ptr*必须**binary （16)**。若要创建的文本指针，执行[插入](../../t-sql/statements/insert-transact-sql.md)或[更新](../../t-sql/queries/update-transact-sql.md)语句不是空的数据与**文本**， **ntext**，或**映像**列。  
  
 WITH LOG  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 忽略此参数。 日志记录由数据库的当前恢复模式决定。  
  
 *data*  
 是实际**文本**， **ntext**或**映像**要存储数据。 *数据*可以是一个文本值或参数。 可以使用 WRITETEXT 以交互方式插入的文本的最大长度大小约为 120 KB 的**文本**， **ntext**，和**映像**数据。  
  
## <a name="remarks"></a>注释  
 使用 WRITETEXT 替换**文本**， **ntext**，和**映像**数据和 UPDATETEXT 修改**文本**， **ntext**，和**映像**数据。 UPDATETEXT 是更灵活，因为仅的一部分，它将更改**文本**， **ntext**，或**映像**而不是整个列的列。  
  
 为了获得最佳性能，建议**文本**， **ntext**，和**映像**数据要插入或更新 8040 字节的倍数的块区大小。  
  
 如果数据库恢复模式是简单或大容量日志**文本**， **ntext**，和**映像**当新数据时，使用 WRITETEXT 的操作的最小日志记录的操作插入或追加。  
  
> [!NOTE]  
>  在更新现有值时，不使用最小日志记录。  
  
 为了正确使用 WRITETEXT，列必须已经包含有效的文本指针。  
  
 如果表没有行文本，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过不初始化节省空间**文本**列中添加显式或隐式的 null 值时**文本**具有 INSERT、 和没有文本指针的列可以是获取此类 null 值。 若要初始化**文本**为 NULL，列使用 UPDATE 语句。 如果表有行内文本，则不必为空值初始化文本列，而且始终可以获取文本指针。  
  
 ODBC SQLPutData 函数有更快，然后使用 WRITETEXT 比不太动态内存。 此函数可以插入达 2 千兆字节的**文本**， **ntext**，或**映像**数据。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在行文本指向**文本**， **ntext**，或**映像**数据可能存在，但可能不会有效。 有关 text in row 选项的信息，请参阅[sp_tableoption &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 有关使文本指针无效的信息，请参阅[sp_invalidate_textptr &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
## <a name="permissions"></a>权限  
 需要对指定表的 UPDATE 权限。 可在转移 UPDATE 权限时转移这些权限。  
  
## <a name="examples"></a>示例  
 以下示例将文本指针放到局部变量 `@ptrval` 中，然后 `WRITETEXT` 将新的文本字符串放到 `@ptrval` 指向的行中。  
  
> [!NOTE]  
>  若要运行此示例，必须安装 pubs 示例数据库。  
  
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
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40;Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
