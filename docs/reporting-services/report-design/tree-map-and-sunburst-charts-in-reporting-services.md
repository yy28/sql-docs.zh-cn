---
title: "SQL Server Reporting Services 中的树状图和旭日图 |Microsoft 文档"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 5e15fa8674a09821becd437e78cfb0bb472e3bc8
ms.openlocfilehash: 50224e926c08951887a6423ab1c95eb7ac23a944
ms.contentlocale: zh-cn
ms.lasthandoff: 10/30/2017

---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>在 Reporting Services 中的树状图和旭日图
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

SQL Server[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]树状图和旭日图可视化非常适合用于以可视方式表示分层数据。 本文将简要介绍如何添加到一个树状图或旭日图[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]报表。 文章还包括 AdventureWorks 示例查询，以帮助你开始。  
  
##  <a name="bkmk_treemap_chart"></a>树状图图表  

树状图图表将图表区划分为矩形，分别表示的不同级别和数据层次结构的相对大小。 该图表类似于树上的分枝，从树干开始，接着划分为越来越小的分枝。 每个矩形被分成较小的矩形，分别表示层次结构中的下一个级别。 顶级树状图矩形左上角到右下角中的最小矩形图的最大的矩形排列。  在一个矩形内，下一个更高级也用从左上角到右下角的矩形表示。  

例如，在以下示例树状图的图中，西南区域最大，德国是最小。 在西南部，自行车路都比山地自行车路大。  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>若要插入的树状图图表和设置示例 AdventureWorks 数据  
   
> [!NOTE]
> 向报表添加图表之前，创建数据源和数据集。  示例数据和示例查询，请参阅[示例 AdventureWorks 数据](#bkmk_sample_data)。  
  
1.  右键单击设计图面，然后选择**插入** > **图表**。 选择**树状图**图标。

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  重新定位并调整图表的大小。 若要使用示例数据，宽度为 5 英寸的图表是一个不错的起点。  
  
3.  从示例数据中添加以下字段︰  
  
    * **值**: LineTotal
    * **类别组**（按以下顺序）：
        1. CategoryName
        2. SubcategoryName
    * **序列组**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要优化常规形状的树状图的页面大小，请将图例位置设置为底部。  
  
5.  若要添加工具提示显示 subcategory 和行合计，右键单击**LineTotal**，然后选择**序列属性**。  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     设置**工具提示**为以下值的属性：  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    有关详细信息，请参阅[显示一系列 &#40; 上的工具提示报表生成器和 SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  更改默认图表标题改为**分类按地区的销售**。  
  
7.  字体的大小、整体图表区的大小和特定矩形的大小会影响显示的标签值的数目。 若要查看更多的标签，更改**标签字体**属性**LineTotal**到**10pt**从默认值**8 磅**。  
  
  
##  <a name="bkmk_sunburst_chart"></a>旭日图  
 
在旭日图中，由一系列圆圈表示层次结构。 层次结构的最高级别位于中心，和较低级别的层次结构是显示在中心之外的环。  层次结构的最低级别是外部环。  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>若要插入旭日图并设置示例 AdventureWorks 数据  
> [!NOTE] 
> 向报表添加图表之前，创建数据源和数据集。 示例数据和示例查询，请参阅[示例 AdventureWorks 数据](#bkmk_sample_data)。  
  
1.  右键单击设计图面，然后选择**插入** > **图表**。 选择**旭日图**图标。
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  重新定位并调整图表的大小。 若要使用示例数据，宽度为 5 英寸的图表是一个不错的起点。  
  
3.  从示例数据中添加以下字段︰  

    * **值**: LineTotal
    * **类别组**（按以下顺序）：
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **序列组**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要优化常规形状旭日图的页面大小，请将图例位置设置为底部。  
  
5.  更改默认图表标题改为**根据区域划分销售原因分类销售**。  
  
6. 若要将类别组的值作为标签添加到旭日图中，设置标签属性**可见 = true**和**UseValueAsLabel = false**。<br /><br /> 字体的大小、整体图表区的大小和特定矩形的大小会影响显示的标签值。  若要查看更多的标签，更改**标签字体**属性**LineTotal**到**10pt**从默认值**8 磅**。

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  如果希望使用不同的颜色范围，请更改图表的“调色板”  属性。  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a>示例 AdventureWorks 数据  
 本部分包括一个示例查询和创建数据源和中的数据集的基本步骤[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]。 如果报表已包含数据源和数据集，则可以跳过本节。  
  
 查询将返回 AdventureWorks 销售订单详细信息数据与销售区域、 产品类别、 产品子类别和销售原因数据。  
  
1.  **获取数据**。  
  
     本部分中的查询基于 AdventureWorks 数据库，这是可从 GitHub 下载： [AdventureWorks 2016 完整数据库备份](https://github.com/Microsoft/sql-server-samples/releases)。  
  
  
2.  **创建数据源**。  
  
    1.  下**报表数据**，右键单击**数据源**，然后选择**添加数据源**。  
  
    2.  选择“使用我的报表中嵌入的连接” 。  
  
    3.  对于连接类型，选择**Microsoft SQL Server**。  
  
    4.  输入你的服务器和数据库的连接字符串。 例如：  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  若要验证连接，请选择**测试连接**按钮，，然后选择**确定**。  
  
     有关创建数据源的详细信息，请参阅[添加并验证数据连接 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **创建数据集**。  
  
    1. 下**报表数据**，右键单击**数据集**，然后选择**添加数据集**。  
  
    2. 选择“使用在我的报表中嵌入的数据集” 。  
  
    3. 选择你创建的数据源。  
  
    4. 选择**文本**查询类型，然后复制并粘贴到以下查询**查询**文本框：  
  
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
  
     有关创建数据集的详细信息，请参阅[创建共享数据集或嵌入数据集 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>另请参阅  
* [共享数据集设计视图 &#40;报表生成器 &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [上一系列 &#40; 显示工具提示报表生成器和 SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [教程： Power BI 中的树状图](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [树形图：面向 Office 的 Microsoft Research 数据可视化应用](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


