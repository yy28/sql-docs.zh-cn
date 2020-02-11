---
title: 创建筛选索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- filtered indexes [SQL Server], about filtered indexes
- designing indexes [SQL Server], filtered
- filtered indexes [SQL Server]
- nonclustered indexes [SQL Server], filtered
- indexes [SQL Server], filtered
ms.assetid: 25e1fcc5-45d7-4c53-8c79-5493dfaa1c74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de9a9d71a90f33db85636b1bd0344023f1a86c91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63155385"
---
# <a name="create-filtered-indexes"></a>创建筛选索引
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建筛选索引。 筛选索引是一种经过优化的非聚集索引，尤其适用于涵盖从定义完善的数据子集中选择数据的查询。 筛选索引使用筛选谓词对表中的部分行进行索引。 与全表索引相比，设计良好的筛选索引可以提高查询性能、减少索引维护开销并可降低索引存储开销。  
  
 筛选索引与全表索引相比具有以下优点：  
  
-   **提高了查询性能和计划质量**  
  
     设计良好的筛选索引可以提高查询性能和执行计划质量，因为它比全表非聚集索引小并且具有经过筛选的统计信息。 与全表统计信息相比，经过筛选的统计信息更加准确，因为它们只涵盖筛选索引中的行。  
  
-   **减少了索引维护开销**  
  
     仅在数据操作语言 (DML) 语句对索引中的数据产生影响时，才对索引进行维护。 与全表非聚集索引相比，筛选索引减少了索引维护开销，因为它更小并且仅在索引中的数据更改时才进行维护。 筛选索引的数量可以非常多，特别是在其中包含很少更改的数据时。 同样，如果筛选索引只包含频繁修改的数据，则索引大小较小时可以减少更新统计信息的开销。  
  
-   **减少了索引存储开销**  
  
     在没必要创建全表索引时，创建筛选索引可以减少非聚集索引的磁盘存储开销。 可以使用多个筛选索引替换一个全表非聚集索引而不会明显增加存储需求。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [设计注意事项](#Design)  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **创建筛选索引，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Design"></a> 设计注意事项  
  
-   在列中只有少量相关值需要查询时，可以针对值的子集创建筛选索引。 例如，当列中的值大部分为 NULL 并且查询只从非 NULL 值中进行选择时，可以为非 NULL 数据行创建筛选索引。 由此得到的索引与对相同键列定义的全表非聚集索引相比，前者更小且维护开销更低。  
  
-   表中含有异类数据行时，可以为一种或多种类别的数据创建筛选索引。 通过将查询范围缩小为表的特定区域，这可以提高针对这些数据行的查询性能。 此外，由此得到的索引与全表非聚集索引相比，前者更小且维护开销更低。  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   不能对视图创建筛选索引。 但是，查询优化器可以从对视图中引用的表定义的筛选索引中获益。 对于从视图中选择数据的查询，如果查询结果正确，查询优化器会考虑对此查询使用筛选索引。  
  
-   筛选索引与索引视图相比，具有以下优点：  
  
    -   减少了索引维护开销。 例如，相对于索引视图而言，查询处理器使用更少的 CPU 资源便可更新筛选的索引。  
  
    -   改善了计划质量。 例如，在查询编译期间，查询优化器考虑使用筛选的索引的情况要比考虑使用等效的索引视图的情况多。  
  
    -   联机索引重新生成。 您可以在筛选的索引可用于查询时重新生成它们。 索引视图不支持联机索引重新生成。 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql) 的 REBUILD 选项。  
  
    -   非唯一索引。 筛选索引可以是非唯一的，而索引视图必须是唯一的。  
  
-   筛选索引是针对一个表定义的，仅支持简单比较运算符。 如果需要引用多个表或具有复杂逻辑的筛选表达式，则应创建视图。  
  
-   如果筛选索引表达式等效于查询谓词并且查询并未在查询结果中返回筛选索引表达式中的列，则筛选索引表达式中的列不需要作为筛选索引定义中的键或包含列。  
  
-   如果查询谓词在不与筛选索引表达式等效的比较中使用了筛选索引表达式中的某列，则该列应为筛选索引定义中的键或包含列。  
  
-   如果筛选索引表达式中的某列在查询结果集中，则该列应为筛选索引定义中的键或包含列。  
  
-   表的聚集索引键不需要是筛选索引定义中的键或包含列。 聚集索引键自动包含在所有非聚集索引（包括筛选索引）中。  
  
-   如果筛选索引结果的筛选索引表达式中指定的比较运算符会导致隐式或显式数据转换，则转换发生在比较运算符的左边时，会出现错误。 解决方法是在比较运算符的右边编写包含数据转换运算符（CAST 或 CONVERT）的筛选索引表达式。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 要求对表或视图具有 ALTER 权限。 用户必须是 **sysadmin** 固定服务器角色的成员，或者是 **db_ddladmin** 和 **db_owner** 固定数据库角色的成员。 若要修改筛选索引表达式，请使用 CREATE INDEX WITH DROP_EXISTING。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-filtered-index"></a>创建筛选索引  
  
1.  在对象资源管理器中，单击加号以便展开包含您要创建筛选索引的表的数据库。  
  
2.  单击加号以便展开 **“表”** 文件夹。  
  
3.  单击加号以便展开您要创建筛选索引的表。  
  
4.  右键单击“索引”文件夹，指向“新建索引”，然后选择“非群集索引…”    。  
  
5.  在 **“新建索引”** 对话框的 **“常规”** 页中，在 **“索引名称”** 框中输入新索引的名称。  
  
6.  在“索引键列”下，单击“添加…”   。  
  
7.  在 "**从**_Table_name_中选择列" 对话框中，选中要添加到唯一索引的一个或多个表列的复选框。  
  
8.  单击“确定”。   
  
9. 在“筛选器”页的“筛选表达式”下，输入要用于创建筛选索引的 SQL 表达式********。  
  
10. 单击“确定”。   
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-filtered-index"></a>创建筛选索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Looks for an existing filtered index named "FIBillOfMaterialsWithEndDate"  
    -- and deletes it from the table Production.BillOfMaterials if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
        WHERE name = N'FIBillOfMaterialsWithEndDate'  
        AND object_id = OBJECT_ID (N'Production.BillOfMaterials'))  
    DROP INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials  
    GO  
    -- Creates a filtered index "FIBillOfMaterialsWithEndDate"  
    -- on the table Production.BillOfMaterials   
    -- using the columms ComponentID and StartDate.  
  
    CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials (ComponentID, StartDate)  
        WHERE EndDate IS NOT NULL ;  
    GO  
    ```  
  
     以上筛选索引对下面的查询有效。 您可以显示查询执行计划，以确定查询优化器是否使用了该筛选索引。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ProductAssemblyID, ComponentID, StartDate   
    FROM Production.BillOfMaterials  
    WHERE EndDate IS NOT NULL   
        AND ComponentID = 5   
        AND StartDate > '01/01/2008' ;  
    GO  
    ```  
  
#### <a name="to-ensure-that-a-filtered-index-is-used-in-a-sql-query"></a>确保在 SQL 查询中使用筛选索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
        WITH ( INDEX ( FIBillOfMaterialsWithEndDate ) )   
    WHERE EndDate IN ('20000825', '20000908', '20000918');   
    GO  
    ```  
  
 有关详细信息，请参阅[CREATE INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
  
