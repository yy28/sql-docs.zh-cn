---
title: "使用分层方法对层次结构表中的数据重新排序 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: 7b8064c7-62c6-488d-84d2-57a5828fb907
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3d15df3ae3bf757b54e2e4d48c55b94285540d9
ms.sourcegitcommit: b09bccd6dfdba55b022355e892c29cb50aadd795
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
# <a name="lesson-2-4---reordering-data-in-a-hierarchical-table-using-hierarchical-methods"></a>第 2-4 课 - 使用分层方法对层次结构表中的数据重新排序
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]重新组织层次结构是一项常见的维护任务。 在此任务中，使用包含 [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) 方法的 UPDATE 语句首先将一行移到层次结构的新位置。 然后，我们会将整个子树移到一个新位置。  
  
`GetReparentedValue` 方法使用两个参数。 第一个参数用于描述要修改的层次结构部分。 例如，如果层次结构为 **/1/4/2/3/** ，希望更改 **/1/4/** 部分，将层次结构变为 **/2/1/2/3/**，后两个节点 (**2/3/**) 保持不变，则必须提供要更改的节点 (**/1/4/**) 作为第一个参数。 第二个参数提供新的层次结构级别，在示例中为 **/2/1/**。 这两个参数无须包含相同的级别数。  
  
### <a name="to-move-a-single-row-to-a-new-location-in-the-hierarchy"></a>将一行移到层次结构中的新位置上  
  
1.  当前，Wanida 向 Sariya 报告。 在此过程中，将 Wanida 从其当前的节点 **/1/1/** 移出，使她可以向 Jill 报告。 她的新节点将变为 **/3/1/** ，而 **/1/** 成为第一个参数， **/3/** 成为第二个参数。 这些值与 Sariya 和 Jill 的 **OrgNode** 值相对应。 执行下列代码将 Wanida 从 Sariya 的组织移到 Jill 的组织中：  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  执行下面的代码以查看结果：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    现在，Wanida 位于节点 **/3/1/**。  
  
### <a name="to-reorganize-a-section-of-a-hierarchy"></a>重新组织层次结构中的某一部分  
  
1.  为了演示如何同时移动大量人员，请先执行下列代码，添加一个向 Wanida 报告的实习生：  
  
    ```  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  现在，Kevin 向 Wanida 报告，Wanida 向 Jill 报告，而 Jill 向 David 报告。 也就是说，Kevin 位于级别 **/3/1/1/**。 若要将 Jill 的所有下属都移到一位新经理之下，需要将 **OrgNode** 为 **/3/** 的所有节点更新为新值。 执行下列代码以便将 Wanida 更新为向 Sariya 负责，但 Kevin 仍向 Wanida 负责：  
  
    ```  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  执行下面的代码以查看结果：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
之前向 Jill 报告的整个组织树（Wanida 和 Kevin）现在均向 Sariya 报告。  
  
有关重新组织层次结构中的某一部分的存储过程，请参阅 [移动子树](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees)的“移动子树”部分。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[摘要：管理层次结构表中的数据](../../relational-databases/tables/lesson-2-5-summary-managing-data-in-a-hierarchical-table.md)  
  
  
  
