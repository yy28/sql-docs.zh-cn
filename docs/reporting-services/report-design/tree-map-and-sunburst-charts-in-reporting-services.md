---
title: SQL Server Reporting Services 中的树状图和旭日图 | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 152507403574ae4c699a3aa30a2376c0ed6b2af2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002931"
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Reporting Services 中的树状图和旭日图
[!INCLUDE[feedback-stackoverflow-msdn-connect-md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 树状图和旭日图可视化非常适合用于以可视方式表示分层数据。 本文将概述如何将树状图或旭日图添加到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表中。 文章还包括一个 AdventureWorks 示例查询，帮助入门。  
  
##  <a name="bkmk_treemap_chart"></a> 树状图  

树状图将图表区划分为多个矩形，分别表示数据层次结构的不同级别和相对大小。 该图表类似于树上的分枝，从树干开始，接着划分为越来越小的分枝。 每个矩形被分成更小的矩形，表示层次结构中的下一级。 顶级树状图矩形表示为最大的矩形，位于图表左上角，最小的矩形位于右下角。  在一个矩形内，下一个更高级也用从左上角到右下角的矩形表示。  

例如，在以下示例树状图中，西南区域最大，德国最小。 在西南部，自行车路都比山地自行车路大。  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>插入树状图与设置示例 AdventureWorks 数据  
   
> [!NOTE]
> 在向报表添加图表前，请创建数据源和数据集。  有关示例数据和示例查询，请参阅[示例 AdventureWorks 数据](#bkmk_sample_data)。  
  
1.  右键单击设计图面，然后选择“插入” > “图表”。 选择“树状图”图标。

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  重新定位并调整图表的大小。 为了配合示例数据，最好选择宽度为 5 英寸的图表。  
  
3.  从示例数据中添加以下字段︰  
  
    * 值：LineTotal
    * 类别组（按下面的顺序）：
        1. CategoryName
        2. SubcategoryName
    * 序列组：TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要优化常规形状树状图的页面大小，请将图例位置设置为底部。  
  
5.  若要添加显示子类别和行总计的工具提示，请右键单击“LineTotal”，然后单击“序列属性”。  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     将“工具提示”属性设为以下值：  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    有关详细信息，请参阅[显示序列的相关工具提示（报表生成器和 SSRS）](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)。  
  
6.  将默认图表标题改为“根据区域划分的的销售”。  
  
7.  字体的大小、整体图表区的大小和特定矩形的大小会影响显示的标签值的数目。 要查看更多标签，请将 LineTotal 的“标签字体”属性从默认的 8 磅改为 10 磅。  
  
  
##  <a name="bkmk_sunburst_chart"></a> 旭日图  
 
在旭日图中，通过一系列环表示层次结构。 最高级别的层次结构位于中心，而较低级别的层次结构为中心之外显示的环。  层次结构的最低级别是外部环。  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>插入旭日图与设置示例 AdventureWorks 数据  
> [!NOTE] 
> 在向报表添加图表前，请创建数据源和数据集。 有关示例数据和示例查询，请参阅[示例 AdventureWorks 数据](#bkmk_sample_data)。  
  
1.  右键单击设计图面，然后选择“插入” > “图表”。 选择“旭日图”图标。
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  重新定位并调整图表的大小。 为了配合示例数据，最好选择宽度为 5 英寸的图表。  
  
3.  从示例数据中添加以下字段︰  

    * 值：LineTotal
    * 类别组（按下面的顺序）：
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * 序列组：TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要优化常规形状旭日图的页面大小，请将图例位置设置为底部。  
  
5.  将默认图表标题改为“出于销售原因根据区域划分的销售”。  
  
6. 若要将类别组的值作为标签添加到旭日图中，请设置标签属性 Visible = true 和 UseValueAsLabel=False。<br /><br /> 字体的大小、整体图表区的大小和特定矩形的大小会影响显示的标签值。  要查看更多标签，请将 LineTotal 的“标签字体”属性从默认的 8 磅改为 10 磅。

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  如果希望使用不同的颜色范围，请更改图表的“调色板”  属性。  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> 示例 AdventureWorks 数据  
 本部分包括一个示例查询和在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 中创建数据源和数据集的基本步骤。 如果报表已包含数据源和数据集，可以跳过本部分。  
  
 查询将返回 AdventureWorks 销售订单详细信息数据与销售区域、产品类别、产品子类别和销售原因数据。  
  
1.  **获取数据**。  
  
     本部分中的查询基于 Adventureworks 数据库，可从 GitHub：[AdventureWorks 2016 完整数据库备份](https://github.com/Microsoft/sql-server-samples/releases)中下载。  
  
  
2.  **创建数据源**。  
  
    1.  在“报表数据”中，右键单击“数据源”，然后选择“添加数据源”。  
  
    2.  选择“使用我的报表中嵌入的连接” 。  
  
    3.  对于连接类型，请选择“Microsoft SQL Server”。  
  
    4.  输入服务器和数据库的连接字符串。 例如：  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  要验证连接，请选择“测试连接”按钮，然后选择“确定”。  
  
     有关创建数据源的详细信息，请参阅[添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
3.  **创建数据集**。  
  
    1. 在“报表数据”中，右键单击“数据集”，然后选择“添加数据集”。  
  
    2. 选择“使用在我的报表中嵌入的数据集” 。  
  
    3. 选择所创建的数据源。  
  
    4. 选择文本查询类型，然后复制以下查询，并将其粘贴到“查询”文本框中：  
  
        ```  
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    5. 选择“确定”。  
  
     有关创建数据集的详细信息，请参阅[创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)。  
  
  
## <a name="see-also"></a>另请参阅  
* [共享数据集设计视图（报表生成器）](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [显示序列的相关工具提示（报表生成器和 SSRS）](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [教程：Power BI 中的树状图](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [树形图：面向 Office 的 Microsoft Research 数据可视化应用](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

