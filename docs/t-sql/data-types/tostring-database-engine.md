---
title: "ToString （数据库引擎） |Microsoft 文档"
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
- ToString
- ToString_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ToString [Database Engine]
ms.assetid: 5fc11ca5-c26d-4518-9512-67aa0270f110
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1544b27215083f8628696cebaaf14c53c628a9ba
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="tostring-database-engine"></a>ToString（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回一个字符串的逻辑表示形式*这*。 当从转换时，隐式调用 ToString **hierarchyid**发生类型为字符串。 充当相反[分析 &#40; 数据库引擎 &#41;](../../t-sql/data-types/parse-database-engine.md)。
  
## <a name="syntax"></a>语法  
  
```sql
-- Transact-SQL syntax  
node.ToString  ( )   
-- This is functionally equivalent to the following syntax  
-- which implicitly calls ToString():  
CAST(node AS nvarchar(4000))  
```  
  
```sql
-- CLR syntax  
string ToString  ( )   
```  
  
## <a name="return-types"></a>返回类型
**SQL Server 返回 type:nvarchar(4000)**
  
**CLR 返回类型： 字符串**
  
## <a name="remarks"></a>注释  
返回层次结构中的逻辑位置。 例如，`/2/1/`表示第四行 ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 中的文件系统的以下层次结构：
  
```sql
/        C:\  
/1/      C:\Database Files  
/2/      C:\Program Files  
/2/1/    C:\Program Files\Microsoft SQL Server  
/2/2/    C:\Program Files\Microsoft Visual Studio  
/3/      C:\Windows  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-transact-sql-example-in-a-table"></a>A. 表中的 Transact-SQL 示例  
下面的示例返回同时`OrgNode`为这两者的列**hierarchyid**数据类型和更易读的字符串格式：
  
```sql
SELECT OrgNode,  
OrgNode.ToString() AS Node  
FROM HumanResources.EmployeeDemo  
ORDER BY OrgNode ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
OrgNode   Node  
0x        /  
0x58      /1/  
0x5AC0    /1/1/  
0x5B40    /1/2/  
0x5BC0    /1/3/  
0x5C20    /1/4/  
...  
```  
  
### <a name="b-converting-transact-sql-values-without-a-table"></a>B. 不使用表转换 Transact-SQL 值  
下面的代码示例使用`ToString`要转换**hierarchyid**为一个字符串，值和`Parse`要转换到的字符串值**hierarchyid**。
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`hierarchyidRepresentation    StringRepresentation`
  
`-------------------------    -----------------------`
  
`0x5ADE                       /1/1/3/`
  
### <a name="c-clr-example"></a>C. CLR 示例  
下面的代码段调用 tostring （） 方法：
  
```sql
this.ToString()  
```  
  
## <a name="see-also"></a>另请参阅
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[分层数据 (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

