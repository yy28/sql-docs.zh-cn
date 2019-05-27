---
title: 教程：向报表添加饼图（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f004241f078a9fb23acbca392f687a9b7c20ae84
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099051"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>教程：向报表添加饼图（报表生成器）
  饼图和圆环图将数据显示为整体的一定比例。 饼图常用于在各组之间进行比较。 饼图和圆环图与棱锥图和漏斗图一起构成一组称为形状图的图表。 形状图没有轴。 在形状图上放置某数值字段后，该图表将计算每个值相对总计的百分比。  
  
 如果饼图上有太多数据点，这些数据点就可能挤在一起，这会降低图表的可读性。 在此情况下，应考虑使用折线图。 仅在已经将数据聚合到少量数据点之后，才能考虑使用饼图。  
  
 下图显示了将创建的饼图。  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将学习如何执行以下操作：  
  
1.  [使用图表向导创建饼图](#Chart)  
  
2.  [选择图表类型](#ChartType)  
  
3.  [每个切片中显示百分比](#Percentages)  
  
4.  [将小切片合并为一个切片](#CombineSlices)  
  
5.  [自定义绘图效果](#DrawingEffect)  
  
6.  [添加报表标题](#Title)  
  
7.  [保存报表](#Save)  
  
> [!NOTE]  
>  在本教程中，将向导的多个步骤合并为两个过程。 有关如何转到报表服务器、添加数据源和添加数据集的分步说明，请参阅本系列教程中的第一个教程：[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
 估计的时间才能完成本教程中：10 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Chart"></a> 1.使用图表向导创建饼图  
 从“入门”对话框中使用图表向导创建嵌入数据集，选择共享数据源，并创建饼图。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-create-a-new-chart-report"></a>创建新的图表报表  
  
1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。  
  
     此时将显示“入门”对话框。  
  
    > [!NOTE]  
    >  如果未显示入门对话框中，从报表生成器按钮，单击**新建**。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击“图表向导”。  
  
4.  在“选择数据集”页上，单击“创建数据集”，然后单击“下一步”。  
  
5.  在“选择数据源的连接”页中，选择现有数据源或浏览到报表服务器并选择一个数据源，然后单击“下一步”。 您可能需要输入用户名和密码。  
  
    > [!NOTE]  
    >  只要您具有足够的权限，则选择哪一个数据源并不重要。 您将不会从数据源中获取数据。 有关详细信息，请参阅[获取数据连接的备选方式（报表生成器）](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在 **“设计查询”** 页中，单击 **“编辑为文本”**。  
  
7.  将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  （可选）单击“运行”按钮 (**!**)，查看要用于图表的数据。  
  
9. 单击“下一步” 。  
  
##  <a name="ChartType"></a> 2.选择图表类型  
 可以从各种预定义的图表类型中进行选择。  
  
#### <a name="to-add-a-pie-chart"></a>添加饼图  
  
1.  上**选择图表类型**页上，单击**饼图**，然后单击**下一步**。 将打开“排列图表字段”页。  
  
     在“排列图表字段”页上，将“Product”字段拖到“类别”窗格中。 类别定义了饼图上的切片数。 在本示例中，将有 8 个切片，每个产品对应一个切片。  
  
2.  将“Sales”字段拖到“值”窗格中。 Sales 表示子类别的销售量。 “值”窗格显示 `[Sum(Sales)]`，因为该图表显示的是每个产品的销售总额。  
  
3.  单击“下一步” 。  
  
4.  上**选择一种样式**页上，在样式窗格中，选择一种样式。  
  
     样式指定字形、颜色集和边框样式。 选择样式时，“预览”窗格将显示具有该样式的图表的示例。  
  
5.  单击 **“完成”**。  
  
     图表将添加到设计图面中。  
  
6.  单击图表以显示图表控点。 拖动该图表的右下角以扩大该图表。 请注意，报表设计图面的大小将增大以容纳图表。  
  
7.  单击 **“运行”** 以预览报表。  
  
 报表会显示具有 8 个切片的饼图，每个产品对应一个切片。 每个切片的大小表示该产品在 2004 年的销售额。 其中有三个切片非常薄。  
  
##  <a name="Percentages"></a> 3.在每个切片中显示百分比  
 在饼图的每个切片上，可以显示此切片占整个饼图的百分比。  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>在饼图的每个切片中显示百分比  
  
1.  切换到报表设计视图。  
  
2.  右键单击饼图，然后单击“显示数据标签”。 数据标签会显示在图表上。  
  
3.  右击标签，然后依次**序列标签属性**。  
  
4.  在标签数据，从下拉列表框中，选择 **#PERCENT**。  
  
     若要将值显示为百分比，则 UseValueAsLabel 属性必须为 false。 如果系统提示设置此值，请在“确认操作”对话框中单击“是”。  
  
5.  （可选）若要指定标签显示的小数位数，请键入`#PERCENT{Pn}`其中*n*是要显示的小数位数数字。 例如，若要不显示小数位数，请键入`#PERCENT{P0}`。  
  
    > [!NOTE]  
    >  设置百分比格式时，“序列标签属性”对话框中的“数字格式”不起作用。 它将标签的格式设置为百分比，但不会计算每一切片占饼图的百分比。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  单击 **“运行”** 以预览报表。  
  
 报表会显示每个饼图切片占总体的百分比。  
  
##  <a name="CombineSlices"></a> 4.将多个小型切片合并为一个切片  
 在饼图所包含的切片中，有三个切片非常小。 可以将多个小型切片合并为一个表示所有这些小型切片的大型切片。  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>将饼图上所有小于 5% 的切片组合为一个切片  
  
1.  切换到报表设计视图。  
  
2.  上**视图**选项卡上，在**显示/隐藏**组中，选择**属性**。  
  
3.  在设计图面上，单击饼图的任一切片。 序列的属性将显示在“属性”窗格中。  
  
4.  在 **“常规”** 部分，展开 **CustomAttributes** 节点。  
  
5.  将“CollectedStyle”属性设置为“SingleSlice”。  
  
6.  确保将“CollectedThreshold”属性设置为“5”。  
  
7.  确保将“CollectedThresholdUsePercent”属性设置为“True”。  
  
8.  在功能区中，在**主页**选项卡上，单击**运行**以预览报表。  
  
 现在，在图例中已存在类别“其他”。 新饼图切片将所有小于 5% 的切片组合成一个占整个饼图 6% 的切片。  
  
##  <a name="DrawingEffect"></a> 5.自定义绘图效果  
 在图表向导中，饼图的默认样式为“海蓝色”，这将呈现凹陷绘图效果。 可以在运行改向导后更改此样式。  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>向饼图添加绘制效果  
  
1.  切换到报表设计视图。  
  
2.  如果属性窗格未打开，在**视图**选项卡上，选择**属性**。  
  
3.  双击饼图本身。 饼图的序列属性将会显示在“属性”窗格中。  
  
4.  在“属性”窗格中，展开 **CustomAttributes** 节点。  
  
5.  设置**PieDrawingStyle**到**SoftEdge**。  
  
    > [!NOTE]  
    >  绘图效果和三维效果是相互排斥的选项。 如果图表应用了三维效果， **PieDrawingStyle**属性窗格上不可用。  
  
6.  单击 **“运行”** 以预览报表。  
  
 下图显示了具有软边效果的饼图。  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="Title"></a> 6.添加报表标题  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”。  
  
2.  键入 **Camera and Camcorder Sales**，按 Enter，然后键入 **As a Percentage of Total Sales**，如下所示：  
  
     **Camera and Camcorder Sales**  
  
     **As a Percentage of Total Sales**  
  
3.  选择**Camera and Camcorder Sales**，然后单击**加粗**按钮**字体**一部分**主页**功能区选项卡。  
  
4.  选择**作为 a Percentage of Total Sales**，然后在**字体**部分**主页**选项卡上，将字号设置为**10**。  
  
5.  （可选）您可能需要使“标题”文本框更高一些，以容纳两行文本。  
  
     此标题将显示在报表的顶部。 未定义页标头时，报表体顶部的项就等同于报表标头。  
  
6.  单击 **“运行”** 以预览报表。  
  
##  <a name="Save"></a> 7.保存报表  
  
#### <a name="to-save-the-report"></a>保存报表  
  
1.  切换到报表设计视图。  
  
2.  从“报表生成器”按钮，单击 **“另存为”**。  
  
3.  在“名称”中，键入“Sales Pie Chart”。  
  
4.  单击“保存” 。  
  
 报表将保存在报表服务器上。  
  
## <a name="next-steps"></a>后续步骤  
 这样，您就成功完成了“向报表添加饼图”教程的学习。 若要了解有关图表的详细信息，请参阅[图表（报表生成器和 SSRS）](report-design/charts-report-builder-and-ssrs.md)和[迷你图和数据条（报表生成器和 SSRS）](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
