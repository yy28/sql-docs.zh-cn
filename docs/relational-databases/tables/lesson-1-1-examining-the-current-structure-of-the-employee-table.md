---
title: 检查 Employee 表的当前结构 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fa6d4693132ec646438ab7cd0f45f85569c4109f
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="lesson-1-1---examining-the-current-structure-of-the-employee-table"></a>第 1-1 课 - 检查 Employee 表的当前结构
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
示例 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]（或更高版本）数据库包含基于“HumanResources”架构的“Employee”表。 为了避免更改原始表，此步骤将对名为 **EmployeeDemo** 的 **Employee**表创建一个副本。 若要简化此示例，你只需从原始表中复制五列数据。 然后，查询 **HumanResources.EmployeeDemo** 表以查看在不使用 **hierarchyid** 数据类型的情况下表中数据的结构。  
  
### <a name="to-copy-the-employee-table"></a>复制 Employee 表  
  
1.  在查询编辑器窗口中，运行下列代码以将 **Employee** 表中的表结构和数据复制到名为 **EmployeeDemo**的新表中。 由于原始表已使用 hierarchyid，本次查询实质上合会并层次结构，以便检索 employee 的管理员。 在本课程的后续部分中，我们将重新构建该层次结构。
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
      (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
            WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
                (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID
        , emp.JobTitle, emp.HireDate
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee emp ;
    GO
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>检查 EmployeeDemo 表的结构和数据  
  
-   这个新的 **EmployeeDemo** 表表示现有数据库中你可能要迁移到新结构的典型表。 在查询编辑器窗口中，运行下列代码以显示表如何使用自联接来显示雇员/经理关系：  
  
    ```  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL    1   adventure-works\ken0    Chief Executive Officer
    1   adventure-works\ken0    2   adventure-works\terri0  Vice President of Engineering
    1   adventure-works\ken0    16  adventure-works\david0  Marketing Manager
    1   adventure-works\ken0    25  adventure-works\james1  Vice President of Production
    1   adventure-works\ken0    234 adventure-works\laura1  Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0   Information Services Manager
    1   adventure-works\ken0    273 adventure-works\brian3  Vice President of Sales
    2   adventure-works\terri0  3   adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0    Senior Tool Designer
    ...  
    ```  
  
    结果在继续，共 290 行。  
  
请注意， **ORDER BY** 子句会使输出将每个管理级别的直接下属都列在一起。 例如，MgrID 1 (ken0) 的所有七个直接下属都彼此紧挨着列出。 虽然有可能实现，但是要将最终向 MgrID 1 负责的所有雇员进行分组将会更加困难。  
  
在下一个任务中，我们将使用 **hierarchyid** 数据类型创建一个新表，然后将数据移到该新表中。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[使用现有层次结构数据填充表](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
  
