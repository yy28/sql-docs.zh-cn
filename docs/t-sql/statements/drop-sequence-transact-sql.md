---
title: "拖放序列 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SEQUENCE
- DROP_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SEQUENCE statement
- sequence number object, dropping
ms.assetid: c25772d3-61af-4aa7-b58b-a6f67a793e3d
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d7247c5e809c8e26fbd17dc01e8c2f624a170ff
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-sequence-transact-sql"></a>DROP SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  从当前数据库中删除序列对象。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP SEQUENCE [ IF EXISTS ] { [ database_name . [ schema_name ] . | schema_name. ]    sequence_name } [ ,...n ]  
 [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地将删除序列。  
  
 *database_name*  
 要在其中创建序列对象的数据库的名称。  
  
 *schema_name*  
 序列对象所属架构的名称。  
  
 *sequence_name*  
 要删除的序列的名称。 类型是**sysname**。  
  
## <a name="remarks"></a>注释  
 在生成编号后，序列对象与其生成的编号之间没有延续关系，因此可以删除序列对象，即使生成的编号仍在使用。  
  
 当序列对象由存储过程或触发器引用时，可以删除序列对象，因为序列对象未绑定到架构上。 如果序列对象是作为表中的默认值引用的，则无法删除序列对象。 错误消息将列出引用序列的对象。  
  
 若要列出数据库中的所有序列对象，请执行以下语句。  
  
```  
SELECT sch.name + '.' + seq.name AS [Sequence schema and name]   
    FROM sys.sequences AS seq  
    JOIN sys.schemas AS sch  
        ON seq.schema_id = sch.schema_id ;  
GO  
```  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求具有架构的 ALTER 或 CONTROL 权限。  
  
### <a name="audit"></a>审核  
 审核**删除序列**，监视器**SCHEMA_OBJECT_CHANGE_GROUP**。  
  
## <a name="examples"></a>示例  
 以下示例从当前数据库中删除一个名为 `CountBy1` 的序列对象。  
  
```  
DROP SEQUENCE CountBy1 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 序列 &#40;Transact SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [创建序列 &#40;Transact SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [下一个值 &#40;Transact SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

