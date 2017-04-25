---
title: "检查 Employee 表的当前结构 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e4f881ca9ee3cf85edbbb4d474406e94fe1658ef
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-1---examining-the-current-structure-of-the-employee-table"></a>第 1-1 课 - 检查 Employee 表的当前结构
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库包含基于 **HumanResources** 架构的 **Employee** 表。 为了避免更改原始表，此步骤将对名为 **EmployeeDemo** 的 **Employee**表创建一个副本。 若要简化此示例，你只需从原始表中复制五列数据。 然后，查询 **HumanResources.EmployeeDemo** 表以查看在不使用 **hierarchyid** 数据类型的情况下表中数据的结构。  
  
### <a name="to-copy-the-employee-table"></a>复制 Employee 表  
  
1.  在查询编辑器窗口中，运行下列代码以将 **Employee** 表中的表结构和数据复制到名为 **EmployeeDemo**的新表中。  
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT EmployeeID, LoginID, ManagerID, Title, HireDate   
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee ;  
    GO  
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>检查 EmployeeDemo 表的结构和数据  
  
-   这个新的 **EmployeeDemo** 表表示现有数据库中你可能要迁移到新结构的典型表。 在查询编辑器窗口中，运行下列代码以显示表如何使用自联接来显示雇员/经理关系：  
  
    ```  
    SELECT   
         Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
         Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.Title  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  Title  
    NULL NULL                      109 adventure-works\ken0     Chief Executive Officer  
    3    adventure-works\roberto0  4   adventure-works\rob0     Senior Tool Designer  
    3    adventure-works\roberto0  9   adventure-works\gail0    Design Engineer  
    3    adventure-works\roberto0  11  adventure-works\jossef0  Design Engineer  
    3    adventure-works\roberto0  158 adventure-works\dylan0   Research and Development Manager  
    3    adventure-works\roberto0  263 adventure-works\ovidiu0  Senior Tool Designer  
    3    adventure-works\roberto0  267 adventure-works\michael8 Senior Design Engineer  
    3    adventure-works\roberto0  270 adventure-works\sharon0  Design Engineer  
    6    adventure-works\david0    2   adventure-works\kevin0   Marketing Assistant  
    ...  
    ```  
  
    结果在继续，共 290 行。  
  
请注意， **ORDER BY** 子句会使输出将每个管理级别的直接下属都列在一起。 例如， **MgrID** 3 (roberto0) 的所有七个直接下属都彼此紧挨着列出。 虽然有可能实现，但是要将最终向 **MgrID** 3 负责的所有雇员进行分组将会更加困难。  
  
在下一个任务中，我们将使用 **hierarchyid** 数据类型创建一个新表，然后将数据移到该新表中。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[使用现有层次结构数据填充表](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
  

