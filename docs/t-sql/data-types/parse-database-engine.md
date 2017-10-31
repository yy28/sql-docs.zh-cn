---
title: "分析 （数据库引擎） |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 027940c7575f3c7901cd8668879064ff375d9986
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="parse-database-engine"></a>Parse（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

分析的规范字符串表示形式转换**hierarchyid**到**hierarchyid**值。 当从到的字符串类型的转换时，隐式调用分析**hierarchyid**时发生。 充当相反[ToString](../../t-sql/data-types/tostring-database-engine.md)。 Parse （） 是一种静态方法。
  
## <a name="syntax"></a>语法  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>参数  
*输入*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]：要转换的字符数据类型值。
  
CLR：要计算的字符串值。
  
## <a name="return-types"></a>返回类型  
**SQL Server 返回类型： hierarchyid**
  
**CLR 返回类型： SqlHierarchyId**
  
## <a name="remarks"></a>注释  
如果分析收到一个值，不是有效的字符串表示形式**hierarchyid**，将引发异常。 例如，如果**char**数据类型包含尾随空格，则引发异常。
  
## <a name="examples"></a>示例  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. 不使用表转换 Transact-SQL 值  
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
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="b-clr-example"></a>B. CLR 示例  
下面的代码段调用 parse （） 方法：
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>另请参阅
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[分层数据 (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

