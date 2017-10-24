---
title: "READTEXT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c501fe8ea8146b4b2ec6e138f72fc2604b4b374
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  读取**文本**， **ntext**，或**映像**值从**文本**， **ntext**，或**映像**列中，从指定的偏移量和读取指定的数目的字节。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[子字符串](../../t-sql/functions/substring-transact-sql.md)函数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>参数  
 *表* **。** *列*  
 要对其执行读取操作的表和列的名称。 表和列名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 必须指定表名和列名。但是，可根据需要指定数据库名称和数据库所有者名称。  
  
 *text_ptr*  
 有效的文本指针。 *text_ptr*必须**binary （16)**。  
  
 *偏移量*  
 是的字节数 (时**文本**或**映像**使用数据类型) 或字符 (时**ntext**使用数据类型) 跳过在其开始读取之前**文本**，**映像**，或**ntext**数据。  
  
 *大小*  
 是的字节数 (时**文本**或**映像**使用数据类型) 或字符 (时**ntext**使用数据类型) 的要读取数据。 如果*大小*为 0，读取的数据的 4 KB 字节。  
  
 HOLDLOCK  
 使文本值被锁定以进行读取，直到事务结束为止。 其他用户可读取该值，但不能对其进行修改。  
  
## <a name="remarks"></a>注释  
 使用[TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)函数来获取有效*text_ptr*值。 TEXTPTR 返回一个指向**文本**， **ntext**，或**映像**列中指定的行或**文本**， **ntext**，或**映像**如果返回多个行由查询返回的最后一行中的列。 由于 TEXTPTR 返回 16 字节的二进制字符串，因此我们建议声明一个局部变量来保存该文本指针，然后在 READTEXT 中使用该变量。 有关声明本地变量的详细信息，请参阅[DECLARE @local_variable &#40;Transact SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，可能存在行内文本指针，但该指针可能无效。 有关详细信息**一行中的文本**选项，请参阅[sp_tableoption &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). 有关使文本指针无效的详细信息，请参阅[sp_invalidate_textptr &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 值 @@TEXTSIZE函数取代如果小于指定大小的 READTEXT READTEXT 为指定的大小。 @@TEXTSIZE函数指定要由 SET TEXTSIZE 语句返回集的数据的字节数限制。 有关如何设置 TEXTSIZE 的会话设置的详细信息，请参阅[SET TEXTSIZE &#40;Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 READTEXT 权限默认授予对指定的表具有 SELECT 权限的用户。 可在转移 SELECT 权限时转移权限。  
  
## <a name="examples"></a>示例  
 以下示例读取 `pr_info` 表中 `pub_info` 列的第 2 个至第 26 个字符。  
  
> [!NOTE]  
>  若要运行此示例，你必须安装**pubs**示例数据库。  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [@@TEXTSIZE (Transact-SQL)](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  

