---
title: 教程：地图报表（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8fe9eaf39f101e6f64946e7c60a04765e4099d5a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946933"
---
# <a name="tutorial-map-report-report-builder"></a>教程：地图报表 （报表生成器）
  本教程旨在帮助您了解地图功能，您可以使用该功能针对地理背景显示报表数据。  
  
 地图以空间数据为基础，这些数据通常包含点、线条和多边形。 例如，多边形可以表示国家/地区轮廓，线条可以表示道路，而点则可以表示市县所在位置。 各种类型的空间数据作为一组地图元素显示在单独的地图层上。  
  
 若要改变地图元素的外观，可以指定一个字段，通过字段值将地图元素与数据集中分析数据相匹配。 还可以定义相关规则，依据数据范围改变颜色、大小、或其他属性。  
  
 本教程中，将生成一个地图报表，该报表显示了纽约州各县内的商店位置。  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将学习如何执行下列操作：  
  
1.  [使用地图向导从多边形层创建地图](#Map)  
  
2.  [添加地图点层以显示商店位置](#PointLayer)  
  
3.  [添加地图线条层以显示路线](#LineLayer)  
  
4.  [添加必应地图图块背景](#TileLayer)  
  
5.  [将层设置为透明](#Transparent)  
  
6.  [改变县颜色根据销售](#Vary)  
  
    1.  [空间数据和分析数据之间建立关系](#Relationship)  
  
    2.  [多边形指定颜色规则](#ColorRules)  
  
    3.  [在色阶中的数据的格式设置为货币](#ColorScale)  
  
    4.  [创建新图例](#NewLegend)  
  
    5.  [将图例与颜色规则](#Associate)  
  
    6.  [清除的不含数据的县的颜色](#NoData)  
  
7.  [添加自定义点](#CustomPoint)  
  
8.  [将地图视图居中](#CenterView)  
  
9. [添加报表标题](#Title)  
  
10. [保存报表](#Save)  
  
> [!NOTE]  
>  在本教程中，将向导的多个步骤合并为两个过程：一个用于创建数据集，一个用于创建表。 有关如何转到报表服务器、选择数据源、创建数据集和运行向导的分步说明，请参阅本系列教程中的第一个教程：[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 估计的时间才能完成本教程中：30 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Map"></a> 1.通过地图向导使用多边形层创建地图  
 从地图库向报表中添加地图。 该地图具有一个层，此层显示了纽约州中的各个县。 各县的形状为根据地图库中的地图内嵌入的空间数据得出的多边形。  
  
#### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>使用地图向导在新报表中添加地图  
  
1.  单击**启动**，依次指向**程序**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**报表生成器**，然后单击**报表生成器**。  
  
     此时将显示“入门”对话框。  
  
    > [!NOTE]  
    >  如果未显示入门对话框中，从报表生成器按钮，单击**新建**。  
  
2.  在左窗格中，确认**报表**处于选中状态。  
  
3.  在右窗格中，单击“地图向导”。  
  
4.  单击 **“创建”**。  
  
5.  **选择空间数据的来源**页上，确认**地图库**处于选中状态。  
  
6.  在地图库窗格中，展开**州/按县**下**USA**，然后单击**纽约**。  
  
     此时，“地图预览”窗格将显示纽约的县地图。  
  
7.  单击“下一步” 。  
  
8.  上**选择空间数据和地图视图选项**页上，接受默认值。 默认情况下，来自地图库的地图元素将自动嵌入到报表定义中。  
  
9. 单击“下一步” 。  
  
10. 在“选择地图可视化”页上，确认已选中“基本地图”，然后单击“下一步”。  
  
11. 在“选择颜色主题和数据可视化”页上，选择“显示标签”选项。  
  
12. 如果已选择，则清除“单色图”选项。  
  
13. 从**数据字段**下拉列表中，单击 #COUNTYNAME。 向导中的“地图预览”窗格显示以下各项：  
  
    -   一个标题，其文本为“地图标题”。  
  
    -   一个地图，显示纽约的各个县，其中每个县都用一种不同的颜色表示，且县名称出现在县区域上方适合的位置。  
  
    -   一个图例，包含标题和项 1 至 5 的列表。  
  
    -   一个色阶，包含值 0 到 160 但没有颜色。  
  
    -   一个距离宽度，显示公里数 (km) 和英里数 (mi)。  
  
14. 单击 **“完成”**。  
  
     此时，将向设计图面添加一个地图。  
  
15. 单击地图以选择它并显示**地图层窗格**。 **地图层窗格**显示了一个多边形层的层类型**嵌入**。 每个县都是该层上的一个嵌入地图元素。  
  
    > [!NOTE]  
    >  如果没有看到**地图层**窗格中，它可能会显示您当前视图之外。 请使用位于“设计”视图窗口底部的滚动条来更改视图。 或者，在**视图**选项卡上，清除**属性**或**报表数据**选项，以提供更多的设计图面区域。  
  
16. 右键单击地图标题，然后单击**Title 属性**。  
  
17. 将标题文本替换为**应用商店的销售额**。  
  
18. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
19. 预览报表。  
  
 呈现的报表显示地图标题、地图以及距离刻度。 各县位于地图多边形层上。 各个县均为多边形，以调色板中的颜色区分，但颜色并不与任何数据关联。 距离刻度同时用公里和英里显示距离。  
  
 并不显示地图图例和色阶，因为没有任何与各县关联的分析数据。 稍后，您将在本教程中添加分析数据。  
  
##  <a name="PointLayer"></a> 2.添加地图点层以显示商店位置  
 使用地图层向导添加一个点层，用于显示商店的位置。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>基于 SQL Server 空间查询添加点层  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。 在工具栏上，单击“新建层向导”按钮 ![rs_IconMapLayerWizard](../../2014/tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")。  
  
3.  在“选择空间数据的来源”页上，选择“SQL Server 空间查询”，然后单击“下一步”。  
  
4.  上**选择具有 SQL Server 空间数据的数据集**页上，单击**添加具有 SQL Server 空间数据的新数据集**，然后单击**下一步**。  
  
5.  在“选择与 SQL Server 空间数据源的连接”页上，选择现有数据源，或浏览到报表服务器并选择数据源。  
  
6.  单击“下一步” 。  
  
7.  在设计查询页上，单击**编辑为文本**。  
  
8.  将以下文本粘贴到查询窗格中：  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Rochester No.2 Store' as StoreName, 700 as SellingArea, 'Rochester' as City, 'Monroe' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-77.6240415667866 43.1547066024338)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. 在查询设计器工具栏中，单击“运行”(**!**)。  
  
     结果集将显示七列：StoreKey、 StoreName、 SellingArea、 City、 County、 销售和 SpatialLocation。 此数据表示纽约州销售生活消费品的一组商店。 结果集中的每行都包含一个商店标识符、商店名称、用于产品显示的区域、商店所在的市和县、总销售额以及用经度和纬度表示的空间位置。 显示区域范围从 455 平方英尺到 1125 平方英尺。  
  
10. 单击“下一步” 。  
  
     此时，将会为您创建一个名为 DataSet1 的报表数据集。 在完成向导后，可以将“报表数据”用于其字段集合。  
  
11. 上**选择空间数据和地图视图选项**页上，确认**空间字段**是`SpatialLocation`并且**层类型**是**点**. 接受本页上的其他默认值。  
  
     地图视图显示圆圈，这些圆圈标记了每个商店的位置。  
  
12. 单击“下一步” 。  
  
13. 指定一个地图类型，它显示随分析数据而改变的标记。 在选择地图可视化效果上，单击**分析标记地图**，然后单击**下一步**。  
  
14. 上**选择分析数据集**页上，单击 DataSet1。 此数据集同时包含分析数据和空间数据，它将显示在新的点层上。  
  
15. 单击“下一步” 。  
  
16. 上**选择颜色主题和数据可视化**页上，清除**使用标记颜色实现数据可视化效果**选项，并选择选项**使用标记类型可视化数据**.  
  
17. 在中**数据字段**，选择`[Sum(SellingArea)]`来存储到某个位置设置要显示的产品区域的大小来改变标记类型。  
  
18. 单击 **“完成”**。  
  
     将向报表添加该地图层。 图例根据 SellingArea 值显示标记类型。  
  
     双击地图以显示“地图层”窗格。 “地图层”窗格显示新层“PointLayer1”，以及空间数据源类型“DataRegion”。  
  
19. 添加图例标题。 右键单击图例标题，然后依次**图例标题属性**。  
  
20. 删除标题，然后键入**Display Area (Square Feet)**。  
  
21. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
22. 查看向导设置的默认值。 在中**地图层窗格**，右键单击点层，然后单击**标记类型规则**。  
  
     上**常规**选项卡上，在图例中出现的顺序列出这些标记。 上**分发**选项卡中，子范围数为 5。 上**图例**选项卡上，图例文本设置为每个区域中显示的开始和结束值。  
  
23. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. 预览报表。  
  
 该地图显示纽约州的商店的位置。 每个商店的标记类型基于显示区域。 系统会自动为您计算五个范围的显示区域。  
  
##  <a name="LineLayer"></a> 3.添加地图线条层以显示路线  
 使用地图层向导添加一个显示两个商店间路线的地图层。 本教程中，通过三个商店位置创建路径。 在业务应用程序中，路径可能是两个商店间的最佳路线。  
  
#### <a name="to-add-a-line-layer-to-map"></a>向地图添加线条层  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。 在工具栏上，单击**新建层向导**。  
  
3.  在“选择空间数据的来源”页上，选择“SQL Server 空间查询”，然后单击“下一步”。  
  
4.  在“选择具有 SQL Server 空间数据的数据集”页上，单击“添加具有 SQL Server 空间数据的新数据集”，然后单击“下一步”。  
  
5.  上**选择与 SQL Server 空间数据源的连接**，选择 DataSource1，第一个过程中创建的数据源。  
  
6.  单击“下一步” 。  
  
7.  在 **“设计查询”** 页中，单击 **“编辑为文本”**。 查询设计器切换到基于文本的模式。  
  
8.  将以下文本粘贴到查询窗格中：  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. 单击“下一步” 。  
  
     此时，地图上将显示一条连接三个商店的路径。  
  
10. 在“选择空间数据和地图视图选项”页上，确认“空间字段”为“路线”，且“层类型”为“线条”。 接受其他默认值。  
  
     地图视图显示一条从位于纽约州北部的商店到位于纽约州南部商店的路径。  
  
11. 单击“下一步” 。  
  
12. 在“选择地图可视化”页上，单击“基本线条图”，然后单击“下一步”。  
  
13. 在“选择颜色主题和数据可视化”上，选择“单色图”选项。 该路径基于所选主题显示为某种颜色。  
  
14. 单击 **“完成”**。  
  
 地图显示新线条层与空间数据源类型**数据集**。 在本例中，空间数据来自数据源，但没有分析数据与此线条关联。  
  
##  <a name="TileLayer"></a> 4.添加 Bing 地图图块背景  
 添加一个地图层，用于显示 Bing 地图图块背景。  
  
#### <a name="to-add-a-virtual-earth-tile-background"></a>添加 Virtual Earth 图块背景  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。 在工具栏上，单击**添加层**![rs_IconMapAddLayer](../../2014/tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")。  
  
3.  从下拉列表中，单击“图块层”。  
  
     “地图层”窗格中的最后一层为“TileLayer1”。 默认情况下，图块层显示道路图样式。  
  
    > [!NOTE]  
    >  在本向导中，还可以在“选择空间数据和地图视图选项”页上添加图块层。 若要执行此操作，请选择“为该地图视图添加必应地图背景”。 在呈现的报表中，图块背景为当前地图视区中心和缩放级别显示 Bing 地图图块。  
  
4.  单击 TileLayer1 上的向下箭头，然后单击**图块属性**。  
  
5.  在中**类型**，选择**空中**。 空中视图不包含文本。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Transparent"></a> 5.将层设置为透明  
 若希望某一层上的项透过另一层显示出来，则可以调整层的顺序以及每层的透明度以获得您想要的效果。  
  
#### <a name="to-set-the-transparency-of-a-layer"></a>设置层的透明度  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。  
  
3.  单击 PolygonLayer1 上的向下箭头，然后单击**层数据**。 将打开“地图多边形层属性”对话框。  
  
4.  单击 **“可见性”**。  
  
5.  在中**透明度 （%）**，类型**30**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 设计图面将县显示为半透明。  
  
##  <a name="Vary"></a> 6.根据销售改变县颜色  
 多边形层上的每个县都有一种不同的颜色，因为报表处理器会根据您在地图向导的最后一页选择的主题，自动从调色板中分配一个颜色值。  
  
 在下面的步骤中，指定颜色规则，以便将特定的颜色与每个县的商店销售额范围关联起来。 颜色红-黄-绿指示相应的高-中-低销售额。 设置色阶的格式以显示货币。 在新的图例中显示年销售额范围。 对于不包含商店的县，不使用任何颜色，以指明没有关联的数据。  
  
###  <a name="Relationship"></a> 6a. 在空间数据与分析数据之间建立关系  
 若要基于分析数据改变县形状中的颜色，首先必须将分析数据与空间数据关联起来。 在本教程中，您将使用要匹配的县名称。  
  
##### <a name="to-build-a-relationship-between-spatial-data-and-analytical-data"></a>在空间数据与分析数据之间建立关系  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。  
  
3.  单击 PolygonLayer1 上的向下箭头，然后单击**层数据**。 将打开“地图多边形层属性”对话框。  
  
4.  单击 **“分析数据”**。  
  
5.  从下拉列表中选择 DataSet1。 此数据集是您为县指定空间数据查询时由向导创建的。  
  
6.  在中**用于匹配的字段**，单击**添加**。 将添加一个新行。  
  
7.  在中**来自空间数据集**，从下拉列表单击 COUNTYNAME。  
  
8.  在中**来自分析数据集**，从下拉列表中，单击 [县]。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 预览报表。  
  
 通过从空间数据源和分析数据集中指定一个匹配字段，报表处理器可以基于地图元素对分析数据进行分组。 针对您指定的值，数据绑定的地图元素具有成功的匹配项。  
  
 对于包含商店的每个县，其颜色取决于您在向导中选择的样式的调色板。  
  
###  <a name="ColorRules"></a> 6b. 为多边形指定颜色规则  
 若要创建根据商店销售额改变每个县颜色的规则，必须指定范围值、要显示的范围的划分数以及要使用的颜色。  
  
##### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>为具有关联数据的所有多边形指定颜色规则  
  
1.  切换到“设计”视图。  
  
2.  单击 PolygonLayer1 上的向下箭头，然后单击**多边形颜色规则**。 将打开“地图颜色规则属性”对话框。 请注意，已选择“使用调色板实现数据的可视化效果”颜色规则选项。 此选项已由向导进行设置。  
  
3.  选择“使用颜色范围实现数据的可视化效果”。 调色板选项被开始颜色、中间颜色和结束颜色选项取代。  
  
4.  为每个县的销售额定义范围值。 在“数据字段”中，从下拉列表中选择“`[Sum(Sales)]`”。  
  
5.  若要更改格式以便以千为单位显示货币，请将表达式更改为以下形式： `=Sum(Fields!Sales.Value)/1000`  
  
6.  将“开始颜色”更改为“红色”。  
  
7.  将“结束颜色”更改为“绿色”。  
  
     “红色”表示低销售值，“黄色”表示中等销售值，而“绿色”表示高销售值。 报表处理器将基于这些值以及在“分布”页上选择的选项来计算颜色范围。  
  
8.  单击 **“分布”**。  
  
9. 确认分布类型为“最佳”。 对于步骤 5 中的表达式，最佳分布将值划分到各个子范围，这些子范围在每个范围中的项数与每个范围的跨度之间实现平衡。  
  
10. 对于本页上的其他选项接受默认值。 如果您选择最佳分布类型，则在运行报表时将计算子范围数。  
  
11. 单击 **“图例”**。  
  
12. 在“色阶选项”中，确认已选中“在色阶中显示”。  
  
13. 在“在此图例中显示”中，从下拉列表中选择空行。 现在，您只将颜色范围显示在色阶中。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 色阶显示五种颜色：红色、橙色、黄色、黄绿色和绿色。 每个颜色表示一个销售额范围，此范围是以县为单位根据销售额自动计算得出的。  
  
###  <a name="ColorScale"></a> 6c. 将色阶中的数据的格式设置为“货币”  
 默认情况下，数据具有常规格式。 您可以应用自定义格式。  
  
##### <a name="to-set-the-format-for-the-color-scale"></a>设置色阶的格式  
  
1.  右键单击色阶，然后依次**色阶属性**。  
  
2.  单击**数**。  
  
3.  在中**类别**，单击**货币**。  
  
4.  在中**小数位数**，类型**0**。 此格式指定货币没有小数位。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  预览报表。  
  
 色阶对于每个范围用货币格式显示年销售额。  
  
###  <a name="NewLegend"></a> 6d. 创建新图例  
 默认情况下，所有规则显示在第一个图例中。 若要改进地图的显示效果，可以添加图例。  
  
 若要更改默认显示，有两个步骤：创建新的图例，然后将地图层的规则结果与新的图例相关联。  
  
##### <a name="to-create-a-new-legend"></a>创建新图例  
  
1.  切换到“设计”视图。  
  
2.  右键单击该地图视区外的然后依次**添加图例**。 将在默认位置向地图添加新图例。  
  
3.  右键单击图例，然后依次**图例属性**。  
  
4.  在中**位置选项**，指定想要显示相对于视区的图例的位置单击。 设计图面上的地图将更改以显示您的选择效果。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  单击**标题**图例以选择图例标题。  
  
7.  单击**标题**再次以进入文本插入模式。 替换**标题**通过**销售额 （千）**，然后在文本外部单击。  
  
 图例将展开以显示标题。  
  
###  <a name="Associate"></a> 6e。 将图例与颜色规则关联  
 每个图例可以显示一组或多组规则结果。  
  
##### <a name="to-associate-a-legend-with-color-rules"></a>将图例与颜色规则关联  
  
1.  双击地图以显示“地图层”窗格。  
  
2.  单击 PolygonLayer1 上的向下箭头，然后单击**多边形颜色规则**。 将打开“地图颜色规则属性”对话框。  
  
3.  单击 **“图例”**。  
  
4.  在中**色阶选项**，清除**在色阶中显示**。  
  
5.  在中**图例选项**，从下拉列表中，选择 Legend2。 将显示图例文本选项。 默认情况下使用常规 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 格式字符串设置图例文本的格式。 N0 中的 0 指定没有小数位数。  
  
6.  在中**图例文本**，使用以下格式指定货币没有小数位数： `#FROMVALUE {C0} - #TOVALUE {C0}`  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     在设计图面上，图例显示颜色范围，且示例数据的格式设置为货币。  
  
8.  预览报表。  
  
 具有关联的商店和销售额的县根据颜色规则进行显示。 没有销售额的县没有颜色。  
  
###  <a name="NoData"></a> 6f。 更改没有数据的县的颜色  
 可以为层上所有地图元素设置默认显示选项。 颜色规则优先于这些显示选项。  
  
##### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>为层上的所有元素设置显示属性  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。  
  
3.  单击“PolygonLayer1”上的向下箭头，然后单击“多边形属性”。 将打开“地图多边形属性”对话框。 在应用基于规则的显示选项之前，此对话框中设置的显示选项将应用于层上的所有多边形。  
  
4.  单击**填充**。  
  
5.  确保填充样式为**纯色。** 。渐变样式和图案样式应用于所有颜色。  
  
6.  在中**颜色**，单击向下箭头，然后单击**浅钢蓝色**。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  预览报表。  
  
 不具有关联数据的县显示为蓝色。 只有具有关联的分析数据的县才显示在**红色**通过**绿色**您指定的颜色规则的颜色。  
  
##  <a name="CustomPoint"></a> 7.添加自定义点  
 若要表示尚未建立的新存储，请指定一个点，并使用**图钉**标记类型。  
  
#### <a name="to-add-a-custom-point"></a>添加自定义点  
  
1.  切换到“设计”视图。  
  
2.  双击地图以显示“地图层”窗格。 在工具栏上，单击**添加层**，然后单击**点层**。  
  
     将向地图添加一个新点层。 默认情况下，该点层的空间数据类型为“嵌入”。  
  
3.  单击 PointLayer2 上的向下箭头，然后单击**添加点**。  
  
4.  将指针移到地图视区上方。 光标将变为十字准线。  
  
5.  单击地图上您要添加点的位置。 在本教程中，单击县中路线起点旁边的位置。 用圆圈标记的点将添加到层中您单击的位置。 默认情况下，该点处于选中状态。  
  
6.  右键单击添加的点，然后单击“嵌入的点属性”。  
  
7.  选择的选项**覆盖此层的点选项**。 其他页将显示在对话框中。 您在此处设置的值优先于层或颜色规则的显示选项。  
  
8.  单击**标记**。  
  
9. 有关**标记类型**，选择**星型**。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 预览报表。  
  
 您添加的新点显示为**星型**。  
  
#### <a name="to-add-a-label-for-the-custom-point"></a>为自定义点添加标签  
  
1.  切换到“设计”视图。  
  
2.  右键单击您刚的点添加，然后依次**嵌入的点属性**。  
  
3.  单击**标签**。  
  
4.  在中**标签文本**，类型**New Store**。  
  
5.  在“位置”中，单击“顶部”。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  预览报表。  
  
 标签显示在商店位置上方。  
  
##  <a name="CenterView"></a> 将地图视图居中  
 更改地图视区中心和缩放级别。  
  
#### <a name="to-change-the-viewport"></a>更改视区  
  
1.  右键单击地图视区，然后依次**视区属性**。  
  
2.  单击**居中和缩放**。  
  
3.  验证选项**设置视图中心和缩放级别**处于选中状态。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  左键单击地图视区，并将视区中心拖到您希望的位置。  
  
6.  使用鼠标滚轮更改视区的缩放级别。  
  
7.  预览报表。  
  
 在“设计”视图中，显示图面上的地图以及视图基于示例数据。 在呈现的报表中，地图视图位于您指定的视图的中心。  
  
##  <a name="Title"></a> 添加报表标题  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”。  
  
2.  键入 **Sales in New York Stores** ，然后在文本框外部单击。  
  
 此标题将显示在报表的顶部。 当未定义页眉时，表体顶部的项等同于报表表头。  
  
##  <a name="Save"></a> 保存报表  
  
#### <a name="to-save-the-report"></a>保存报表  
  
1.  切换到“设计”视图。  
  
2.  从“报表生成器”按钮，单击 **“另存为”**。  
  
3.  在“名称”中，键入“纽约的商店销售额”。  
  
 单击“保存” 。  
  
## <a name="next-steps"></a>后续步骤  
 到此为止，我们结束了有关如何向报表添加地图的演练。  
  
 有关详细信息，请参阅[映射&#40;报表生成器和 SSRS&#41; ](report-design/maps-report-builder-and-ssrs.md)和博客文章[空间数据的制图调整 SQL Server Reporting services](https://go.microsoft.com/fwlink/?LinkId=152771) blogs.msdn.com 上的。  
  
 有关更多教程，请参阅[教程&#40;报表生成器&#41;](report-builder-tutorials.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)   
 [地图向导和地图层向导（报表生成器和 SSRS）](report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
