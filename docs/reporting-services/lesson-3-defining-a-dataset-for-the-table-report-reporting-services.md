---
title: "第 3 课： 定义数据集的表报表 (Reporting Services) |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
caps.latest.revision: 53
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce3439962e88c24980615d2f2648b56cc88505fa
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>第 3 课：为表报表定义数据集 (Reporting Services)
定义数据源后，您需要定义数据集。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中，在报表中使用的数据包含在“数据集”中。 数据集包括一个指向数据源的指针、将由报表使用的查询以及计算字段和变量。  
  
在报表设计器中使用查询设计器来设计数据集。 在本教程中，将创建一个查询，用于从 [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库中检索销售订单信息。  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>为报表数据定义 Transact-SQL 查询  
  
1.  在“报表数据”窗格中，单击“新建”，然后单击“数据集…”。 此时将打开 **“数据集属性”** 对话框。  
  
2.  在“名称”框中，键入 **AdventureWorksDataset**。  
  
3.  单击“使用在我的报表中嵌入的数据集”。  
  
4.  选择在前面的课程中创建的数据源 [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]。   
5. 将“查询类型”选择为“文本”。  
  
6.  将以下 Transact-SQL 查询键入（或复制并粘贴）到“查询”框中。  
  
    ```  
    SELECT   
       soh.OrderDate AS [Date],   
       soh.SalesOrderNumber AS [Order],   
       pps.Name AS Subcat, pp.Name as Product,    
       SUM(sd.OrderQty) AS Qty,  
       SUM(sd.LineTotal) AS LineTotal  
    FROM Sales.SalesPerson sp   
       INNER JOIN Sales.SalesOrderHeader AS soh   
          ON sp.BusinessEntityID = soh.SalesPersonID  
       INNER JOIN Sales.SalesOrderDetail AS sd   
          ON sd.SalesOrderID = soh.SalesOrderID  
       INNER JOIN Production.Product AS pp   
          ON sd.ProductID = pp.ProductID  
       INNER JOIN Production.ProductSubcategory AS pps   
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID  
       INNER JOIN Production.ProductCategory AS ppc   
          ON ppc.ProductCategoryID = pps.ProductCategoryID  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,   
       soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'  
    ```  
  
7.  （可选）单击“查询设计器”按钮。 查询将在基于文本的查询设计器中显示。 通过单击“编辑为文本”，可以切换到图形查询设计器。 通过单击查询设计器工具栏上的“运行![ssrs_querydesigner_run](../reporting-services/media/ssrs-querydesigner-run.png)”按钮，查看查询的结果。  
  
    将看到来自 [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库中四个不同表的六个字段的数据。 查询利用别名等 Transact-SQL 功能。 例如，SalesOrderHeader 表称为 soh 。  
  
8.  单击“确定”退出查询设计器。  
  
9.  单击“确定”退出“数据集属性”对话框。  
  
    此时将在“报表数据”窗格中显示 **AdventureWorksDataset** 数据集和字段。  
    ![ssrs_adventureworksdataset](../reporting-services/media/ssrs-adventureworksdataset.png)  
  
## <a name="next-task"></a>下一个任务  
您已成功指定了一个用于检索报表数据的查询。 接下来将创建报表布局。 请参阅[第 4 课：向报表添加表 (Reporting Services)](../reporting-services/lesson-4-adding-a-table-to-the-report-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
[查询设计工具 (SSRS)](../reporting-services/report-data/query-design-tools-ssrs.md)  
[SQL Server 连接类型 (SSRS)](../reporting-services/report-data/sql-server-connection-type-ssrs.md)  
[教程：编写 Transact-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
  


