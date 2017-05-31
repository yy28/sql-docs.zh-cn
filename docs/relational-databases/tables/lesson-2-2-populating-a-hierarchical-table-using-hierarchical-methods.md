---
title: "使用分层方法填充层次结构表 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID
ms.assetid: 2c95fa60-5b8e-4a05-ac09-cffe2b05900a
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e4d9493f0abe60af4e4c063223cef63a080ed13f
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-2-2---populating-a-hierarchical-table-using-hierarchical-methods"></a>第 2-2 课 - 使用分层方法填充层次结构表
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 有 8 名在市场营销部门工作的雇员。 雇员的层次结构如下所示：  
  
**David**（ **EmployeeID** 为 6）是市场营销经理。 **David**下辖三名市场营销专员，他们分别是：  
  
-   **Sariya**， **EmployeeID** 46  
  
-   **John**， **EmployeeID** 271  
  
-   **Jill**， **EmployeeID** 119  
  
销售助理 **Wanida** (**EmployeeID** 269)，是 **Sariya**的下属；销售助理 **Mary** (**EmployeeID** 272)，是 **John**的下属。  
  
### <a name="to-insert-the-root-of-the-hierarchy-tree"></a>插入层次结构树的根  
  
1.  下例将市场营销经理 **David** 插入层次结构的根处的表中。 **OrdLevel** 列是一个计算列。 因此，它不是 INSERT 语句的一部分。 第一条记录使用 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) 方法将其自身填充为层次结构的根。  
  
    ```  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  执行以下代码来检查表中的初始行：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
如上一课所述，使用 `ToString()` 方法将 **hierarchyid** 数据类型转换成更易于理解的格式。  
  
### <a name="to-insert-a-subordinate-employee"></a>插入下属雇员  
  
1.  **Sariya** 是 **David**的下属。 若要插入 **Sariya** 的节点，必须创建数据类型为 **hierarchyid** 的适当的 **OrgNode**值。 下面的代码创建一个数据类型为 **hierarchyid** 的变量，并用表的根 OrgNode 值填充此变量。 然后使用该变量和 [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) 方法插入从属节点行。 `GetDescendant` 采用两个参数。 检查以下选项的参数值：  
  
    -   如果父级为 NULL， `GetDescendant` 返回 NULL。  
  
    -   如果父级不为 NULL，并且 child1 和 child2 为 NULL， `GetDescendant` 返回父级的子级。  
  
    -   如果父级和 child1 不为 NULL，而 child2 为 NULL， `GetDescendant` 返回一个大于 child1 的父级的子级。  
  
    -   如果父级和 child2 不为 NULL，而 child1 为 NULL， `GetDescendant` 返回一个小于 child2 的父级的子级。  
  
    -   如果父级、child1 和 child2 都不为 NULL， `GetDescendant` 返回一个大于 child1 且小于 child2 的父级的子级。  
  
    下面的代码使用根父级的 `(NULL, NULL)` 参数，因为除了根外，表中尚未存在其他行。 执行下面的代码以插入 **Sariya**：  
  
    ```  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  从第一个过程重复查询来对表进行查询并查看项的显示方式：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="to-create-a-procedure-for-entering-new-nodes"></a>创建输入新节点的过程  
  
1.  若要简化数据的输入，请创建下面的存储过程以向 **EmployeeOrg** 表添加雇员。 该过程接受有关将要添加的雇员的输入值。 这包括新雇员的上司的 **EmployeeID** 、新雇员的 **EmployeeID** 号以及他们的名字和职位。 该过程使用 `GetDescendant()` 和 [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) 方法。 执行下面的代码以创建此过程：  
  
    ```  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  以下示例添加作为 **David**的直接或非直接下属的其余 4 名雇员。  
  
    ```  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  再次执行下面的查询以检查 **EmployeeOrg** 表中的行：  
  
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
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
现在，市场营销组织已完全填充在表中。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[使用层次结构方法查询层次结构表](../../relational-databases/tables/lesson-2-3-querying-a-hierarchical-table-using-hierarchy-methods.md)  
  
  
  

