---
title: "GetLevel （数据库引擎） |Microsoft 文档"
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
- GetLevel
- GetLevel_TSQL
dev_langs: TSQL
helpviewer_keywords: GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a12afc32b16a6cd6af3cf5a5551b783a450207e1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="getlevel-database-engine"></a>GetLevel（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回一个整数，表示节点的深度*这*在树中。
  
## <a name="syntax"></a>语法  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  
  
## <a name="return-types"></a>返回类型  
**SQL Server 返回类型： smallint**
  
**CLR 返回类型： SqlInt16**
  
## <a name="remarks"></a>注释  
用于确定一个或多个节点的级别或者筛选指定级别的成员的节点。 层次结构的根节点为级别 0。
  
GetLevel 是对广度优先搜索索引非常有用。 有关详细信息，请参阅[层次结构数据 &#40;SQL server&#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. 将层次结构级别返回为列  
下面的示例返回的文本表示形式**hierarchyid**，然后为此层次结构级别和**EmpLevel**列对于表中的所有行：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. 返回层次结构级别的所有成员  
下面的示例返回表中层次结构级别为 2 的所有行：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. 返回层次结构的根节点  
下面的示例返回层次结构级别的根节点：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. CLR 示例  
下面的代码段调用 getlevel （） 方法：
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>另请参阅
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[分层数据 (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
