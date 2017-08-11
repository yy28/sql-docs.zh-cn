---
title: "教程： 将一个柱形图添加到报表 （报表生成器） |Microsoft 文档"
ms.custom: 
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c231648deb4920a3e36a594271d1c9c199313668
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>教程：向报表添加柱形图（报表生成器）
本教程中将创建 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分页报表，该报表包含一个柱形图，将序列显示为一组按类别分组的垂直条。 

柱形图对以下方面很有用：  
  
-   显示一段时间内数据的更改。  
-   比较多个序列的相对值。  
-   显示移动平均线，以显示趋势。  
  
下图显示了将创建的带有移动平均线的柱形图。  
  
![report-builder-column-chart-tutorial](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> 在本教程中，将向导的多个步骤合并为一个过程。 有关如何浏览到报表服务器、选择数据源和创建数据集的分步说明，请参阅本系列中的第一个教程：[教程：创建基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
本教程的预计学时：15 分钟。  
  
## <a name="requirements"></a>需求  
有关要求的信息，请参阅[教程先决条件（报表生成器）](../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
## <a name="Chart"></a>1.使用图表向导创建图表报表  
在本部分中，使用图表向导创建嵌入数据集、选择共享数据源并创建柱形图。  
  
> [!NOTE]  
> 在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
### <a name="to-create-a-chart-report"></a>创建图表报表  
  
1.  通过计算机、[Web 门户或 SharePoint 集成模式](../reporting-services/report-builder/start-report-builder.md) 启动报表生成器 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    将打开“新建报表或数据集”对话框。  
  
    如果未出现“新建报表或数据集”对话框，请通过“文件”菜单转至“新建”。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击**图表向导**。  
  
4.  上**选择数据集页**，单击**创建数据集**，然后单击**下一步**。  
  
5.  上**选择数据源的连接**页上，选择现有的数据源或浏览到报表服务器并选择数据源，，然后单击**下一步**。 您可能需要输入用户名和密码。  
  
    > [!NOTE]  
    > 只要您具有足够的权限，则选择哪一个数据源并不重要。 您将不会从数据源中获取数据。 有关详细信息，请参阅[获取数据连接的备选方式（报表生成器）](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
6.  在“设计查询”页上，单击“编辑为文本”。  
  
7.  将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  （可选）单击“运行”按钮 (**!**)，查看要用于图表的数据。  
  
9. 单击“下一步” 。  
  
## <a name="ChartType"></a>2.选择图表类型  
可从几种预定义的图表类型中进行选择，完成向导后可修改图表。  
  
### <a name="to-add-a-column-chart"></a>添加柱形图  
  
1.  上**选择图表类型**页上，柱形图是默认图表类型。 单击“下一步” 。  
  
2.  上**排列图表字段**页上，销售日期将字段拖动到**类别**。 “类别”显示在水平轴上。  
  
3.  销售将字段拖动到**值**。 **值**框显示 sum （sales），因为销售的总计值的总和聚合的每个日期。 “值”显示在垂直轴上。  
  
4.  单击“下一步” 。  
 
6.  单击 **“完成”**。  
  
    图表将添加到设计图面中。 请注意，新的柱形图只显示代表性数据。 图例标有 Sales Date A、Sales Date B 等，只为大概给出报表的外形。 
    
    ![report-builder-column-chart-1-design-view](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  单击图表以显示图表控点。 拖动该图表的右下角以扩大该图表。 请注意，报表设计图面的大小将增大以容纳图表。  
  
8.  单击 **“运行”** 以预览报表。  

    ![report-builder-column-chart-1-preview](../reporting-services/media/report-builder-column-chart-1-preview.png)

请注意，图表不会在水平轴上显示每个类别的标签。 默认情况下，仅包括适合放在轴旁边的标签。 
  
## <a name="Horizontal"></a>3.设置水平轴上的日期格式  
默认情况下，水平轴采用常用格式显示值，将自动调整为适合图表的大小。  
  
1.  切换到报表设计视图。  
  
2.  右键单击水平轴 >**水平轴属性**。  
  
3.  上**数**选项卡上，在**类别**，选择**日期**。  
  
5.  在**类型**框中，选择**31 年 1 月 2000年**。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  在主页选项卡上，单击**运行**以预览报表。  
  
日期会以您选择的日期格式显示。 图表仍不会在水平轴上显示每个类别的标签。 

![report-builder-column-chart-2-preview](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
通过旋转标签和指定间隔，可以自定义标签显示方式。  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4.旋转水平轴上的轴标签  
  
1.  切换到报表设计视图。  
  
2.  右键单击水平轴标题，然后单击**显示轴标题**以删除标题。 因为水平轴显示日期，所以不需要标题。  
  
3.  右键单击水平轴 >**水平轴属性**。  
  
5.  上**标签**选项卡上，在**更改轴标签自动调整选项**，选择**禁用自动调整**。  
  
7.  在**标签旋转角度**，选择**-90**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    水平轴的示例文本将旋转 90 度。  
    
    ![report-builder-column-chart-rotate-x-axis](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. 单击 **“运行”** 以预览报表。  
  
在图表中，会标签旋转。  

![report-builder-column-chart-rotate-x-axis-preview](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="Legend"></a>5.移动图例  
系统会根据类别和序列数据自动创建图例。 可在柱形图的图表区域的下方移动图例。  
  
1.  切换到报表设计视图。  
  
2.  右键单击图表上的图例 >**图例属性**。  
  
3.  下**布局和位置**，选择一个不同的位置。 例如，选择底部中间选项。  
  
    如果将图例置于图表的顶部或底部，则图例的布局将会从垂直改为水平。 你可以选择一个不同的布局中**布局**框。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  （可选）因为本教程中只有一个类别，所以图表不需要图例。 若要删除它，右键单击图例 >**删除图例**。  
  
6.  单击 **“运行”** 以预览报表。  
  
## <a name="ChartTitle"></a>6.设置图表的标题  
    
1.  切换到报表设计视图。  
  
2.  选择的单词**图表标题**在图表的顶部，然后键入**应用商店销售订单合计**。  
  
3.  单击 **“运行”** 以预览报表。  
  
## <a name="Vertical"></a>7.设置垂直轴的格式和标签  
默认情况下，垂直轴采用常用格式显示值，将自动调整为适合图表的大小。   
  
1.  切换到报表设计视图。  
  
2. 单击图表左侧垂直轴上的标签以选择它们。  
  
3.  上**主页**选项卡 >**数**组中，单击**货币**按钮。 轴标签将更改以显示货币格式。  
  
4.  单击**减少小数位数**按钮两次，以显示数字舍入为最接近美元。  
  
5.  右键单击垂直轴 >**垂直轴属性**。  
  
6.  上**数**选项卡上，请注意，**货币**中已选择**类别**框中，和**小数位数**已**0** （零）。  
  
7.  检查**值的显示位置**。 **千位**已被选中。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 右键单击垂直轴 >**显示轴标题**。 

10. 右键单击垂直轴标题 >**轴标题属性**。  
  
10. 替换中的文本**标题文本**字段**总 （以千为单位） 上的销售**。 还可以指定与如何设置标题格式相关的多种选项。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 单击 **“运行”** 以预览报表。  

    ![report-builder-column-chart-format-y-axis](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8.水平 (x) 轴上显示所有标签

你会注意到 x 轴上仅显示了部分标签。 在本部分中，可在“属性”窗格设置属性以显示所有标签。

1.  切换到报表设计视图。  
  
2.  单击图表，然后选择水平轴标签。

3. 在“属性”窗格中，将 LabelInterval 设置为 1。

    ![report-builder-column-chart-set-label-interval](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    该图表同设计视图中一样。 
    
5.  单击 **“运行”** 以预览报表。

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    现在，图表显示其所有标签。
  
## <a name="Average"></a>9.添加带已计算序列的移动平均线  

移动平均值是序列中数据的平均值，它是根据一段时间内的数据计算的。 移动平均线可以确定趋势。
  
1.  切换到报表设计视图。  
  
2.  双击图表以显示**图表数据**窗格。  
  
3.  右键单击**[sum （sales)]**字段**值**区域中，然后单击**添加计算系列**。  

     ![report-builder-column-chart-add-calculated-series](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  在**公式**，验证**移动平均线**选择。  
  
5.  在**设置公式参数**，为**段**，选择**4**。  
  
6.  上**边框**选项卡上，在**线条宽度**，选择**3pt**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 单击 **“运行”** 以预览报表。  
  
图表将显示一条线条，它按日期显示销售总计的移动平均线，每隔四天计算一次平均值。 阅读更多有关 [向图表添加移动平均线](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)的信息。 

![report-builder-column-chart-moving-average](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="Title"></a>10.添加报表标题  
  
1.  切换到报表设计视图。  
  
2.  在设计图面上，单击“单击以添加标题”。  
  
3.  键入 **Sales Chart**，再按 Enter，然后键入 **January to December 2015**，内容如下所示：  
  
    **Sales Chart**  
  
    **January to December 2015**  
  
4.  选择“Sales Chart”，然后转至“主文件夹”选项卡 > “字体”部分 > “粗体”。  
  
5.  选择**到 2015 年 12 月的 1 月**，然后在**主页**选项卡 >**字体**部分 > 将字体大小设置为**10**。  
  
6.  （可选）你可能需要进行**标题**高度以适应行文本的两行的文本框。 单击下边缘中间，显示双向箭头时下拉。 并且可能需要拖动图表的顶部，使标题不重叠。  
  
    此标题将出现在报表的顶部。 未定义页标头时，报表体顶部的项就等同于报表标头。  
  
7.  单击 **“运行”** 以预览报表。  
  
## <a name="Save"></a>11.保存报表  
  
### <a name="to-save-the-report"></a>保存报表  
  
1.  切换到报表设计视图。  
  
2.  从“报表生成器”按钮，单击 **“另存为”**。  

    可将其保存到计算机或报表服务器中。
  
3.  在**名称**，类型**销售订单柱形图**。  
  
4.  单击 **“保存”**。  
  
## <a name="next-steps"></a>后续步骤  
您已成功完成“向报表添加柱形图”教程。 若要了解有关图表的详细信息，请参阅[图表 &#40;报表生成器和 SSRS &#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md)和[迷你图和数据条 &#40;报表生成器和 SSRS &#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>另請參閱  
-    [报表生成器教程](../reporting-services/report-builder-tutorials.md) 
-    [SQL Server 2016 中的报表生成器](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


