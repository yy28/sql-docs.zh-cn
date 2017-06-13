---
title: "树形图和旭日图 Reporting Services 中的 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e09afe4634c02db6e74413e7c1c10565450b3559
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="tree-map-and-sunburst-charts-in-reporting-services"></a>Reporting Services 中的树形图和旭日图
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 树形图和旭日图可视化非常适合用于以可视方式表示分层数据。   本主题将概述如何将树形图或旭日图添加到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表中。 本主题还包括示例 Adventureworks 查询，帮助您入门。  
  
##  <a name="bkmk_treemap_chart"></a> 树形图  
 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
  
 树形图将图表区划分为多个矩形，分别表示数据层次结构的不同级别和相对大小。 该图表类似于树上的分枝，从树干开始，接着划分为越来越小的分枝。 每个矩形被分成更小的矩形，表示层次结构中的下一级。 顶级树形图矩形表示为最大的矩形，位于图表左上角，最小的矩形位于右下角。  在一个矩形内，下一个更高级也用从左上角到右下角的矩形表示。  
  
 例如，在以下示例树形图中，西南区域最大，德国最小。 在西南部，自行车路都比山地自行车路大。  
  
 ![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-tree-map-chart-and-configure-for-the-sample-adventureworks-data"></a>插入树形图与配置示例 Adventureworks 数据  
 **注意** ：在向报表添加图表前，请创建数据源和数据集。  有关示例数据和示例查询，请参阅本主题中的 [示例 AdventureWorks 数据](#bkmk_sample_data) 部分。  
  
1.  在设计图面上单击右键，单击“插入”，然后单击“图表”。  
  
     选择树状图![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")。  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  重新定位并调整图表的大小。   为了配合示例数据，最好选择宽度为 5 英寸的图表。  
  
3.  从示例数据中添加以下字段︰  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**值：** LineTotal<br /><br /> **类别组：** 按照以下顺序添加：<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> **序列组：** TerritoryName|  
  
4.  若要优化常规形状树形图的页面大小，将图例位置设置为底部。  
  
5.  若要添加显示子类别和行总计的工具提示，请右键单击“LineTotal”，然后单击“系列属性”。  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     按如下所述设置“工具提示”  属性：  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
     有关详细信息，请参阅[在序列上显示工具提示（报表生成器和 SSRS）](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)。  
  
6.  将默认图表标题改为“根据区域划分的的销售”。  
  
7.  字体的大小、整体图表区的大小和特定矩形的大小会影响显示的标签值的数目。  若要查看更多标签，请将 LineTotal 标签字体属性更改为 10 磅，而不是默认的 8 磅。  
  
  
##  <a name="bkmk_sunburst_chart"></a> 旭日图  
 ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
 在旭日图中，用一系列圆圈来表示层次结构，层次结构中的最高级别位于中心位置，较低级别则显示为中央外的环。  层次结构的最低级别是外部环。  
  
 ![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-configure-for-the-sample-adventureworks-data"></a>插入旭日图与配置示例 Adventureworks 数据  
 **注意** ：在向报表添加图表前，请创建数据源和数据集。  有关示例数据和示例查询，请参阅本主题中的 [示例 AdventureWorks 数据](#bkmk_sample_data) 部分。  
  
1.  在设计图面上单击右键，单击“插入”，然后单击“图表”。  
  
     选择旭日图![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")。  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  重新定位并调整图表的大小。   为了配合示例数据，最好选择宽度为 5 英寸的图表。  
  
3.  从示例数据中添加以下字段︰  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**值：** LineTotal<br /><br /> **类别组：** 按照以下顺序添加：<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName,<br /><br /> 3) SalesReasonName<br /><br /> **序列组：** TerritoryName。|  
  
4.  若要优化常规形状旭日图的页面大小，请将图例位置设置为底部。  
  
5.  将默认图表标题改为“出于销售原因根据区域划分的销售”。  
  
6.  |||  
    |-|-|  
    |![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")|若要将类别组的值作为标签添加到旭日图中，请设置标签属性 **Visible** = true 和 **UseValueAsLabel**=False。<br /><br /> 字体的大小、整体图表区的大小和特定矩形的大小会影响显示的标签值。  若要查看更多标签，请将 LineTotal 标签字体属性更改为 8 磅，而不是默认的 10 磅。|  
  
7.  如果希望使用不同的颜色范围，请更改图表的“调色板”  属性。  
  
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> 示例 AdventureWorks 数据  
 本部分包括一个示例查询和在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]中创建数据源和数据集的基本步骤。 如果你的报表已包含数据源和数据集，可以跳过本部分。  
  
 查询将返回 Adventureworks 销售订单详细信息数据与销售区域、产品类别、产品子类别和销售原因数据。  
  
1.  **获取数据︰**  
  
     本部分中的查询基于 Adventureworks 数据库，可从  [Adventure Works 2014 完整数据库备份](https://msftdbprodsamples.codeplex.com/releases/view/125550)中下载。  
  
     有关如何安装数据库的详细信息，请参阅 [如何安装 Adventure Works 2014 示例 Databases.pdf](https://msftdbprodsamples.codeplex.com/releases/view/125550)。  
  
2.  **创建数据源：**  
  
    1.  在“报表数据”窗格中，右键单击“数据源”，然后单击“添加数据源”。  
  
    2.  选择“使用我的报表中嵌入的连接” 。  
  
    3.  选择 **Microsoft SQL Server**的连接类型。  
  
    4.  键入服务器和数据库的连接字符串，例如下面的字符串︰  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2014  
        ```  
  
    5.  一个不错的做法是用“测试连接”  按钮进行验证，然后单击“确定” 。  
  
     有关创建数据源的详细信息，请参阅[添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
3.  **创建数据集：**  
  
    -   在“报表数据”窗格中，右键单击“数据集”，然后单击“添加数据集”。  
  
    -   选择“使用在我的报表中嵌入的数据集” 。  
  
    -   选择在前面的过程中创建的数据源。  
  
    -   选择“文本”  查询类型，然后将以下查询复制并粘贴到“查询”  文本框中：  
  
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
  
    -   单击“确定” 。  
  
     有关创建数据集的详细信息，请参阅[创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [共享数据集设计视图（报表生成器）](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [在序列上显示工具提示（报表生成器和 SSRS）](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)   
 [教程︰Power BI 中的树形图](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)   
 [树形图︰Microsoft Research 面向 Office 的数据可视化应用](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


