---
title: IsDescendantOf（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 28816e7b109c397826506078388da69fea271d93
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418106"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

如果这是父级的后代，则返回 true。
  
## <a name="syntax"></a>语法  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>参数  
parent  
要执行 IsDescendantOf 测试的 Hierarchyid 节点。
  
## <a name="return-types"></a>返回类型  
SQL Server 返回类型：bit
  
CLR 返回类型：SqlBoolean
  
## <a name="remarks"></a>Remarks  
对于以父级为根的子树中的所有节点，返回 true；对于其他所有节点，返回 false。
  
父级被视为其本身的后代。
  
## <a name="examples"></a>示例  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. 在 WHERE 子句中使用 IsDescendantOf  
下面的示例返回某个经理以及向该经理报告的雇员：
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. 使用 IsDescendantOf 计算关系  
下面的代码声明并填充三个变量。 然后它计算层次结构关系，基于比较返回两个显示结果之一：
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. 调用公共语言运行时方法  
下面的代码段调用 `IsDescendantOf()` 方法。
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>另请参阅
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[分层数据 (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
