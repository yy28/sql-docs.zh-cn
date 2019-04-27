---
title: 教程：向报表添加条形图（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b21826cb926dbd5f8b0315f490b20850c6ccd23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62648309"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>教程：向报表添加条形图（报表生成器）
  条形图以水平方式显示类别数据。 这有助于：  
  
-   提高长类别名称的可读性。  
  
-   提高绘制为值的时间的可理解性。  
  
-   比较多个序列的相对值。  
  
 下图显示了您将创建的条形图，条形图中按字母顺序显示了 2008 和 2009 年度前五位销售人员的销售情况。  
  
 ![rs_BarChartTutorial](../../2014/tutorials/media/rs-barcharttutorial.gif "rs_BarChartTutorial")  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将学习如何执行下列操作：  
  
1.  [使用图表向导创建图表](#Chart)  
  
2.  [选择图表类型](#ChartType)  
  
3.  [垂直轴上显示所有类别值](#AllValues)  
  
4.  [修改垂直轴上的名称的显示](#Sort)  
  
5.  [移动图例](#Legend)  
  
6.  [移动图表标题](#ChartTitle)  
  
7.  [格式和标签的水平轴](#Horizontal)  
  
8.  [添加筛选器以显示前五个值](#Filter)  
  
9. [添加报表标题](#Title)  
  
10. [保存报表](#Save)  
  
> [!NOTE]  
>  在本教程中，将向导的多个步骤合并为一个过程。 有关如何转到报表服务器、创建数据集和选择数据源的分步说明，请参阅本系列教程中的第一个教程：[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 估计的时间才能完成本教程中：15 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Chart"></a> 1.使用图表向导创建图表报表  
 从**Getting Started**对话框中，创建嵌入数据集、 选择共享的数据源，并使用图表向导创建条形图。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-create-a-new-chart-report"></a>创建新的图表报表  
  
1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。  
  
     此时将显示 **“入门”** 对话框。  
  
    > [!NOTE]  
    >  如果**Getting Started**对话框不会不会显示，单击报表生成器按钮，然后单击**新建**。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击“图表向导”。  
  
4.  在“选择数据集”页上，单击“创建数据集”，然后单击“下一步”。  
  
5.  在“选择数据源的连接”页中，选择现有数据源或浏览到报表服务器并选择一个数据源，然后单击“下一步”。 您可能需要输入用户名和密码。  
  
    > [!NOTE]  
    >  只要您具有足够的权限，则选择哪一个数据源并不重要。 您将不会从数据源中获取数据。 有关详细信息，请参阅[获取数据连接的备选方式（报表生成器）](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在“设计查询”页上，单击“编辑为文本”。  
  
7.  将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2009, CAST(150000. AS money) AS SalesYear2008  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(190000. AS money) AS SalesYear2008  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2009, CAST(195000. AS money) AS SalesYear2008  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(160000. AS money) AS SalesYear2008  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(220000. AS money) AS SalesYear2008  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(215000. AS money) AS SalesYear2008  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2009, CAST(207000. AS money) AS SalesYear2008  
    ```  
  
8.  （可选）单击“运行”按钮 (**!**)，查看要用于图表的数据。  
  
9. 单击“下一步” 。  
  
##  <a name="ChartType"></a> 2.选择图表类型  
 可以从各种预定义的图表类型中进行选择。  
  
#### <a name="to-add-a-column-chart"></a>添加柱形图  
  
1.  在“选择图表类型”页上，柱形图为默认图表类型。  
  
2.  单击“条形图”，然后单击“下一步”。  
  
     “排列图表字段”页上的“可用字段”窗格中有 4 个字段：FirstName、 LastName、 SalesYear2009 和 SalesYear2008。  
  
3.  将 LastName 拖动到“类别”窗格。  
  
4.  将 SalesYear2009 拖动到“值”窗格。 SalesYear2009 表示每个销售人员在 2009 年的销售总额。 “值”窗格显示 `[Sum(SalesYear2009)]` ，因为该图表显示的是每个产品的销售总额。  
  
5.  将 SalesYear2008 拖动到 SalesYear2009 下的“值”窗格。 SalesYear2008 表示每个销售人员在 2008 年的销售总额。  
  
6.  单击“下一步” 。  
  
7.  上**选择一种样式**页上，在样式窗格中，选择一种样式。  
  
     样式指定字形、颜色集和边框样式。 选择样式时，“预览”窗格将显示具有该样式的图表的示例。  
  
8.  单击 **“完成”**。  
  
     图表将添加到设计图面中。  
  
9. 单击图表以显示图表控点。 拖动该图表的右下角以扩大该图表。  
  
10. 单击 **“运行”** 以预览报表。  
  
 报表将显示每个销售人员在 2008 和 2009 年度销售情况的条形图。 条形图的长度对应于总销售额。  
  
##  <a name="AllValues"></a> 3.修改垂直轴上的名称的显示  
 默认情况下，垂直轴上只显示某些值。 您可以更改图表以显示所有类别。  
  
#### <a name="to-display-all-sales-persons-along-the-category-axis-of-a-bar-chart"></a>沿条形图的类别轴显示所有销售人员  
  
1.  切换到报表设计视图。  
  
2.  右键单击垂直轴，然后依次**垂直轴属性**。  
  
3.  在“轴范围和间隔”下的“间隔”框中，键入 1。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  右键单击垂直**轴标题**并清除**显示轴标题**复选框。  
  
6.  单击 **“运行”** 以预览报表。  
  
> [!NOTE]  
>  如果无法阅读垂直轴上的销售人员姓名，则可以增加图表的高度，或更改轴标签的格式选项。  
  
###  <a name="CategoryExpression"></a> 垂直轴上显示姓氏和名字  
 可以更改类别表达式以将每个销售人员的姓氏包含在名字之后。  
  
##### <a name="to-change-the-category-expression"></a>更改类别表达式  
  
1.  切换到报表设计视图。  
  
2.  双击图表以显示“图表数据”窗格。  
  
3.  在“类别组”区域中右键单击 [LastName]，然后单击“类别组属性”。  
  
4.  在“标签”中，单击表达式 (Fx) 按钮。  
  
5.  键入以下表达式： `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
     此表达式将连接姓氏、逗号和名字。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  单击 **“运行”** 以预览报表。  
  
 如果在运行报表时没有显示名字，则您可以手动刷新数据。 在仍处于预览模式时，在“导航”组的“运行”选项卡上，单击“刷新”。  
  
> [!NOTE]  
>  如果无法阅读垂直轴上的销售人员姓名，则可以增加图表的高度，或更改轴标签的格式选项。  
  
##  <a name="Sort"></a> 4.更改垂直轴上的名称的排序顺序  
 当您对图表中的数据进行排序时，您是在更改类别轴上的值的顺序。  
  
#### <a name="to-sort-the-names-in-alphabetical-order-on-the-bar-chart"></a>按字母顺序对条形图中的姓名进行排序  
  
1.  切换到报表设计视图。  
  
2.  双击图表以显示“图表数据”窗格。  
  
3.  在“类别组”区域中右键单击 [LastName]，然后单击“类别组属性”。  
  
4.  单击 **“排序”**。 “更改排序选项”页将显示排序表达式的列表。 默认情况下，此列表具有一个与原始类别组表达式相同的排序表达式。  
  
5.  在排序依据，单击表达式 (**Fx**) 按钮。  
  
6.  键入以下表达式： `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
7.  单击“确定” 。  
  
8.  重新**类别组属性**页上，在**顺序**下拉列表中，选择**Z 到 A**。这将选择反向字母顺序，以便按顺序从上到下显示姓名。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 单击 **“运行”** 以预览报表。  
  
 水平轴上的姓名按相反顺序与**Alerca**顶部并**Zeng**底部。  
  
##  <a name="Legend"></a> 5.移动图例  
 为了提高图表值的可读性，可能需要移动图表图例。 例如，在水平显示图条的条形图中，可以更改图例的位置，将其放置在图表区的上方或下方。 这可为图条提供更大的水平空间。  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>在条形图的图表区下方显示图例  
  
1.  切换到报表设计视图。  
  
2.  右键单击图表上的图例。  
  
3.  选择“图例属性”。  
  
4.  对于“图例位置”，请选择其他位置。 例如，将图例位置设置为底部中间。  
  
     如果将图例置于图表的顶部或底部，则图例的布局将会从垂直改为水平。 可以从“布局”下拉列表中选择不同的布局。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  单击 **“运行”** 以预览报表。  
  
##  <a name="ChartTitle"></a> 6.设置图表的标题  
  
#### <a name="to-change-the-chart-title-above-the-chart-area-of-a-bar-chart"></a>更改条形图的图表区上方的图表标题  
  
1.  切换到报表设计视图。  
  
2.  选择词语**图表标题**在顶部的图表，然后键入以下文本：**Sales for 2008 and 2009**。  
  
3.  单击该文本的外部。  
  
4.  单击 **“运行”** 以预览报表。  
  
##  <a name="Horizontal"></a> 7.设置水平轴的格式和标签  
 默认情况下，水平轴采用常用格式显示值，将自动调整为适合图表的大小。  
  
#### <a name="to-format-the-numbers-on-the-horizontal-axis"></a>设置水平轴上数字的格式  
  
1.  切换到报表设计视图。  
  
2.  沿图表底部单击水平轴，以选择它。  
  
     在功能区中，在**主页**选项卡上，在**数量**组中，单击**货币**按钮。 水平轴标签将更改为货币。  
  
3.  （可选）删除小数位数。 在“货币”按钮附近，单击两次“减少小数位数”按钮。  
  
4.  右键单击水平轴，然后单击“水平轴属性”。  
  
5.  上**数量**选项卡上，选择**以千为单位显示值。**  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  右键单击**轴标题**然后单击**轴标题属性**。  
  
8.  在中**标题文本**框中，键入**以千为单位销售**然后单击**确定**。  
  
9. 单击 **“运行”** 以预览报表。  
  
 报表将在水平轴上以千为单位将销售额显示为货币，且没有小数位数。  
  
##  <a name="Filter"></a> 8.添加筛选器以显示前五个值  
 可以向图表添加筛选器，以指定数据集中哪些数据要包含于图表中或排除在图表外。  
  
#### <a name="to-add-a-filter-and-display-the-top-five-values"></a>添加筛选器并显示前五个值  
  
1.  切换到报表设计视图。  
  
2.  双击图表以显示“图表数据”窗格。  
  
3.  在“类别组”区域中，右键单击 [LastName] 字段，然后单击“类别组属性”。  
  
4.  单击 **“筛选器”**。 “更改筛选器”页可以显示筛选器表达式的列表。 默认情况下，此列表为空。  
  
5.  单击 **“添加”**。 此时将显示一个新的空白筛选器。  
  
6.  在中**表达式**，类型 **[Sum(SalesYear2009)]**。 此时将创建基础表达式 `=Sum(Fields!SalesYear2009.Value)`，可以查看是否单击了“fx”按钮。  
  
7.  验证确保数据类型是“文本”。  
  
8.  在“运算符”中，从下拉列表中选择“前 N 个”。  
  
9. 在“值”中，键入以下表达式：=5  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 单击 **“运行”** 以预览报表。  
  
 如果在运行报表时没有对结果进行筛选，则可以手动刷新数据。 在“导航”组的“运行”选项卡上，单击“刷新”。  
  
 图表将显示 2009 年销售数据中前五位销售人员的姓名。  
  
##  <a name="Title"></a> 9.添加报表标题  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”。  
  
2.  类型**Sales Bar Chart**，再按 ENTER，，然后键入**Top Five Sellers for 2009**，使其如下所示：  
  
     **Sales Bar Chart**  
  
     **Top Five Sellers for 2009**  
  
3.  选择 **Sales Bar Chart**，并单击“加粗”按钮。  
  
4.  选择**Top Five Sellers for 2009**，然后在**字体**部分**主页**选项卡上，将字号设置为**10**。  
  
5.  （可选）您可能需要使“标题”文本框更高一些，以容纳两行文本。  
  
     此标题将显示在报表的顶部。 未定义页标头时，报表体顶部的项就等同于报表标头。  
  
6.  单击 **“运行”** 以预览报表。  
  
##  <a name="Save"></a> 10.保存报表  
  
#### <a name="to-save-the-report"></a>保存报表  
  
1.  切换到报表设计视图。  
  
2.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
3.  在“名称”中，键入 Sales Bar Chart。  
  
4.  单击“保存” 。  
  
 报表将保存在报表服务器上。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功完成“向报表添加条形图”教程的学习。 若要了解有关图表的详细信息，请参阅[图表（报表生成器和 SSRS）](report-design/charts-report-builder-and-ssrs.md)和[迷你图和数据条（报表生成器和 SSRS）](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
