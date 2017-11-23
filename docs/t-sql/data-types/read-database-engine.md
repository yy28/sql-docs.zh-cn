---
title: "读取 （数据库引擎） |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs: TSQL
helpviewer_keywords: Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72ebda7a9bd00b44983d29db2ef433c9f7d43f94
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="read-database-engine"></a>Read（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

读取读取二进制表示形式**SqlHierarchyId**从传入的**BinaryReader**和设置**SqlHierarchyId**与此值的对象。 不能通过使用调用读取[!INCLUDE[tsql](../../includes/tsql-md.md)]。 请改为使用 CAST 或 CONVERT。
  
## <a name="syntax"></a>语法  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>参数  
*r*  
 **BinaryReader**生成二进制流对应的二进制表示形式的对象**hierarchyid**节点。  
  
## <a name="return-types"></a>返回类型
 **CLR 返回类型： void**  
  
## <a name="remarks"></a>注释  
 读取不会验证其输入。 如果给定了无效的二进制输入，则读取可能引发异常。 或者，它可能成功，生成无效**SqlHierarchyId**对象的方法可以产生不可预知的结果或引发异常。  
  
 只能调用读取上新创建**SqlHierarchyId**对象。  
  
 内部使用读取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当有必要，如时将数据写入到**hierarchyid**列。 之间进行转换时，读取还内部调用**varbinary**和**hierarchyid**。  
  
## <a name="examples"></a>示例  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>另请参阅  
[写入 &#40; 数据库引擎 &#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40; 数据库引擎 &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
