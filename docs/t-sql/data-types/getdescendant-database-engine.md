---
title: "GetDescendant （数据库引擎） |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d79b0bc3d47acf6be5315688398e7047b823d8e7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="getdescendant-database-engine"></a>GetDescendant（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回父级的一个子节点。
  
## <a name="syntax"></a>语法  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>参数  
*child1*  
NULL 或**hierarchyid**的当前节点的子级。
  
*child2*  
NULL 或**hierarchyid**的当前节点的子级。
  
## <a name="return-types"></a>返回类型  
**SQL Server 返回类型： hierarchyid**
  
**CLR 返回类型： SqlHierarchyId**
  
## <a name="remarks"></a>注释  
返回作为父节点的后代的一个子节点。
-   如果父级为 NULL，则返回 NULL。  
-   如果父级不为 NULL，而 child1 和 child2 为 NULL，则返回父级的子级。  
-   如果父级和 child1 不为 NULL，而 child2 为 NULL，则返回一个大于 child1 的父级的子级。  
-   如果父级和 child2 不为 NULL，而 child1 为 NULL，则返回一个小于 child2 的父级的子级。  
-   如果父级、child1 和 child2 都不为 NULL，则返回一个大于 child1 且小于 child2 的父级的子级。  
-   如果 child1 不为 NULL 且不是父级的子级，则引发异常。  
-   如果 child2 不为 NULL 且不是父级的子级，则引发异常。  
-   如果 child1 >= child2，则引发异常。  
  
GetDescendant 是确定的。 因此，如果使用相同的输入调用 GetDescendant，则它将始终生成相同的输出。 不过，生成的子级的确切身份可能因其与其他节点的关系而异，如示例 C 所示。
  
## <a name="examples"></a>示例  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>A. 插入一行作为最低级别的后代节点  
新雇用了一名员工，该员工将成为位于 `/3/1/` 节点的现有员工的下属。 执行以下代码以使用不带参数的 GetDescendant 方法用于指定为的新行节点插入新行`/3/1/1/`:
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>B. 插入一行作为较高级别的后代节点  
另一个新的员工加入，向报告如 A.执行的示例所示的相同管理器下面的代码将新行插入使用 GetDescendant 方法使用子 1 参数来指定新行的节点将按照示例 A 中的节点成为`/3/1/2/`:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>C. 在两个现有节点之间插入一行  
第三个员工加入，如示例 A.所示的相同管理器向报告此示例将插入到大于节点的新行`FirstNewEmployee`在示例 A，并小于`SecondNewEmployee`示例 B.执行下面的代码使用 GetDescendant 方法中。 同时使用 child1 参数和 child2 参数指定新行的节点将成为节点 `/3/1/1.1/`：
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
完成示例 A、 B 和 C 后, 添加到表中的节点将对等节点替换为以下**hierarchyid**值：
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
节点 `/3/1/1.1/` 高于节点 `/3/1/1/`，但是在层次结构中处于同一级别。
  
### <a name="d-scalar-examples"></a>D. 标量示例  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持任意插入和删除的任何**hierarchyid**节点。 通过使用 GetDescendant()，并总是可以生成任何这两者之间的节点**hierarchyid**节点。 执行以下代码，使用 `GetDescendant` 生成示例节点：
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>E. CLR 示例  
下面的代码段调用 `GetDescendant()` 方法：
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>另请参阅
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[分层数据 (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
