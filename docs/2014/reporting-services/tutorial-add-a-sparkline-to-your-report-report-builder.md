---
title: 教程：向报表添加迷你图（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 542720be68e6fabd2cb16e25928d73efa4f41d66
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091477"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>教程：向报表添加迷你图（报表生成器）
  在本教程中，您将基于示例销售数据创建一个基本的表报表，然后向该表的单元中添加迷你图。  
  
 您在本教程中创建的报表的增强版本可用作示例 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 报表生成器报表。 有关下载此示例报表和其他内容的详细信息，请参阅[报表生成器示例报表](http://go.microsoft.com/fwlink/?LinkId=184851)。 下图显示与您将创建的报表类似的示例报表。  
  
 ![rs_SparklineMatrixTutorial](../../2014/tutorials/media/rs-sparklinematrixtutorial.gif "rs_SparklineMatrixTutorial")  
  
 视频[如何： 为表 （报表生成器视频） 中创建迷你图](http://technet.microsoft.com/bi/ff871942.aspx)说明了如何使用迷你图创建相似的报表。  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将了解如何执行下列操作：  
  
 1. [创建含有表的报表](#CreateTable)  
  
 2. [表或矩阵向导中创建查询](#Query)  
  
 3. [向表中添加迷你图](#Sparkline)  
  
 4. [水平和垂直方向对齐迷你图](#AlignSparklines)  
  
### <a name="other-optional-steps"></a>其他可选步骤  
 5. [数据格式设置为货币](#FormatCurrency)  
  
 6. [数据格式设置为日期](#FormatDates)  
  
 7. [更改列宽](#Width)  
  
 8. [添加报表标题](#Title)  
  
 9. [保存报表](#Save)  
  
 本教程的预计学时：30 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="CreateTable"></a> 1.创建含有表的报表  
  
#### <a name="to-create-a-report"></a>创建报表  
  
1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。  
  
     **Getting Started**对话框随即打开。  
  
    > [!NOTE]  
    >  如果**Getting Started**对话框不会出现，从**报表生成器**按钮，再单击**新建**。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击“表或矩阵向导”。  
  
4.  在“选择数据集”页上，选择“创建数据集”，然后单击“下一步”。 将打开“选择数据源的连接”页面。  
  
    > [!NOTE]  
    >  本教程不需要具体数据；只需要与 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 数据库的连接。 如果已经具有在“数据源连接”下列出的某一数据源连接，则可以选择该连接并且转到步骤 10。 有关详细信息，请参阅[获取数据连接的备选方式（报表生成器）](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
5.  单击 **“新建”**。 此时将打开 **“数据源属性”** 对话框。  
  
6.  在“名称”中，键入数据源的名称“Product Sales”。  
  
7.  在“选择连接类型”中，确认已选择“Microsoft SQL Server”。  
  
8.  在“连接字符串”中，键入以下文本：  
  
     **数据源 =\<服务器名 >**  
  
     表达式\<服务器名 >，例如，Report001，指定在其安装的 SQL Server 数据库引擎实例的计算机。 因为报表数据不是从 SQL Server 数据库提取的，所以不需要包括数据库的名称。 指定服务器上的默认数据库用于对查询进行分析。  
  
9. 单击 **“凭据”**。 输入访问外部数据源所需的凭据。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     返回至“选择数据源的连接”页。  
  
11. 若要验证是否能连接到数据源，请单击“测试连接”。  
  
     将显示消息“已成功地创建连接”。  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. 单击“下一步” 。  
  
##  <a name="Query"></a> 2.在表向导中创建查询  
 在报表中，可以使用具有预定义查询的共享数据集，也可以创建仅在报表中使用的嵌入数据集。 在本教程中，将创建一个嵌入数据集。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-create-a-query"></a>创建查询  
  
1.  在“设计查询”页中，关系查询设计器处于打开状态。 在本教程中，您将使用基于文本的查询设计器。  
  
2.  单击“编辑为文本”。 基于文本的查询设计器将显示查询窗格和结果窗格。  
  
3.  将以下 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询粘贴到“查询”框中。  
  
    ```  
    SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2010-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  在查询设计器工具栏中，单击“运行”(**!**)。  
  
     该查询运行并显示 **SalesDate**、 **Subcategory**、 **Product**、 **Sales**和 **Quantity**字段的结果集。  
  
5.  单击“下一步” 。  
  
6.  在“排列字段”页上，将 Sales 拖到“值”中。  
  
     **Sales** 由 Sum 函数聚合。 值为 [Sum(Sales)]。  
  
7.  将 Product 拖到“行组”中。  
  
8.  将 SalesDate 拖到“列组”中。  
  
9. 单击“下一步” 。  
  
10. 在“选择布局”页的“选项”下，确认已选择“显示小计和总计”。  
  
     向导的“预览”窗格将显示包含有三行的表。 当您运行报表时，每行将按以下方式显示：  
  
    1.  第一行将对表出现一次以显示列标题。  
  
    2.  第二行将对每个产品重复一次并显示产品名称、每日总计和行总计。  
  
    3.  第三行将对表出现一次以显示总计。  
  
11. 单击“下一步” 。  
  
12. 在 **“选择样式”** 页的 **“样式”** 窗格中，选择 **“石板”**。  
  
     “预览”窗格将显示具有该样式的表的示例。  
  
13. 单击 **“完成”**。  
  
14. 表将添加到设计图面中。 此表有三列和三行。  
  
     在“分组”窗格中查找。 如果未显示“分组”窗格，请在“视图”菜单上，单击“分组”。 “行组”窗格显示一个行组： **Product**。 “列组”窗格显示一个列组： **SalesDate**。 详细信息数据是由数据集查询检索的所有数据。  
  
15. 单击 **“运行”** 以预览报表。  
  
##  <a name="Sparkline"></a> 3.添加迷你图  
  
#### <a name="to-add-a-sparkline-chart-to-a-table"></a>向表中添加迷你图  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  选择表中的“Total”列。  
  
3.  右键单击，指向“插入列”，然后单击“左”。  
  
4.  在新列中，右键单击 [Product] 行中，指向**插入**功能区选项卡，然后依次**迷你图**。  
  
5.  请确保中的第一个迷你图**列**行处于选中状态，然后单击**确定**。  
  
6.  单击要在“图表数据”窗格中显示的迷你图。  
  
7.  单击加号 （+） 在值框中，登录并单击**销售**。  
  
     “Sales”字段中的值现在是迷你图的值。  
  
8.  单击加号 （+） 在类别组框中，登录，然后依次**SalesDate**。  
  
9. 单击 **“运行”** 以预览报表。  
  
     请注意，在表的每一行中都有迷你图，但这些迷你图不正确。 迷你图中的各条形不互连。 在第二行数据中只有四个条形，因此，这些条比第一行中的条宽，因为第一行中有六个条形。 您不能比较每天每个产品的值。 它们之间需要相互对齐。  
  
     还要注意的是，对于每一行，该行的最高的条形是行高。 这也会有误导作用，因为每一行的最大值不相等：Budget Movie-Maker 的最大值是 $10,400，但 Slim Digital 的最大值是 $26,576 — 是前者的两倍还多。 并且，这两行的最大的条形大约为相同高度。 此外，它还需要与其他迷你图相一致。  
  
     ![rs_SprklineMtrxUnaligndBars](../../2014/tutorials/media/rs-sprklinemtrxunaligndbars.gif "rs_SprklineMtrxUnaligndBars")  
  
##  <a name="AlignSparklines"></a> 4.沿水平方向和垂直方向对齐迷你图  
 当迷你图都不使用相同度量值时，则很难阅读。 每个迷你图的水平轴和垂直轴都需要与其他部分匹配。  
  
#### <a name="to-set-alignment-for-the-sparklines-in-the-table"></a>设置表中迷你图的对齐方式  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  右键单击迷你图，然后单击“垂直轴属性”。  
  
3.  选中“对齐轴”复选框。  
  
     Tablix1 显示在列表中。 这是唯一的选项。 该选项设置在各迷你图中条形相对于其他条形的高度。  
  
4.  单击“确定” 。  
  
5.  右键单击迷你图，然后单击“水平轴属性”。  
  
6.  选中“对齐轴”复选框。  
  
     Tablix1 显示在列表中。 这是唯一的选项。 该选项设置在各迷你图中条形相对于其他条形的宽度。 如果某些迷你图中的条形比其他迷你图少，则这些迷你图将对于缺失的数据具有空白空间。  
  
7.  单击“确定” 。  
  
8.  单击“运行”，再次预览报表。  
  
 请注意，所有条形现在与其他行中的条形对齐。  
  
##  <a name="FormatCurrency"></a> 5.（可选）将数据格式设置为货币格式  
 默认情况下，“Sales”字段的汇总数据显示为常规数字。 请设置其格式，以使其显示货币形式的数字。 切换“占位符样式”，将格式化的文本框和占位符文本显示为示例值。  
  
#### <a name="to-format-a-currency-field"></a>设置货币字段格式  
  
1.  单击 **“设计”** 切换到设计视图。  
  
2.  在中单击第二行 （在列标题行） 中的单元格**SalesDate**列，然后拖动以选择包含的所有单元格`[Sum(Sales)]`。  
  
3.  在“开始”选项卡上的“数字”组中，单击“货币”按钮。 单元会更改为显示已设置好格式的货币。  
  
     如果区域设置为“英语(美国)”，则默认示例文本为 [**$12,345.00**]。 如果您看不到示例货币值，请单击**占位符样式**中**数字**组，然后依次**示例值**。  
  
4.  单击 **“运行”** 以预览报表。  
  
 汇总值**销售**以货币形式显示。  
  
##  <a name="FormatDates"></a> 6.（可选）将数据格式设置为日期格式  
 默认情况下，“SalesDate”字段同时显示日期和时间信息。 您可以设置其格式，使其只显示日期。  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>将日期字段设置为默认格式  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击包含 `[SalesDate]`的单元格。  
  
3.  在功能区中，在**主页**选项卡上，在**数量**组中，从下拉列表中，选择**日期**。  
  
     单元格会显示示例日期 **[2000/1/31]**。 如果看不到示例日期，请单击“数字”组中的“占位符样式”，然后单击“示例值”。  
  
4.  单击 **“运行”** 以预览报表。  
  
 **SalesDate**值以默认日期格式显示。  
  
##  <a name="Width"></a> 7.（可选）更改列宽  
 默认情况下，表中的每个单元格都包含一个文本框。 在呈现页面时，文本框将垂直扩展以容纳文本。 在呈现的报表中，每个行将扩展到行中呈现的最高文本框的高度。 设计图面上的行的高度不会影响已呈现报表中的行的高度。  
  
 若要减少每个行占用的垂直空间量，请扩展列宽以容纳单个行的列中的文本框的预计内容。  
  
#### <a name="to-change-the-width-of-columns"></a>更改列宽  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击表，以便在此表的上方和旁边显示列控点和行控点。  
  
     沿此表的上方和一侧显示的灰色条状物就是列控点和行控点。  
  
3.  指向列控点之间的行，使光标变为双箭头。 拖动列，调整到所需大小。 例如，展开的列**产品**，以便产品名称显示在同一行。  
  
4.  单击 **“运行”** 以预览报表。  
  
##  <a name="Title"></a> 8。（可选）添加报表标题  
 报表标题将出现在报表的顶部。 可以将报表标题置于报表表头中或置于表体顶部的文本框中（如果报表未使用表头）。 在本教程中，您将使用自动放置在表体顶部的文本框。  
  
 通过将不同的字体样式、大小和颜色应用于文本的短语和单个字符，可以进一步增强文本。 有关详细信息，请参阅[设置文本框中文本的格式（报表生成器和 SSRS）](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”。  
  
2.  键入 **Product Sales**，然后在文本框外部单击。  
  
3.  右键单击包含 Product Sales 的文本框，然后单击“文本框属性”。  
  
4.  在“文本框属性”对话框中，单击“字体”。  
  
5.  在“大小”列表中，选择“18pt”。  
  
6.  在中**颜色**列表中，选择**褐紫红色**。  
  
7.  选择“粗体”。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> 9。保存报表  
 将报表保存到报表服务器或计算机上。 如果不将报表保存到报表服务器上，则许多 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能（如报表部件和子报表）将不可用。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“最近使用的站点和服务器”**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为报表默认位置的报表文件夹的内容。  
  
4.  在“名称”中，用“Product Sales”替换默认名称。  
  
5.  单击 **“保存”**。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>将报表保存到计算机上  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  依次单击“桌面”、“我的文档”或“我的电脑”，并浏览到要保存该报表的文件夹。  
  
3.  在“名称”中，用“Product Sales”替换默认名称。  
  
4.  单击 **“保存”**。  
  
## <a name="next-steps"></a>后续步骤  
 用于创建具有迷你图的表报表的教程到此结束。 有关迷你图的详细信息，请参阅[迷你图和数据条（报表生成器和 SSRS）](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
