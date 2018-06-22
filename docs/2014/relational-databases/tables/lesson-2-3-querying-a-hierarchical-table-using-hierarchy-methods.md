---
title: 使用层次结构方法查询层次结构表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- HierarchyID
ms.assetid: 3b4f7dae-65b5-4d8d-8641-87aba9aa692d
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a24ce251efe3b6f3e23743be8ca1634f0493683d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018134"
---
# <a name="querying-a-hierarchical-table-using-hierarchy-methods"></a>使用层次结构方法查询层次结构表
  由于 HumanResources.EmployeeOrg 表已完全填充，此任务将说明如何使用某些分层方法来查询层次结构。  
  
### <a name="to-find-subordinate-nodes"></a>查找从属节点  
  
1.  Sariya 有一名下属雇员。 若要查询 Sariya 的下属，请执行使用 [IsDescendantOf](/sql/t-sql/data-types/isdescendantof-database-engine) 方法的以下查询：  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
     结果同时列出 Sariya 和 Wanida。 Sariya 的列出原因是她是 0 级后代。 Wanida 是 1 级后代。  
  
2.  也可以使用 [GetAncestor](/sql/t-sql/data-types/getancestor-database-engine) 方法查询此信息。 `GetAncestor` 对尝试返回的级别采用了一个参数。 由于 Wanida 位于 Sariya 下面一级，因此使用 `GetAncestor(1)` ，如以下代码所示：  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
     这次，结果仅列出 Wanida。  
  
3.  现在，将 `@CurrentEmployee` 更改为 David (EmployeeID 6)，并将级别更改为 2。 执行以下过程也会返回 Wanida：  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
     这次，还收到向 David 报告的位于两个级别之下的 Mary。  
  
### <a name="to-use-getroot-and-getlevel"></a>使用 GetRoot 和 GetLevel  
  
1.  随着层次结构不断扩大，更加难于确定成员在层次结构中的位置。 使用 [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) 方法可查明每一行下方有多少个级别处于层次结构中。 执行下面的代码以查看所有行的下属级别：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  使用 [GetRoot](/sql/t-sql/data-types/getroot-database-engine) 方法查找层次结构中的根节点。 下面的代码返回一个作为根的行：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
  
 下一个任务将重新组织层次结构。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [使用分层方法对层次结构表中的数据重新排序](lesson-2-4-reordering-data-in-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
