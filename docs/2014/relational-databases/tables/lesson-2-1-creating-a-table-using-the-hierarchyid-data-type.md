---
title: 使用 hierarchyid 数据类型创建表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 0d1f361f-336c-4571-99d1-f4813b2d9fc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a5af072e27ff1e1c70d6a3035ceb7eb2a1cc2493
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088907"
---
# <a name="creating-a-table-using-the-hierarchyid-data-type"></a>使用 hierarchyid 数据类型创建表
  下例创建了一个名为 EmployeeOrg 的表，该表包含雇员数据及其报告层次结构。 本例在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中创建该表，但这是可选操作。 为了简化该示例，此表仅包含五列：  
  
-   OrgNode 是一个存储层次结构关系的 `hierarchyid` 列。  
  
-   OrgLevel 是一个计算列，它基于存储层次结构中的各节点级别的 OrgNode 列。 它将用于广度优先索引。  
  
-   EmployeeID 包含用于诸如工资单等应用程序的典型雇员标识号。 在新应用程序的开发过程中，应用程序可以使用 OrgNode 列，不需要这个单独的 EmployeeID 列。  
  
-   EmpName 包含雇员的姓名。  
  
-   Title 包含雇员的职位。  
  
### <a name="to-create-the-employeeorg-table"></a>创建 EmployeeOrg 表  
  
1.  在“查询编辑器”窗口中，运行以下代码来创建 `EmployeeOrg` 表。 将 `OrgNode` 列指定为具有聚集索引的主键，即创建了深度优先索引：  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  运行下面的代码，对 `OrgLevel` 和 `OrgNode` 列创建组合索引，以便支持高效的广度优先搜索：  
  
    ```  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
 现在即可为该表填充数据。 下一个任务将通过使用分层方法来填充该表。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [使用分层方法填充层次结构表](lesson-2-2-populating-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
