---
title: 将列从一个表复制到另一个表 (数据库引擎) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d2654485acdebdf3e7e79b23dadd533617ea937
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137517"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>将列从一个表复制到另一个表 (数据库引擎)
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中通过仅复制列定义或者复制定义和数据将列从一个表复制到另一个表。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要复制列，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 当将具有别名数据类型的列从一个数据库复制到另一个数据库时，别名数据类型在目标数据库中可能不可用。 在这种情况下，将为该列分配该数据库中可用的匹配度最高的基数据类型。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>将列定义从一个表复制到另一个表  
  
1.  右键单击相应表，然后单击“设计”，打开要复制的列所在的表以及要复制到的表。  
  
2.  单击包含要复制的列的表的选项卡，然后选择这些列。  
  
3.  在 **“编辑”** 菜单中，单击 **“复制”**。  
  
4.  单击要将列复制到的表的选项卡。  
  
5.  选择要排在插入列之后的列，然后在 **“编辑”** 菜单中，单击 **“粘贴”**。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>将数据从一个表复制到另一个表  
  
1.  按照以上关于复制列定义的说明执行操作。  
  
    > [!NOTE]  
    >  在开始将数据从一个表复制到另一个表之前，请确保目标列中的数据类型与源列的数据类型相兼容。  
  
2.  在对象资源管理器中，右键单击“视图”节点，然后单击“新建视图”。  
  
3.  在 **“查询设计器”** 菜单中，指向 **“更改类型”**，再单击 **“插入结果”**。  
  
4.  在 **“选择插入结果的目标表”** 对话框中选择要将数据复制到的表，再单击 **“确定”**。  
  
     若要在同一个表内复制行，则可将源表作为目标表添加。  
  
    > [!NOTE]  
    >  **查询设计器** 无法事先确定可以更新哪些表和视图。 因此， **“选择插入结果的目标表”** 对话框中的表列表将显示正在查询的数据连接中的所有可用表和视图，甚至显示不能将行复制到其中的表和视图。  
  
5.  右键单击“关系图”窗格的主题，然后在快捷菜单中单击“将表添加到关系图”。  
  
6.  在 **“添加表”** 对话框中选择要从中复制数据的各个表，单击 **“添加”**，再单击 **“关闭”**。  
  
     这些表将以缩略形式显示在“关系图”窗格中。  
  
7.  在缩略表中，选中要从中复制数据的所有列的复选框。  
  
8.  在“条件”窗格的 **“追加”** 列中，为每个目标列选择要从其中复制数据的列。  
  
9. 通过在“条件”窗格中输入搜索条件来指定要复制的行。 有关详细信息，请参阅[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/visual-database-tools.md)。  
  
     如果未指定搜索条件，则源表中的所有行都会复制到目标表中。  
  
10. 若要复制摘要信息，请指定 **“分组依据”** 选项。 有关详细信息，请参阅[汇总或聚合表中所有行的值 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)。  
  
11. 单击 **“执行 SQL”** 按钮以运行该查询。  
  
     在执行“插入结果”查询时，不会在 [“结果”窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中报告任何结果。 但是，会显示一条消息，指出已复制的行数。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>将列定义从一个表复制到另一个表  
  
1.  不能通过使用 Transact-SQL 语句将单独列从一个表复制到另一个现有表。 但是，您可以通过使用 SELECT INTO 在默认文件组中创建一个新表，并将来自查询的结果行插入该表中。 有关详细信息，请参阅 [ INTO 子句 (Transact-SQL)](/sql/t-sql/queries/select-into-clause-transact-sql)。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>将数据从一个表复制到另一个表  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
