---
title: 第 2 课：创建和管理层次结构表中的数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02cfeec26e7970440af931f554e90789defdcb23
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42783008"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>第 2 课：创建和管理层次结构表中的数据
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
在第 1 课中，你修改了一个现有表以使用 **hierarchyid** 数据类型，并采用现有数据的表示形式填充 **hierarchyid** 列。 在本课程中，您将由新表开始，使用分层方法插入数据。 然后，您将使用分层方法查询和操作数据。 

## <a name="prerequisites"></a>必备条件  
若要完成本教程，需要 SQL Server Management Studio、针对运行 SQL Server 的服务器的访问权限以及 AdventureWorks 数据库。

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks2017 示例数据库](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)。

此处提供在 SSMS 中还原数据库的说明：[还原数据库](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>使用 hierarchyid 数据类型创建表
下例创建了一个名为 EmployeeOrg 的表，该表包含雇员数据及其报告层次结构。 本例在 AdventureWorks2017 数据库中创建该表，但这是可选操作。 为了简化该示例，此表仅包含五列：  
  
-   OrgNode 是一个存储层次结构关系的 **hierarchyid** 列。   
-   OrgLevel 是一个计算列，它基于存储层次结构中的各节点级别的 OrgNode 列。 它将用于广度优先索引。  
-   EmployeeID 包含用于诸如工资单等应用程序的典型雇员标识号。 在新应用程序的开发过程中，应用程序可以使用 OrgNode 列，不需要这个单独的 EmployeeID 列。   
-   EmpName 包含雇员的姓名。    
-   Title 包含雇员的职位。  

## <a name="create-the-employeeorg-table"></a>创建 EmployeeOrg 表  
  
1.  在“查询编辑器”窗口中，运行以下代码来创建 `EmployeeOrg` 表。 将 `OrgNode` 列指定为具有聚集索引的主键，即创建了深度优先索引：  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
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
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
现在即可为该表填充数据。 下一个任务将通过使用分层方法来填充该表。   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>使用分层方法填充层次结构表
AdventureWorks2017 有 8 名在市场营销部门工作的雇员。 雇员的层次结构如下所示：  
  
**David**（ **EmployeeID** 为 6）是市场营销经理。 **David**下辖三名市场营销专员，他们分别是：  
  
-   **Sariya**， **EmployeeID** 46  
  
-   **John**， **EmployeeID** 271  
  
-   **Jill**， **EmployeeID** 119  
  
销售助理 **Wanida** (**EmployeeID** 269)，是 **Sariya**的下属；销售助理 **Mary** (**EmployeeID** 272)，是 **John**的下属。  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>插入层次结构树的根  
  
1.  下例将市场营销经理 **David** 插入层次结构的根处的表中。 **OrdLevel** 列是一个计算列。 因此，它不是 INSERT 语句的一部分。 第一条记录使用 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) 方法将其自身填充为层次结构的根。  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  执行以下代码来检查表中的初始行：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
如上一课所述，使用 `ToString()` 方法将 **hierarchyid** 数据类型转换成更易于理解的格式。  
  
### <a name="insert-a-subordinate-employee"></a>插入下属雇员  
  
1.  **Sariya** 是 **David**的下属。 若要插入 **Sariya** 的节点，必须创建数据类型为 **hierarchyid** 的适当的 **OrgNode**值。 下面的代码创建一个数据类型为 **hierarchyid** 的变量，并用表的根 OrgNode 值填充此变量。 然后使用该变量和 [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) 方法插入从属节点行。 `GetDescendant` 采用两个参数。 检查以下选项的参数值：  
  
    -   如果父级为 NULL， `GetDescendant` 返回 NULL。  
    -   如果父级不为 NULL，并且 child1 和 child2 为 NULL， `GetDescendant` 返回父级的子级。  
    -   如果父级和 child1 不为 NULL，而 child2 为 NULL， `GetDescendant` 返回一个大于 child1 的父级的子级。   
    -   如果父级和 child2 不为 NULL，而 child1 为 NULL， `GetDescendant` 返回一个小于 child2 的父级的子级。   
    -   如果父级、child1 和 child2 都不为 NULL， `GetDescendant` 返回一个大于 child1 且小于 child2 的父级的子级。  
  
    下面的代码使用根父级的 `(NULL, NULL)` 参数，因为除了根外，表中尚未存在其他行。 执行下面的代码以插入 **Sariya**：  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  从第一个过程重复查询来对表进行查询并查看项的显示方式：  
  
    ```sql  
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
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>创建输入新节点的过程  
  
1.  若要简化数据的输入，请创建下面的存储过程以向 **EmployeeOrg** 表添加雇员。 该过程接受有关将要添加的雇员的输入值。 这包括新雇员的上司的 **EmployeeID** 、新雇员的 **EmployeeID** 号以及他们的名字和职位。 该过程使用 `GetDescendant()` 和 [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) 方法。 执行下面的代码以创建此过程：  
  
    ```sql  
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
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  再次执行下面的查询以检查 **EmployeeOrg** 表中的行：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
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

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>使用层次结构方法查询层次结构表
由于 HumanResources.EmployeeOrg 表已完全填充，此任务将说明如何使用某些分层方法来查询层次结构。  
  
