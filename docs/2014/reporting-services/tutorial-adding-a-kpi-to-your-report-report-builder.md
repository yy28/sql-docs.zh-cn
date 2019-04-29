---
title: 教程：将 KPI 添加到您的报表 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5362e72fefa36102737e362a1b4ec8b11b96c77f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62648223"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>教程：将 KPI 添加到您的报表 （报表生成器）
  关键绩效指标 (KPI) 是对业务具有重大意义的可测量值。 本教程讲解如何在报表中包含一个 (KPI)。 在此方案中，按产品子类别的销售汇总为 KPI。 使用颜色、 仪表和指示器显示 KPI 的当前状态。  
  
 下图显示了将创建的报表。  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将学习可以通过设置基于单元值的表格单元格的背景色来添加 KPI 并添加和配置仪表和指示器。 您还了解如何编写设置表单元格的背景色的表达式。  
  
 本教程包含以下过程：  
  
1.  [从表或矩阵向导创建表报表和数据集](#Table)  
  
2.  [组织数据，并选择布局和样式表或矩阵向导](#CompleteWizard)  
  
3.  [使用背景色显示 KPI](#BackgroundColors)  
  
4.  [使用仪表显示 KPI](#Gauge)  
  
5.  [使用指示器显示 KPI](#Indicator)  
  
6.  [添加报表标题](#Title)  
  
7.  [保存报表](#Save)  
  
> [!NOTE]  
>  在本教程中，该向导的步骤合并为两个过程： 一个用于创建数据集，一个用于创建表。 有关如何浏览到报表服务器的分步说明，选择数据源、 创建数据集，并运行该向导，请参阅本系列教程的第一个教程：[教程：创建基本表报表&#40;报表生成器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 估计的时间才能完成本教程中：15 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程的先决条件&#40;报表生成器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Table"></a> 1.从表或矩阵向导创建表报表和数据集  
 从**Getting Started**对话框中，选择共享的数据源，创建嵌入数据集，并显示一个表中的数据。  
  
> [!NOTE]  
>  在本教程中，查询包含了数据值，以便它不需要外部数据源。 这使得很长的查询。 在业务环境中，查询不会包含数据。 这是仅供学习。  
  
#### <a name="to-create-a-new-table"></a>若要创建新表  
  
1.  单击**启动**，依次指向**程序**，指向**Microsoft SQL Server 2012 报表生成器**，然后单击**报表生成器**。  
  
     **Getting Started**对话框随即出现。  
  
    > [!NOTE]  
    >  如果**Getting Started**对话框不会出现，从报表生成器按钮，单击**新建**。  
  
2.  在左窗格中，确认**新的报表**处于选中状态。  
  
3.  在右窗格中，单击**表或矩阵向导**。  
  
4.  在选择数据集页上，单击**创建数据集**。  
  
5.  单击 **“下一步”**。  
  
6.  上**选择数据源的连接**页上，选择现有数据源或浏览到报表服务器，选择数据源。 如果不没有可用的任何数据源或您没有访问报表服务器，可以改用嵌入的数据源。 有关详细信息，请参阅[教程：创建基本表报表&#40;报表生成器&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
7.  单击 **“下一步”**。  
  
8.  上**设计查询**页上，单击**编辑为文本**。  
  
9. 复制并粘贴到查询窗格的以下查询：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. 单击 **“下一步”**。  
  
##  <a name="CompleteWizard"></a> 2.组织数据，并选择布局和样式表或矩阵向导  
 使用该向导提供在其上显示数据的起始设计。 在向导中的预览窗格可帮助你在完成表或矩阵设计之前对数据进行分组的结果可视化。  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>若要将数据组织成组，请选择布局和样式  
  
1.  在排列字段页中，将 Product 拖到**值**。  
  
2.  将 Quantity 拖到**值**并将其置于 Product 下方。  
  
     Quantity 使用 Sum 函数，将使用汇总数值字段的默认函数进行汇总。  
  
3.  将 Sales 拖到**值**和将放在 Quantity 下面。  
  
     步骤 1、 2 和 3 指定要在表中显示的数据。  
  
4.  将 SalesDate 拖到**行组**。  
  
5.  将 Subcategory 拖到**行组**并将其置于 SalesDate 下方。  
  
     步骤 4 和 5 组织字段的值先按日期，然后按所有销售的该日期。  
  
6.  单击 **“下一步”**。  
  
     当您运行报表时，每个表显示日期，每个日期和所有产品、 数量和每个订单的销售总额的所有订单。  
  
7.  在选择布局页中，在**选项**，确认**显示小计和总计**处于选中状态。  
  
8.  确认**受到阻止，小计下方**处于选中状态。  
  
9. 清除选项**展开/折叠组**。  
  
     在本教程中，您创建的报表不使用向下钻取功能，它允许用户展开父组层次结构，以显示子组行和详细信息行。  
  
10. 单击 **“下一步”**。  
  
11. 在选择样式页，在样式窗格中，选择一种样式。  
  
     已完成的报表的图显示了使用海洋样式的报表。  
  
12. 单击 **“完成”**。  
  
     表添加到设计图面。 此表有五个列和五个行。 行组窗格显示了三个行组：SalesDate、 Subcategory、 和的详细信息。 详细信息数据是由数据集查询检索的所有数据。  
  
13. 单击**运行**以预览报表。  
  
 对于在特定日期销售的每个产品，表显示产品名称、 销售数量和总销售额。 数据首先按销售日期组织，然后组织按子类别。  
  
##  <a name="BackgroundColors"></a> 3.使用背景色显示 KPI  
 背景色可以设置为运行报表时计算的表达式。  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>若要使用的背景色显示 KPI 的当前状态  
  
1.  在表中，右键单击两个单元格下从`[Sum(Sales)]`单元格 （小计行中显示子类别的销售额），并单击**文本框属性**。  
  
2.  在中**填充**，单击**fx**按钮旁边**填充颜色**选项并输入以下表达式**设置表达式：BackgroundColor**字段：  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 这会更改背景颜色为绿色，将使用的绿色名为"Lime"，每个单元格包含聚合的汇总阴影`[Sum(Sales)]`是大于或等于 5000。 值的`[Sum(Sales)]`2500年和 5000 之间会变为黄色。 小于 2500年会标为红色值。  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  单击**运行**以预览报表。  
  
 在显示子类别的销售额的小计行，该单元格的背景色是红色、 黄色或绿色根据销售额总计的值。  
  
##  <a name="Gauge"></a> 4.使用仪表显示 KPI  
 仪表显示数据在数据集中的单个值。 本教程使用水平线性仪表，因为其形状和简便性也使其易于阅读，即使是在较小大小时时，表单元内使用。 有关详细信息，请参阅[仪表&#40;报表生成器和 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>若要显示的 KPI 使用仪表的当前状态  
  
1.  切换到“设计”视图。  
  
2.  在表中，右键单击列处理程序的上一个过程中更改的单元格，指向**插入列**，然后单击**右**。 一个新列添加到表。  
  
3.  类型**KPI**列标题中。  
  
4.  上**插入**选项卡上，在**数据区域**组中，单击**仪表**，然后单击表外的设计图面。 **选择仪表类型**对话框随即出现。  
  
5.  单击**线性**。 第一个线性仪表类型**水平**，处于选中状态。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     仪表添加到设计图面。  
  
7.  从报表数据窗格中，将 Sales 拖至该仪表。 在仪表中拖动 Sales 时，将打开仪表数据窗格。  
  
8.  Sales 放**值**列表。  
  
     该字段拖到仪表中时，通过使用内置 Sum 函数聚合该字段。  
  
9. 右键单击仪表中的指针，然后单击**指针属性**。  
  
10. 在中**指针类型**，选择**栏**。 这会将指针从标记更改为仪表添加到表时，将更可见的条。  
  
11. 单击**指针填充**。 在中**辅助颜色**选取**黄色**。 渐变填充模式将从白色更改为黄色。  
  
12. 右键单击仪表中的刻度，然后单击**刻度属性**。  
  
13. 设置**最大**为 25000 的选项。  
  
    > [!NOTE]  
    >  而不是如 25000 常量，您可以使用表达式来动态计算的值**最大**选项。 表达式将使用聚合功能的聚合，看起来类似于表达式`=Max(Sum(Fields!Sales.value), "Tablix1")`。  
  
14. 将表内的仪表拖到显示的列的插入子类别的销售额的小计行中的第三个单元格。  
  
    > [!NOTE]  
    >  您可能需要调整列大小，以便容纳该单元格的水平线性仪表。 若要调整列大小，单击列标题，并使用控点水平和垂直调整单元格的大小。  
  
15. 单击**运行**以预览报表。  
  
     水平条仪表发生更改，具体取决于 KPI 的值的长度。  
  
16. （可选）添加处理溢出，以便最大刻度上方的任何值始终指向最大 pin 使用最大 pin:  
  
    1.  打开属性窗格。  
  
    2.  单击缩放。 在属性窗格中显示线性刻度的属性。  
  
    3.  在中**刻度针**类别中，展开**MaximumPin**节点。  
  
    4.  设置**启用**属性设置为`True`。 Pin 将显示在刻度上的最大值之后。  
  
    5.  设置**BorderColor**到`Lime`。  
  
17. 单击**运行**以预览报表。  
  
##  <a name="Indicator"></a> 5.使用指示器显示 KPI  
 指标是传递数据值的快速的小型简单的仪表。 由于其大小和简单起见，指示器通常用于表和矩阵中。 有关详细信息，请参阅[指标&#40;报表生成器和 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>若要显示使用指示器的 KPI 的当前状态  
  
1.  切换到“设计”视图。  
  
2.  在表中，右键单击列处理程序的上一个过程中更改的单元格，指向**插入列**，然后单击**右**。 一个新列添加到表。  
  
3.  类型**KPI**列标题中。  
  
4.  单击子类别小计单元格。  
  
5.  上**插入**选项卡上，在**数据区域**组中，双击**指示器。**  
  
     **选择指示器类型**对话框随即打开。  
  
6.  单击**形状**。 第一个形状类型， **3 个交通灯 （无边框）** 处于选中状态。  
  
     在本教程中，将使用此指标。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     指示器将添加到设计图面。  
  
8.  右键单击指示器，然后单击**指示器属性**。  
  
9. 单击**值和状态**。  
  
10. 在值下拉列表中，选择 **[sum （sales)]**，但不是更改任何其他选项。  
  
     默认情况下，会发生数据同步的数据区域和您看到的值**Tablix1**，在报表中，表数据区域的名称中**同步作用域**框。  
  
     在此报表中，您还可以更改放在 SalesDate 字段内同步在子类别小计单元中指示器的作用域。  
  
11. 单击**运行**以预览报表。  
  
##  <a name="Title"></a> 6.添加报表标题  
 报表标题显示在报表的顶部。 可以将报表标题置于报表表头或如果报表不使用其中一个，在表体顶部的文本框中。 将使用自动放置在表体顶部的文本框。  
  
 通过将不同的字体样式、 大小和颜色应用于短语和单个字符的文本，可以进一步增强文本。 有关详细信息，请参阅[文本框中设置文本格式&#40;报表生成器和 SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
#### <a name="to-add-a-report-title"></a>若要添加报表标题  
  
1.  在设计图面上，单击**单击此项可添加标题**。  
  
2.  类型**Product Sales KPI**，然后在文本框外部单击。  
  
3.  或者，右键单击包含该文本框**Product Sales KPI**，单击**文本框属性**，然后在字体选项卡上选择不同的字体样式、 大小和颜色。  
  
4.  单击**运行**以预览报表。  
  
##  <a name="Save"></a> 7.保存报表  
 将报表保存到报表服务器或您的计算机。 如果不执行报表保存到报表服务器，许多[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]功能，如报表部件和子报表不可用。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>若要将报表保存在报表服务器上  
  
1.  从**报表生成器**按钮，再单击**另存为**。  
  
2.  单击**最近使用的站点和服务器**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     将显示消息"正在连接到报表服务器"。 连接完成后，你将看到报表服务器管理员指定为报表的默认位置的报表文件夹的内容。  
  
4.  在中**名称**，将使用默认名称为**Product Sales KPI**。  
  
5.  单击“保存” 。  
  
 报表将保存到报表服务器。 连接到的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>若要将报表保存在计算机上  
  
1.  从**报表生成器**按钮，再单击**另存为**。  
  
2.  单击**桌面**，**我的文档**，或**我的计算机**，并浏览到要保存报表的文件夹。  
  
> [!NOTE]  
>  如果你没有访问报表服务器，请单击**桌面**，**我的文档**，或**我的计算机**并将报表保存到您的计算机。  
  
1.  在中**名称**，将使用默认名称为**Product Sales KPI**。  
  
2.  单击“保存” 。  
  
## <a name="next-steps"></a>后续步骤  
 已成功添加到您的报表教程 KPI。 有关详细信息，请参阅仪表 （报表生成器）[指标&#40;报表生成器和 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
