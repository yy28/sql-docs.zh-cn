---
title: 优化 NewOrg 表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
author: stevestein
ms.author: sstein
ms.openlocfilehash: 39c09a3a73051e7a61f3a62a125232d83d1570c0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068082"
---
# <a name="optimizing-the-neworg-table"></a>优化 NewOrg 表
  在使用[现有层次结构数据填充表](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)任务中创建的**NewOrd**表包含所有雇员信息，并使用数据类型表示层次结构 `hierarchyid` 。 此任务添加了新的索引，以便支持对 `hierarchyid` 列的搜索。  
  
## <a name="clustered-index"></a>聚集索引  
 `hierarchyid`列（**OrgNode**）是**NewOrg**表的主键。 此表创建时，其内包含了一个名为 **PK_NewOrg_OrgNode** 的聚集索引，用于强制实现“OrgNode”**** 列的唯一性。 此聚集索引还支持对表进行深度优先搜索。  
  
## <a name="nonclustered-index"></a>非聚集索引  
 此步骤将创建两个非聚集索引，用于支持典型搜索。  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>为 NewOrg 表创建索引以提高搜索效率  
  
1.  若要改善在层次结构中同一级别的查询，可以使用 [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) 方法创建一个包含此层次结构中的此级别的计算列。 然后，对此级别和 `Hierarchyid` 创建一个组合索引。 运行下列代码以创建计算列和广度优先索引：  
  
    ```  
    ALTER TABLE NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  对“EmployeeID”**** 列创建一个唯一索引。 即采用传统方式通过 **EmployeeID** 号单独查找一个雇员。 运行下列代码以便对 **EmployeeID**创建索引：  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON NewOrg(EmployeeID) ;  
    GO  
    ```  
  
3.  运行下列代码以分别按照三个索引的顺序从表中检索数据：  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM NewOrg   
    ORDER BY OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY H_Level, OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  比较结果集以查看每类索引中的存储顺序。 下面只显示了各输出的前四行。  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     深度优先索引：雇员记录存储在与相应经理的记录相邻的位置。  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     **EmployeeID**优先索引：各行按照 **EmployeeID** 顺序存储。  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
> [!NOTE]  
>  有关显示深度优先索引和广度优先索引之间差异的关系图，请参阅[分层数据 (SQL Server)](../hierarchical-data-sql-server.md)。  
  
#### <a name="to-drop-the-unnecessary-columns"></a>删除不需要的列  
  
1.  “ManagerID”**** 列用于表示雇员/经理关系，现在由“OrgNode”**** 列来表示。 如果其他应用程序不需要“ManagerID”**** 列，可以考虑使用下列语句删除该列：  
  
    ```  
    ALTER TABLE NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  “EmployeeID”**** 列也是冗余列。 “OrgNode”**** 列可以唯一标识每个雇员。 如果其他应用程序不需要“EmployeeID”**** 列，可以考虑使用下列代码先删除索引再删除该列：  
  
    ```  
    DROP INDEX EmpIDs_unq ON NewOrg ;  
    ALTER TABLE NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>使用新表替换原始表  
  
1.  如果原始表包含任何其他索引或约束，请将它们添加到“NewOrg”**** 表中。  
  
2.  将旧的“EmployeeDemo”**** 表替换为新表。 运行下列代码以删除旧表，然后使用旧表的名称重新命名新表：  
  
    ```  
    DROP TABLE EmployeeDemo ;  
    GO  
    sp_rename 'NewOrg', EmployeeDemo ;  
    GO  
    ```  
  
3.  运行下列代码以检查最终表：  
  
    ```  
    SELECT * FROM EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [摘要：将表转换为层次结构](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
