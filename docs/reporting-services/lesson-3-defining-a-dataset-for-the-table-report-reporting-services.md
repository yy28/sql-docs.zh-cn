---
title: 第 3 课：为表报表定义数据集 (Reporting Services) | Microsoft Docs
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eaa2af570ae363e6a48c8d14e5b73c70e6790b5c
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106031"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>第 3 课：为表报表定义数据集 (Reporting Services)

定义数据源后，您需要定义数据集。 在 [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)] 中，在报表中使用的数据包含在“数据集”中。 数据集包括一个指向数据源的指针、将由报表使用的查询、计算字段和变量。

在报表设计器中使用查询设计器来定义数据集。 在本教程中，将创建一个查询，用于从 AdventureWorks2016 数据库中检索销售订单信息。

## <a name="define-a-transact-sql-query-for-report-data"></a>为报表数据定义 Transact-SQL 查询  

1. 在“报表数据”窗格中，选择“新建” > “数据集...”。“数据集属性”对话框将打开，并显示“查询”部分。

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. 在“名称”框中，键入“AdventureWorksDataset”。

3. 在下面选择“使用在我的报表中嵌入的数据集”单选按钮。

4. 从“数据源”下拉框中，选择“AdventureWorks2016”。

5. 有关查询类型，选择“文本”单选按钮。

6. 将以下 Transact-SQL 查询键入（或复制并粘贴）到“查询”文本框中。

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
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
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. （可选）选择“查询设计器”按钮。 查询将在基于文本的“查询设计器”中显示。 通过选择“查询设计器”工具栏上的 ![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png)“运行”按钮，查看查询的结果。 显示的数据集包含来自 AdventureWorks2016 数据库的四个表的六个字段。 查询利用别名等 Transact-SQL 功能。 例如，SalesOrderHeader 表称为 soh。

8. 选择“确定”退出“查询设计器”。

9. 选择“确定”退出“数据集属性”对话框。

“报表数据”窗格将显示 AdventureWorksDataset 数据集和字段。

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>后续步骤

你已成功指定了一个用于检索报表数据的查询。 接下来将创建报表布局。 继续学习[第 4 课：向报表添加表 (Reporting Services)](lesson-4-adding-a-table-to-the-report-reporting-services.md)。

## <a name="see-also"></a>另请参阅

[查询设计工具 (SSRS)](../reporting-services/report-data/query-design-tools-ssrs.md)
[SQL Server 连接类型 (SSRS)](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[教程：编写 Transact-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)
