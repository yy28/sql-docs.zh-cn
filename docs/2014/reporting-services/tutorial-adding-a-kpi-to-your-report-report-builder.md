---
title: 教程：向报表添加 KPI（报表生成器）| Microsoft Docs
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
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946014"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>教程：向报表添加 KPI（报表生成器）
  关键绩效指标 (KPI) 是对业务具有重大意义的可测量值。 本教程教您如何在报表中包含一个 KPI。 在本教程中，按产品子类别进行的销售汇总为 KPI。 可以使用颜色、仪表和指示器来显示 KPI 的当前状态。  
  
 下图显示了将创建的报表。  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，将学习如何通过基于单元值设置表单元的背景色来添加 KPI，以及添加和配置仪表和指示器。 还将学习如何编写设置表单元的背景色的表达式。  
  
 本教程包含下列过程：  
  
1.  [从表或矩阵向导创建表报表和数据集](#Table)  
  
2.  [组织数据，并选择布局和样式表或矩阵向导](#CompleteWizard)  
  
3.  [使用背景色显示 KPI](#BackgroundColors)  
  
4.  [使用仪表显示 KPI](#Gauge)  
  
5.  [使用指示器显示 KPI](#Indicator)  
  
6.  [添加报表标题](#Title)  
  
7.  [保存报表](#Save)  
  
> [!NOTE]  
>  在本教程中，将向导的多个步骤合并为两个过程：一个用于创建数据集，一个用于创建表。 有关如何转到报表服务器、选择数据源、创建数据集和运行向导的分步说明，请参阅本系列教程中的第一个教程：[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 估计的时间才能完成本教程中：15 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Table"></a> 1.使用表向导或矩阵向导创建表报表和数据集  
 从**Getting Started**对话框中，选择共享的数据源，创建嵌入数据集，并显示一个表中的数据。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-create-a-new-table"></a>创建新表  
  
1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。  
  
     此时将显示 **“入门”** 对话框。  
  
    > [!NOTE]  
    >  如果**Getting Started**对话框不会出现，从报表生成器按钮，单击**新建**。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击“表或矩阵向导”。  
  
4.  在选择数据集页上，单击**创建数据集**。  
  
5.  单击“下一步” 。  
  
6.  在“选择数据源的连接”页上，选择现有数据源或浏览到报表服务器并选择一个数据源。 如果没有可用数据源，或无权访问报表服务器，可以改用嵌入数据源。 有关详细信息，请参阅[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
7.  单击“下一步” 。  
  
8.  在“设计查询”页上，单击“编辑为文本”。  
  
9. 复制并将以下查询粘贴到查询窗格中：  
  
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
  
10. 单击“下一步” 。  
  
##  <a name="CompleteWizard"></a> 2.组织数据，并选择布局和样式表或矩阵向导  
 使用此向导可提供用于显示数据的起始设计。 此向导中的预览窗格可帮助您在完成表或矩阵设计之前将对数据进行分组的结果可视化。  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>若要将数据组织成组，请选择布局和样式  
  
1.  在“排列字段”页上，将 Product 拖到“值”中。  
  
2.  将 Quantity 拖到“值”中并将其置于 Product 下方。  
  
     将使用汇总数值字段的默认函数 Sum 函数对 Quantity 进行汇总。  
  
3.  将 Sales 拖到“值”中并将其放在 Quantity 下面。  
  
     步骤 1、2 和 3 指定要在表中显示的数据。  
  
4.  将 SalesDate 拖到“行组”中。  
  
5.  将 Subcategory 拖到“行组”中并将其置于 SalesDate 下方。  
  
     步骤 4 和 5 首先按日期组织字段的值，然后按照该日期的所有销售组织字段的值。  
  
6.  单击“下一步” 。  
  
     当您运行报表时，表将显示每个日期、每个日期的所有订单以及每个订单的所有产品、数量和销售额总计。  
  
7.  在“选择布局”页的“选项”下，确认已选择“显示小计和总计”。  
  
8.  验证是否选择了“分块式，小计下方显示”。  
  
9. 清除“展开/折叠组”选项。  
  
     在本教程中，创建的报表不会使用明细功能（用户可通过此功能来展开父组层次结构）来显示子组行和详细信息行。  
  
10. 单击“下一步” 。  
  
11. 在“选择样式”页的“样式”窗格中，选择样式。  
  
     已完成报表的图采用“海洋”样式显示报表。  
  
12. 单击 **“完成”**。  
  
     表将添加到设计图面中。 此表有五个列和五个行。 “行组”窗格显示三个行组：“SalesDate”、“Subcategory”和“Details”。 详细信息数据是由数据集查询检索的所有数据。  
  
13. 单击 **“运行”** 以预览报表。  
  
 对于在特定日期销售的每个产品，表显示产品名称、销售数量及销售额总计。 此数据首先按销售日期组织，然后按子类别组织。  
  
##  <a name="BackgroundColors"></a> 3.使用背景色显示 KPI  
 可将背景色设置为运行报表时计算的表达式。  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>使用背景色显示 KPI 的当前状态  
  
1.  在表中，右键单击两个单元格下从`[Sum(Sales)]`单元格 （小计行中显示子类别的销售额），并单击**文本框属性**。  
  
2.  在中**填充**，单击**fx**按钮旁边**填充颜色**选项并输入以下表达式**设置表达式：字段中输入以下表达式：  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 对于包含大于或等于 5000 的 `[Sum(Sales)]` 聚合汇总的每个单元，该表达式会使用名为“Lime”的绿色阴影，将背景色会更改为绿色。 2500 和 5000 之间的 `[Sum(Sales)]` 值会变为黄色。 小于 2500 的值会变为红色。  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  单击 **“运行”** 以预览报表。  
  
 在显示子类别销售额的小计行中，根据销售额总计的值，单元的背景色为红色、黄色或绿色。  
  
##  <a name="Gauge"></a> 4.使用仪表显示 KPI  
 仪表显示数据集中的单个值。 本教程使用水平线性仪表，因为即使是在该仪表较小或在表单元内使用的情况下，其形状和简便性也使其易于读取。 有关详细信息，请参阅 [仪表（报表生成器和 SSRS）](report-design/gauges-report-builder-and-ssrs.md)。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>使用仪表显示 KPI 的当前状态  
  
1.  切换到“设计”视图。  
  
2.  在表中，右键单击列处理程序的上一个过程中更改的单元格，指向**插入列**，然后单击**右**。 此时将向表添加一个新列。  
  
3.  类型**KPI**列标题中。  
  
4.  上**插入**选项卡上，在**数据区域**组中，单击**仪表**，然后单击表外的设计图面。 此时将显示 **“选择仪表类型”** 对话框。  
  
5.  单击**线性**。 第一个线性仪表类型**水平**，处于选中状态。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     此时将向设计图面添加一个仪表。  
  
7.  从“报表数据”窗格，将 Sales 拖至该仪表。 当您在仪表中拖动 Sales 时，将打开“仪表数据”窗格。  
  
8.  Sales 放**值**列表。  
  
     将该字段拖到仪表中时，将使用内置 Sum 函数聚合该字段。  
  
9. 右键单击仪表中的指针，然后单击**指针属性**。  
  
10. 在中**指针类型**，选择**栏**。 这会将指针从标记改为条形，从而在将仪表添加到表中时更加清晰可见。  
  
11. 单击**指针填充**。 在中**辅助颜色**选取**黄色**。 渐变填充模式将从白色改为黄色。  
  
12. 右键单击仪表中的刻度，然后单击“刻度属性”。  
  
13. 设置**最大**为 25000 的选项。  
  
    > [!NOTE]  
    >  可以使用一个表达式动态计算“最大值”选项的值来代替常数（如 25000）。 该表达式将使用聚合功能的聚合，类似于表达式 `=Max(Sum(Fields!Sales.value), "Tablix1")`。  
  
14. 将表内的仪表拖到所插入列的小计行（此行显示子类别的销售额）的第三个单元中。  
  
    > [!NOTE]  
    >  可能需要调整列大小，以使单元能够容纳水平线性仪表。 若要调整列大小，请单击列标题，并使用控点水平和垂直调整单元大小。  
  
15. 单击 **“运行”** 以预览报表。  
  
     仪表中条形的水平长度将根据 KPI 的值变化。  
  
16. （可选）添加处理溢出的最大刻度格，以使超出最大刻度的任何值始终指向最大刻度格：  
  
    1.  打开“属性”窗格。  
  
    2.  单击缩放。 该线性刻度的属性将显示在“属性”窗格中。  
  
    3.  在中**刻度针**类别中，展开**MaximumPin**节点。  
  
    4.  设置**启用**属性设置为`True`。 随即将在刻度的最大值之后显示一个刻度格。  
  
    5.  设置**BorderColor**到`Lime`。  
  
17. 单击 **“运行”** 以预览报表。  
  
##  <a name="Indicator"></a> 5.使用指示器显示 KPI  
 指示器是以直观的形式传递数据值的小巧而简单的仪表。 由于指示器尺寸较小且具有简便性，其经常被用于表和矩阵中。 有关详细信息，请参阅[指示器（报表生成器和 SSRS）](report-design/indicators-report-builder-and-ssrs.md)。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>使用指示器显示 KPI 的当前状态  
  
1.  切换到“设计”视图。  
  
2.  在表中，右键单击列处理程序的上一个过程中更改的单元格，指向**插入列**，然后单击**右**。 此时将向表添加一个新列。  
  
3.  类型**KPI**列标题中。  
  
4.  单击子类别小计的单元。  
  
5.  上**插入**选项卡上，在**数据区域**组中，双击**指示器。**  
  
     “选择指示器类型”对话框即会打开。  
  
6.  单击**形状**。 第一个形状类型， **3 个交通灯 （无边框）** 处于选中状态。  
  
     在本教程中，您将使用该指示器。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     该指示器将添加到设计图面中。  
  
8.  右键单击指示器，然后单击“指示器属性”。  
  
9. 单击**值和状态**。  
  
10. 在值下拉列表中，选择 **[sum （sales)]**，但不是更改任何其他选项。  
  
     默认情况下，数据区域会发生数据同步，且将在“同步作用域”框中看到“Tablix1”值（报表中表数据区域的名称）。  
  
     在该报表中，还可以更改放在子类别小计单元中的指示器的作用域，以在 SalesDate 字段内同步。  
  
11. 单击 **“运行”** 以预览报表。  
  
##  <a name="Title"></a> 6.添加报表标题  
 报表标题将出现在报表的顶部。 可以将报表标题置于报表表头中或置于表体顶部的文本框中（如果报表未使用表头）。 您将使用自动放在表体顶部的文本框。  
  
 通过将不同的字体样式、大小和颜色应用于文本的短语和单个字符，可以进一步增强文本。 有关详细信息，请参阅[设置文本框中文本的格式（报表生成器和 SSRS）](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”。  
  
2.  类型**Product Sales KPI**，然后在文本框外部单击。  
  
3.  或者，右键单击包含该文本框**Product Sales KPI**，单击**文本框属性**，然后在字体选项卡上选择不同的字体样式、 大小和颜色。  
  
4.  单击 **“运行”** 以预览报表。  
  
##  <a name="Save"></a> 7.保存报表  
 将报表保存到报表服务器或计算机上。 如果不将报表保存到报表服务器上，则许多 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能（如报表部件和子报表）将不可用。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“最近使用的站点和服务器”**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为报表默认位置的报表文件夹的内容。  
  
4.  在“名称”中，用 Product Sales KPI 替换默认名称。  
  
5.  单击“保存” 。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>将报表保存到计算机上  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  依次单击“桌面”、“我的文档”或“我的电脑”，并浏览到要保存该报表的文件夹。  
  
> [!NOTE]  
>  如果无权访问报表服务器，请单击“桌面”、“我的文档”或“我的电脑”，将报表保存到计算机上。  
  
1.  在“名称”中，用 Product Sales KPI 替换默认名称。  
  
2.  单击“保存” 。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功完成“向报表添加 KPI”教程的学习。 有关详细信息，请参阅仪表 （报表生成器）[指标&#40;报表生成器和 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
