---
title: Read（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 60575f2c5c5f1de4a7fa5b2531fb8431f13b4441
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052244"
---
# <a name="read-database-engine"></a>Read（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Read 从传入的 BinaryReader 中读取 SqlHierarchyId 的二进制表示形式，并将 SqlHierarchyId 对象设置为该值。 无法通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 来调用 Read。 请改为使用 CAST 或 CONVERT。
  
## <a name="syntax"></a>语法  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>参数  
*r*  
 BinaryReader 对象，该对象生成对应于 hierarchyid 节点的二进制表示形式的二进制流。  
  
## <a name="return-types"></a>返回类型
 CLR 返回类型：void  
  
## <a name="remarks"></a>Remarks  
 Read 不验证其输入。 如果给出了无效的二进制输入，则 Read 可能引发异常。 或者，它可能成功并生成无效的 SqlHierarchyId 对象，这些对象的方法可能给出不可预测的结果或引发异常。  
  
 只能对新创建的 SqlHierarchyId 对象调用 Read。  
  
 必要时（例如，将数据写入 hierarchyid 列时），[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在内部使用 Read。 在 varbinary 和 hierarchyid 之间进行转换时，也将在内部调用 Read。  
  
## <a name="examples"></a>示例  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>另请参阅  
[Write（数据库引擎）](../../t-sql/data-types/write-database-engine.md)  
[ToString（数据库引擎）](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
