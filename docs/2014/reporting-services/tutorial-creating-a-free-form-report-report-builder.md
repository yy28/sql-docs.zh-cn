---
title: 教程：创建自由格式的报表（报表生成器） | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: eaf7f68cb2658b50bf21ea188324f5208acd488a
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56286797"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>教程：创建自由格式的报表（报表生成器）
  本教程教你如何创建一个与书信格式类似的 SSRS 自由格式报表。 你可以排列报表项来创建一个具有文本框、图像和其他数据区域的窗体。  
  
 你在本教程中创建的报表是基于教程中包括的示例销售数据创建的。 该报表按地区对信息进行分组，并且显示该地区的销售经理的姓名以及详细和汇总销售信息。 您将使用列表数据区域作为自由格式的报表的基础，然后添加具有图像的装饰性面板、插入了数据的静态文本、用于显示详细信息的表以及可选的用于显示汇总信息的饼图和柱形图。  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将了解如何执行下列操作：  
  
-   [创建空白报表、 数据源和数据集](#BlankReport)  
  
-   [添加并配置列表](#List)  
  
-   [添加图形](#Graphics)  
  
-   [添加自由格式文本](#Text)  
  
-   [添加一个表以显示详细信息](#Table)  
  
-   [数据格式](#Format)  
  
-   [保存报表](#Save)  
  
### <a name="other-optional-steps"></a>其他可选步骤  
  
-   [添加线条以便分隔报表区域](#Line)  
  
-   [添加汇总数据可视化](#Visualization)  
  
 本教程的预计学时：20 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="BlankReport"></a> 1.创建空白报表、数据源和数据集  
  
> [!NOTE]  
>  在本教程中，查询包含了数据值，这样报表则不需要外部数据源。 使用此内部数据类型对达成学习目标非常有益，但是该方法会使查询变得很长。 .  
  
#### <a name="to-create-a-blank-report"></a>创建空白报表  
  
1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。  
  
    > [!NOTE]  
    >  此时应显示 **“入门”** 对话框。 如果未显示该对话框，则从“报表生成器”按钮，单击 **“新建”**。  
  
2.  在 **“入门”** 对话框的左窗格中，确保已选择 **“新建报表”** 。  
  
3.  在右窗格中，单击 **“空白报表”**。  
  
#### <a name="to-create-a-new-data-source"></a>创建新数据源  
  
1.  在“报表数据”窗格中，单击 **“新建”**，然后单击 **“数据源”**。  
  
2.  在`Name`框中，键入：**ListDataSource**  
  
3.  单击 **“使用我的报表中嵌入的连接”**。  
  
4.  验证连接类型是否为 Microsoft SQL Server，然后在“连接字符串”框中键入：数据源 = \<servername>  
  
     \<服务器名称 >，例如，Report001，指定在其安装的 SQL Server 数据库引擎实例的计算机。 因为报表数据不是从 SQL Server 数据库提取的，所以不需要包括数据库的名称。 指定服务器上的默认数据库用于对查询进行分析。  
  
5.  单击 **“凭据”**，然后输入连接至 SQL Server 数据库引擎实例所需的凭据。  
  
6.  单击“确定” 。  
  
#### <a name="to-create-a-new-dataset"></a>新建数据集  
  
1.  在“报表数据”窗格中，单击 **“新建”**，然后单击 **“数据集”**。  
  
2.  在`Name`框中，键入：**ListDataset。**  
  
3.  单击“使用在我的报表中嵌入的数据集” ，然后验证数据源是否为 **ListDataSource**。  
  
4.  确保已选择 **“文本”** 查询类型，然后单击 **“查询设计器”**。  
  
5.  单击 **“编辑为文本”**。  
  
6.  复制并将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  单击“运行”图标以运行查询。  
  
     查询结果将是可用于在您的报表中显示的数据。  
  
     ![查询设计器](../../2014/tutorials/media/tutorial-querydesigner.png "查询设计器")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="List"></a> 2.添加并配置列表  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供三个数据区域模板：表、矩阵和列表。 这些模板全都基于 Tablix 数据区域。  
  
 在本教程中，你将使用一个列表来显示一个类似新闻稿的报表中各销售区域的销售信息。 这些信息按地区分组。 您将添加一个按地区对数据进行分组的新行组，然后删除内置的“详细信息”行组。 该列表模板是创建自由格式报表的理想工具。 有关详细信息，请参阅[列出了&#40;报表生成器和 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  此报表使用纸张大小 Letter (8.5 X11) 以及 1 英寸的边距。 高于 9 英寸或宽于 6 1/2 英寸的报表页可能会生成空白页。  
  
#### <a name="to-add-a-list"></a>添加列表  
  
1.  在功能区的 **“插入”** 选项卡的 **“数据区域”** 区域中，单击 **“列表”** ，然后将该列表拖到表体内。 将列表设为 7 英寸高，6.25 英寸宽。  
  
2.  在列表内单击，右键单击列表顶部，然后单击 **“Tablix 属性”**。  
  
     ![添加列表](../../2014/tutorials/media/tutorial-addinglistwithnumbers.png "添加列表")  
  
3.  在 **“数据集名称”** 下拉列表中，选择 **ListDataset**。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  在列表内右键单击，然后单击 **“矩形属性”**。  
  
     ![矩形属性命令](../../2014/tutorials/media/tutorial-rectanglepropertiescommand.png "矩形属性命令")  
  
6.  在 **“常规”** 选项卡中，选中 **“在组件后面添加分页符”** 复选框。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>添加新行组和删除“详细信息”组  
  
1.  在“行组”窗格中，右键单击“详细信息”组，指向 **“添加组”**，然后单击 **“父组”**。  
  
     ![父组命令](../../2014/tutorials/media/tutorial-parentgroupcommand.png "父组命令")  
  
2.  在下拉列表中，选择 `[Territory].`。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     将一列添加到该列表中。 该列包含单元 `[Territory].`。  
  
4.  右键单击列表中的 Territory 列，然后单击 **“删除列”**。  
  
     ![删除列](../../2014/tutorials/media/tutorial-deletecolumnscommand.png "删除列")  
  
5.  单击 **“仅删除列”**。  
  
     ![删除列对话框](../../2014/tutorials/media/tutorial-deletecolumnsdialog.png "删除列对话框")  
  
6.  在“行组”窗格中，右键单击 **“详细信息”** 组，然后单击 **“删除组”**。  
  
     ![删除详细信息组](../../2014/tutorials/media/tutorial-deletedetailsgroup.png "删除详细信息组")  
  
7.  单击 **“仅删除组”**。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Graphics"></a> 3.添加图形  
 使用列表数据区域的好处之一是，您可以将矩形和文本框之类的报表项添加到任何地方，而不会被限制为表格布局。 您将通过添加图形（用颜色填充的矩形）增强报表的外观。  
  
#### <a name="to-add-graphic-elements-to-the-report"></a>向报表添加图形元素  
  
1.  上**插入**选项卡的功能区中，单击**矩形**，然后将一个矩形拖到列表的左上角。 使该矩形 7 英寸高，1 英寸宽。  
  
2.  右键单击该矩形，再单击 **“矩形属性”**。  
  
3.  单击 **“填充”** 选项卡。  
  
4.  在 **“填充颜色”** 下拉列表中，单击 **“其他颜色”**，然后选择 **“深灰”** 色。  
  
     ![选择填充颜色](../../2014/tutorials/media/tutorial-selectfillcolorwithnumbers.png "选择填充颜色")  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  单击 **“运行”** 以预览报表。  
  
 该报表的左侧现在具有一个垂直图形，该图形由一个深灰色的矩形构成。  
  
##  <a name="Text"></a> 4.添加自由格式的文本  
 文本框包含在每个报表页上都重复的静态文本以及多个数据字段。  
  
#### <a name="to-add-text-to-the-report"></a>向报表添加文本  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  在功能区的 **“插入”** 选项卡上，单击 **“文本框”**，然后将一个文本框拖到该列表的左上角，但放在你以前添加的矩形内。 使该文本框大约 3 英寸高，5 英寸宽。  
  
3.  将光标置于文本框的上部，然后键入：Newsletter for。  
  
     ![添加新闻稿标题文本](../../2014/tutorials/media/tutorial-newsletterfor.png "添加新闻稿标题文本")  
  
    > [!NOTE]  
    >  请确保在“for”一词之后包含一个多余的空格。 该空格用于将文本以及您将在下一步骤中添加的字段分隔开来。  
  
4.  将 Territory 字段拖到该文本框，然后将其置于您在步骤 3 中键入的文本之后。  
  
     ![添加 Territorial 字段](../../2014/tutorials/media/tutorial-addterritorialfield.png "添加 Territorial 字段")  
  
5.  选择所有文本，右键单击，然后单击 **“文本属性”**。  
  
6.  单击 **“字体”** 选项卡。  
  
7.  在 **“字体”** 列表中，选择 **“Times New Roman”**；在 **“字号”** 中，选择 **“20 pt”**；在 **“颜色”** 中，选择 **“红色”**。  
  
     ![文本属性](../../2014/tutorials/media/tutorial-textpropertieswithnumbers.png "文本属性")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 将光标置于你在步骤 3 中键入的文本之下，然后键入：**Hello** 。  
  
    > [!NOTE]  
    >  请确保在“Hello”一词之后包含一个多余的空格。 该空格用于将文本以及您将在下一步骤中添加的字段分隔开来。  
  
10. 将 FullName 字段拖到该文本框，将其置于您在步骤 9 中键入的文本之后，然后键入一个逗号 (,)。  
  
     ![添加完整的名称字段](../../2014/tutorials/media/tutorial-addfullnamefield.png "添加完整名称字段")  
  
11. 选择您在步骤 9 和 10 中添加的文本，右键单击，然后单击 **“文本属性”**。  
  
12. 单击 **“字体”** 选项卡。  
  
13. 在 **“字体”** 列表中，选择 **“Times New Roman”**；在 **“字号”** 中，选择 **“16 pt”**；在 **“颜色”** 中，选择 **“黑色”** 。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 将光标置于您在步骤 9 到 13 中添加的文本的下方，然后复制并粘贴以下“难懂的”文本：  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
    Nulla facilisi. Proin ligula enim, porta ut tincidunt id, adipiscing sit amet eros. Ut purus sem, bibendum et vulputate sit amet, facilisis eget magna. Sed aliquam erat non erat eleifend hendrerit. Ut a ligula est, sit amet eleifend enim. Ut et nisl enim, sit amet adipiscing augue. Vivamus eu arcu ac libero posuere elementum. Integer condimentum bibendum venenatis. Integer odio tellus, feugiat in pellentesque semper, interdum nec sem. Sed cursus euismod sem, ut elementum sapien placerat vel.   
    ```  
  
16. 选择您在步骤 15 中添加的文本，右键单击，然后单击 **“文本属性”**。  
  
17. 单击 **“字体”** 选项卡。  
  
18. 在 **“字体”** 列表中，选择 **“Arial”**；在 **“字号”** 中，选择 **“10 pt”**；在 **“颜色”** 中，选择 **“黑色”**。  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![添加新闻稿文本](../../2014/tutorials/media/tutorial-newslettertext.png "添加新闻稿文本")  
  
20. 将光标置于你在步骤 15 中粘贴的文本之下，然后键入：**恭喜你销售总额的**。  
  
    > [!NOTE]  
    >  请确保在“of”一词之后包含一个多余的空格。 该空格用于将文本以及您将在下一步骤中添加的字段分隔开来。  
  
21. 将 Sales 字段拖到该文本框，将其置于您在步骤 20 中键入的文本之后，然后键入一个感叹号 (!)。  
  
22. 突出显示销售量字段，右键单击该字段，然后单击**表达式**。  
  
23. 在表达式框中，更改表达式以便包括 Sum 函数，如下所示：  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![将表达式添加到销售字段](../../2014/tutorials/media/tutorial-addexpressiontosalesfield.png "向 sales 字段添加表达式")  
  
25. 选择您在步骤 20 到 23 中添加的文本，右键单击，然后单击 **“文本属性”**。  
  
26. 单击 **“字体”** 选项卡。  
  
27. 在 **“字体”** 列表中，选择 **“Times New Roman”**；在 **“字号”** 中，选择 **“16 pt”**；在 **“颜色”** 中，选择 **“红色”**。  
  
28. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
29. 选择 `[Sum(Sales)]` ，在功能区的 **“主文件夹”** 选项卡的 **“编号”** 组中，单击 **“货币”** 按钮。  
  
     ![添加货币符号](../../2014/tutorials/media/tutorial-addcurrencysymbol.png "添加货币符号")  
  
30. 右键单击包含“单击以添加标题”文本的文本框，然后单击 **“删除”**。  
  
31. 选择列表框，并且使用箭头键将其移到页面的顶部。  
  
32. 单击 **“运行”** 以预览报表。  
  
 报表将显示静态文本，并且每个报表页都包括属于某个地区的数据。 销售额的格式设为货币。  
  
 ![新闻稿预览](../../2014/tutorials/media/tutorial-newsletters.png "新闻稿预览")  
  
##  <a name="Table"></a> 5.添加一个表以显示销售详细信息  
 使用新建表和矩阵向导可以将表添加到自由格式的报表。 完成向导后，您将手动添加一个合计行。  
  
#### <a name="to-add-a-table"></a>添加表  
  
1.  在功能区的 **“插入”** 选项卡的 **“数据区域”** 区域中，单击 **“表”**，然后单击 **“表向导”**。  
  
2.  在“选择数据集”页上，单击 **ListDataset**。  
  
3.  单击“下一步” 。  
  
4.  在“排列字段”页上，将“Product”字段从“可用字段”拖到“值”中。  
  
5.  对于 SalesDate、Quantity 和 Sales，重复执行步骤 4。 将 SalesDate 放置于 Product 之下，将 Quantity 放置于 SalesDate 之下，并且将 Sales 放置于 SalesDate 之下。  
  
6.  单击“下一步” 。  
  
7.  在 **“选择布局”** 页上，查看表的布局。  
  
     该表非常简单。 它由五列构成，没有行组或列组。 因为它不具有组，所以与组相关的布局选项不可用。 您将手动更新该表以便包括本教程后面部分中的总计。  
  
8.  单击“下一步” 。  
  
9. 在 **“选择样式”** 页的 **“样式”** 窗格中，选择 **“石板”**。  
  
10. 单击 **“完成”**。  
  
11. 将该表拖到您在第 4 课中添加的文本框之下。  
  
    > [!NOTE]  
    >  请确保该表位于列表内。  
  
12. 确认表已选，然后在“行组”窗格中，右键单击“详细信息”，指向 **“添加总计”**，然后单击 **“之后”**。  
  
     ![添加报表总数](../../2014/tutorials/media/tutorial-addtotal.png "添加报表总数")  
  
13. 单击 **“运行”** 以预览报表。  
  
 该报表将显示具有销售详细信息和总计的一个表。  
  
 ![在报表中的销售总额](../../2014/tutorials/media/tutorial-reportsalestotals.png "报表中的销售总额")  
  
##  <a name="Format"></a> 6.设置数据格式  
 将数字数据的格式设为货币，将日期格式设为仅限天和时间。  
  
#### <a name="to-format-fields-table"></a>设置字段表的格式  
  
1.  单击 **“设计”** 切换到设计视图。  
  
2.  单击包含 `[Sum(SalesSales)]` 的表单元，然后在 **“主文件夹”** 选项卡上的 **“数字”** 组中，单击 **“货币”** 按钮。  
  
     ![向总销售额添加货币符号](../../2014/tutorials/media/tutorial-sumsales-currencysymbol.png "向总销售额添加货币符号")  
  
3.  单击包含 `[SalesDate]` 的单元，然后在 **“数字”** 组上，从下拉列表中选择 **“日期”**。  
  
4.  单击 **“运行”** 以预览报表。  
  
 报表现在将显示设置了格式的数据并且更易于阅读。  
  
 ![设置格式在报表中的销售总额](../../2014/tutorials/media/tutorial-reportsalestotals-formatted.png "格式在报表中的销售总额")  
  
##  <a name="Save"></a> 7.保存报表  
 您可以将报表保存到报表服务器、SharePoint 库或本地计算机。 你还可以运行报表并从  “导出”菜单选择格式，将报表以各种格式导出（如 Word 和 PDF）。  
  
 在本教程中，将报表保存到报表服务器。 如果您没有对报表服务器的访问权限，则可以保存到您的计算机。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“最近使用的站点和服务器”**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为报表默认位置的报表文件夹的内容。  
  
4.  在中`Name`，替换默认名称**SalesInformationByTerritory**。  
  
5.  单击“保存” 。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>将报表保存到计算机上  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“桌面”**、 **“我的文档”** 或 **“我的电脑”**，然后浏览到要将报表保存到的文件夹。  
  
3.  在中`Name`，替换默认名称**SalesInformationByTerritory**。  
  
4.  单击“保存” 。  
  
##  <a name="Line"></a> 8.（可选）添加线条以便分隔报表区域  
 添加线条可以分隔报表的可编辑区域和详细信息区域。  
  
#### <a name="to-add-a-line"></a>添加线条  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  在功能区的 **“插入”** 选项卡的 **“报表项”** 区域中，单击 **“线条”**。  
  
3.  将一个线条拖到您在第 4 课中添加的自由格式的文本框之下。  
  
4.  单击该线条。  
  
5.  单击 **“主文件夹”** 选项卡。  
  
6.  在 **“边框”** 区域中，对于宽度选择 **4 1/2** pt，对于颜色选择 **“红色”**。  
  
     ![向报表添加线条](../../2014/tutorials/media/tutorial-reportwithline.png "将行添加到报表")  
  
##  <a name="Visualization"></a> 9.（可选）添加汇总数据可视化  
 矩形有助于控制报表的呈现方式。 将饼图和柱形图放置于矩形内，可以确保报表以您所需的方式呈现。  
  
#### <a name="to-add-a-rectangle"></a>添加矩形  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  在功能区的 **“插入”** 选项卡的 **“报表项”** 区域中，单击 **“矩形”**，然后将该矩形拖到列表内表的右侧。 使该矩形 2 英寸宽，4 英寸高。  
  
3.  将矩形的顶部和表的顶部对齐。  
  
#### <a name="to-add-a-pie-chart"></a>添加饼图  
  
1.  在功能区 **“插入”** 选项卡上的 **“数据可视化”** 区域中，单击 **“图表”** ，然后单击 **“图表向导”**。  
  
2.  在“选择数据集”页中，单击 **ListDataset**，然后单击 **“下一步”**。  
  
3.  单击 **“饼图”**，然后单击 **“下一步”**。  
  
4.  在“排列图表字段”页上，将“Product”拖到“类别”中。  
  
5.  将 Quantity 拖到**值**，然后单击**下一步**。  
  
6.  在 **“选择样式”** 页的 **“样式”** 窗格中，选择 **“石板”**。  
  
7.  单击 **“完成”**。  
  
8.  调整在报表的左上角中出现的图表大小，使其为 1 1/2 英寸高，2 英寸宽。  
  
9. 将图表拖至该矩形内。  
  
     ![添加饼图](../../2014/tutorials/media/tutorial-addpiechart.png "添加饼图")  
  
10. 右键单击图表标题，然后单击 **“标题属性”**。  
  
11. 在中**图表标题属性**对话框中的，标题文本中，键入：Product Quantities Sold。  
  
12. 单击 **“字体”** 选项卡，然后在 **“大小”** 列表中，单击 **10pt**。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-column-chart"></a>添加柱形图  
  
1.  在功能区 **“插入”** 选项卡上的 **“数据可视化”** 区域中，单击 **“图表”** ，然后单击 **“图表向导”**。  
  
2.  在 **“选择数据集”** 页上，单击 **ListDataset**，然后单击 **“下一步”**。  
  
3.  单击 **“柱形”**，然后单击 **“下一步”**。  
  
4.  在排列图表字段页上，拖动到产品字段**类别**。  
  
5.  将“Sales”拖到“值”中，然后单击“下一步”。  
  
     “值”显示在垂直轴上。  
  
6.  在 **“选择样式”** 页的 **“样式”** 窗格中，选择 **“石板”**。  
  
7.  单击 **“完成”**。  
  
     一个柱形图将添加到报表的左上角。  
  
8.  调整图表的大小，使其 2 英寸宽，2 英寸高。  
  
9. 将图表拖至该矩形内的饼图之下。  
  
     ![添加柱形图](../../2014/tutorials/media/tutorial-addcolumnchart.png "添加柱形图")  
  
10. 右键单击图表标题，然后单击 **“标题属性”**。  
  
11. 在中**图表标题属性**对话框中的，标题文本中，键入：Product Sales。  
  
12. 单击 **“字体”** 选项卡，然后在 **“大小”** 列表中，单击 **10pt**，然后单击 **“确定”**。  
  
13. 在柱形图中，右键单击垂直轴，然后取消选中 **“显示轴标题”**。  
  
14. 对于水平轴，重复执行步骤 13。  
  
15. 右键单击图例，然后单击 **“删除图例”**。  
  
    > [!NOTE]  
    >  删除轴标题和图例将在图表为较小大小时更容易阅读。  
  
 ![更改图表标题并删除轴标题](../../2014/tutorials/media/tutorial-columnchart-newtitle-noaxistitle.png "更改图表标题并删除轴标题")  
  
#### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>确认图表位于矩形内  
  
1.  单击你在本课程前面部分添加的矩形。  
  
     在“属性”窗格中，`Name` 属性显示矩形的名称。  
  
     ![矩形的名称](../../2014/tutorials/media/tutorial-rectanglename.png "矩形的名称")  
  
2.  单击饼图。  
  
3.  在中**属性**窗格中，验证`Parent`属性包含矩形的名称。  
  
     ![父属性有关饼图](../../2014/tutorials/media/tutorial-piechart-parentproperty.png "父饼形图的属性")  
  
4.  单击柱形图，重复执行步骤 2 和 3。  
  
    > [!NOTE]  
    >  如果这些图表不位于矩形内，则呈现的报表不会一起显示这些图表。  
  
#### <a name="to-make-the-charts-the-same-size"></a>使图表具有相同大小  
  
1.  单击饼图，按下 Ctrl 键，然后单击柱形图。  
  
2.  选择这两个图表，右键单击，指向 **“布局”**，然后单击 **“使宽度相同”**。  
  
     ![使图表宽度相同](../../2014/tutorials/media/tutorial-makechartssamewidth.png "使图表宽度相同")  
  
    > [!NOTE]  
    >  你首先单击的项决定所有选定项的宽度。  
  
3.  单击 **“运行”** 以预览报表。  
  
 报表现在将在饼图和柱形图中显示汇总销售数据。  
  
 ![SSRS 教程，自由格式的报表](../../2014/tutorials/media/tutorial-reportfinal.png "SSRS 教程，自由格式的报表")  
  
## <a name="more-information"></a>详细信息  
 有关列表的详细信息，请参阅[表、 矩阵和列表&#40;报表生成器和 SSRS&#41;](report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)，[列出了&#40;报表生成器和 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)， [Tablix 数据区域&#40;报表生成器和 SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md)，并[Tablix 数据区域单元、 行和列&#40;报表生成器&#41;和 SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 有关查询设计器的详细信息，请参阅[查询设计器（报表生成器）](../../2014/reporting-services/query-designers-report-builder.md)和[基于文本的查询设计器用户界面（报表生成器）](report-data/text-based-query-designer-user-interface-report-builder.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
