---
title: 以 XML 格式保存执行计划 | Microsoft Docs
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
- XML query plans [SQL Server]
- opening execution plans
- XML Showplans [SQL Server]
- execution plans [SQL Server], saving
- saving execution plans
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9ab8e97457ee4dc0aab09dcefc6027f5ae56a709
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125088"
---
# <a name="save-an-execution-plan-in-xml-format"></a>以 XML 格式保存执行计划
  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以将执行计划保存为 XML 文件，也可以打开这些执行计划进行查看。  
  
 若要使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的执行计划功能或使用 XML 显示计划的 SET 选项，用户必须具有执行（要为其生成执行计划的） [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询的相应权限，还必须获得对该查询所引用的所有数据库的 SHOWPLAN 权限。  
  
### <a name="to-save-a-query-plan-by-using-the-xml-showplan-set-options"></a>使用 XML 显示计划的 SET 选项保存查询计划  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，打开查询编辑器并连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  使用以下语句打开 SHOWPLAN_XML：  
  
    ```  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
     若要打开 STATISTICS XML，请使用以下语句：  
  
    ```  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     SHOWPLAN_XML 将会为查询生成编译时查询执行计划信息，但是不会执行查询。 STATISTICS XML 将会为查询生成运行时查询执行计划信息，而且会执行查询。  
  
3.  执行查询。 例如：  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  在“结果”窗格中，右键单击包含查询计划的“Microsoft SQL Server XML 显示计划”，然后单击“将结果另存为”。  
  
5.  在“保存 \<网格或文本> 结果”对话框中的“保存类型”框中，单击“所有文件(\*.\*)”。  
  
6.  在“文件名”框中，提供“\<名称>.sqlplan”格式的名称，然后单击“保存”。  
  
### <a name="to-save-an-execution-plan-by-using-sql-server-management-studio-options"></a>使用 SQL Server Management Studio 选项保存执行计划  
  
1.  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]生成估计的执行计划或实际的执行计划。 有关详细信息，请参阅[显示估计的执行计划](display-the-estimated-execution-plan.md)或[显示实际执行计划](display-an-actual-execution-plan.md)。  
  
2.  在“结果”窗格的“执行计划”选项卡上，右键单击图形执行计划，然后选择“将执行计划另存为”。  
  
     此外，还可以在 **“文件”** 菜单上选择 **“将执行计划另存为”** 。  
  
3.  在“另存为”对话框中，确保将“保存类型”设置为“执行计划文件(\*.sqlplan)”。  
  
4.  在“文件名”框中，提供“\<名称>.sqlplan”格式的名称，然后单击“保存”。  
  
### <a name="to-open-a-saved-xml-query-plan-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中打开保存的 XML 查询计划  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 **“文件”** 菜单上，选择 **“打开”**，然后单击 **“文件”**。  
  
2.  在“打开文件”对话框中，将“文件类型”设置为“执行计划文件(\*.sqlplan)”，以筛选出保存的 XML 查询计划文件的列表。  
  
3.  选择要查看的 XML 查询计划文件，然后单击 **“打开”**。  
  
     此外，还可以在 Windows 资源管理器中双击扩展名为 **.sqlplan**的文件。 该计划便会在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中打开。  
  
## <a name="see-also"></a>请参阅  
 [SET SHOWPLAN_XML (Transact-SQL)](/sql/t-sql/statements/set-showplan-xml-transact-sql)   
 [SET STATISTICS XML (Transact-SQL)](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
  
