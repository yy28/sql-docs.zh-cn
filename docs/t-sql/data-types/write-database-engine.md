---
title: "写入 （数据库引擎） |Microsoft 文档"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60707b57671c2ad607bd85b0fedececccd478038
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="write-database-engine"></a>Write（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

编写出的二进制表示形式写入**SqlHierarchyId**到传入的**BinaryWriter**。 不能通过使用调用写入[!INCLUDE[tsql](../../includes/tsql-md.md)]。 请改为使用 CAST 或 CONVERT。
  
## <a name="syntax"></a>语法  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>参数  
*w*  
A **BinaryWriter**与对象的二进制表示形式这**hierarchyid**节点将写出。
  
## <a name="return-types"></a>返回类型  
**CLR 返回类型： void**
  
## <a name="remarks"></a>注释  
内部使用写入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当有必要，如加载中的数据时**hierarchyid**列。 之间进行转换时，写入还内部调用**hierarchyid**和**varbinary**。
  
## <a name="examples"></a>示例  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>另请参阅
[读取 &#40; 数据库引擎 &#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40; 数据库引擎 &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