### <a name="find-subordinate-nodes"></a>查找从属节点  
  
1.  Sariya 有一名下属雇员。 若要查询 Sariya 的下属，请执行使用 [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) 方法的以下查询：  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    结果同时列出 Sariya 和 Wanida。 Sariya 的列出原因是她是 0 级后代。 Wanida 是 1 级后代。  
  
2.  也可以使用 [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) 方法查询此信息。 `GetAncestor` 对尝试返回的级别采用了一个参数。 由于 Wanida 位于 Sariya 下面一级，因此使用 `GetAncestor(1)` ，如以下代码所示：  
  
    ```sql  
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
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    这次，还收到向 David 报告的位于两个级别之下的 Mary。  
  
## <a name="use-getroot-and-getlevel"></a>使用 GetRoot 和 GetLevel  
  
1.  随着层次结构不断扩大，更加难于确定成员在层次结构中的位置。 使用 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 方法可查明每一行下方有多少个级别处于层次结构中。 执行下面的代码以查看所有行的下属级别：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  使用 [GetRoot](../../t-sql/data-types/getroot-database-engine.md) 方法查找层次结构中的根节点。 下面的代码返回一个作为根的行：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>使用分层方法对层次结构表中的数据重新排序
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
重新组织层次结构是一项常见的维护任务。 在此任务中，使用包含 [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) 方法的 UPDATE 语句首先将一行移到层次结构的新位置。 然后，我们会将整个子树移到一个新位置。  
  
`GetReparentedValue` 方法使用两个参数。 第一个参数用于描述要修改的层次结构部分。 例如，如果层次结构为 **/1/4/2/3/** ，希望更改 **/1/4/** 部分，将层次结构变为 **/2/1/2/3/**，后两个节点 (**2/3/**) 保持不变，则必须提供要更改的节点 (**/1/4/**) 作为第一个参数。 第二个参数提供新的层次结构级别，在示例中为 **/2/1/**。 这两个参数无须包含相同的级别数。  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>将一行移到层次结构中的新位置上  
  
1.  当前，Wanida 向 Sariya 报告。 在此过程中，将 Wanida 从其当前的节点 **/1/1/** 移出，使她可以向 Jill 报告。 她的新节点将变为 **/3/1/** ，而 **/1/** 成为第一个参数， **/3/** 成为第二个参数。 这些值与 Sariya 和 Jill 的 **OrgNode** 值相对应。 执行下列代码将 Wanida 从 Sariya 的组织移到 Jill 的组织中：  
  
    ```sql  
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
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    现在，Wanida 位于节点 **/3/1/**。  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>重新组织层次结构中的某一部分  
  
1.  为了演示如何同时移动大量人员，请先执行下列代码，添加一个向 Wanida 报告的实习生：  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  现在，Kevin 向 Wanida 报告，Wanida 向 Jill 报告，而 Jill 向 David 报告。 也就是说，Kevin 位于级别 **/3/1/1/**。 若要将 Jill 的所有下属都移到一位新经理之下，需要将 **OrgNode** 为 **/3/** 的所有节点更新为新值。 执行下列代码以便将 Wanida 更新为向 Sariya 负责，但 Kevin 仍向 Wanida 负责：  
  
    ```sql  
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
  
    ```sql  
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
  
