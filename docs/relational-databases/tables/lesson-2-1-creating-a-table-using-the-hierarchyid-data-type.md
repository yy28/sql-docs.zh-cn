---
title: "使用 hierarchyid 数据类型创建表 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: HierarchyID
ms.assetid: 0d1f361f-336c-4571-99d1-f4813b2d9fc4
caps.latest.revision: "17"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2553d79e0cfb2dc2568874f6a52f98cf1d9abc1
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-2-1---creating-a-table-using-the-hierarchyid-data-type"></a>第 2-1 课 - 使用 hierarchyid 数据类型创建表
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] 下列创建了名为 EmployeeOrg 的表，该表包含雇员数据及其报告层次结构。 本例在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中创建该表，但这是可选操作。 为了简化该示例，此表仅包含五列：  
  
-   OrgNode 是一个存储层次结构关系的 **hierarchyid** 列。  
  
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
[使用分层方法填充层次结构表](../../relational-databases/tables/lesson-2-2-populating-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
  
