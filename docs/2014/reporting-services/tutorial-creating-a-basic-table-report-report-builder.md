---
title: 教程：生成基本表报表（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93213609abbc3e274cc61207d02b3828f9b90d7d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099026"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>教程：生成基本表报表（报表生成器）
  本教程教您如何基于示例销售数据创建基本表格报表。 下图显示了将创建的报表。  
  
 ![rs_CreateBasicReportTutorial](../../2014/tutorials/media/rs-createbasicreporttutorial.gif "rs_CreateBasicReportTutorial")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>你将学习的内容  
 在本教程中，您将了解如何执行下列操作：  
  
1.  [从“入门”创建新的报表](#CreateTable)  
  
    1.  [在表向导中指定数据连接](#DataConnection)  
  
    2.  [在表向导中创建查询](#Query)  
  
    3.  [在表向导中将数据组织到组中](#Groups)  
  
    4.  [在表向导中添加小计行和合计行](#Subtotals)  
  
    5.  [在表向导中选择样式](#Style)  
  
2.  [将数据格式设置为货币](#FormatCurrency)  
  
3.  [将数据格式设置为日期格式](#FormatDate)  
  
4.  [更改列宽](#Width)  
  
5.  [添加报表标题](#Title)  
  
6.  [保存报表](#Save)  
  
7.  [导出报表](#Export)  
  
 完成本教程的预计学时：20 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="1-create-a-new-report-from-getting-started"></a><a name="CreateTable"></a>1. 从入门创建新报表  
 从 "**入门**" 对话框创建表报表。 有两类模式：报表设计模式和共享数据集设计模式。 在报表设计模式中，您可以在“报表数据”窗格中指定数据，在设计图面上指定报表布局。 在共享数据集设计模式中，可以创建与他人共享的数据集查询。 在本教程中，您将使用报表设计模式。  
  
#### <a name="to-create-a-new-report"></a>创建新的报表  
  
1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。  
  
     随即将打开“入门”**** 对话框。  
  
    > [!NOTE]  
    >  如果未显示 "**入门**" 对话框，请在 "**报表生成器**" 按钮中单击 "**新建**"。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，确认已选中“表或矩阵向导”****。  
  
##  <a name="1a-specify-a-data-connection-in-the-table-wizard"></a><a name="DataConnection"></a>1a. 在表向导中指定数据连接  
 数据连接包含要连接到外部数据源（如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库）的信息。 通常会从数据源所有者处获取连接信息以及要使用的凭据类型。 若要指定数据连接，可以从报表服务器使用共享数据源或创建仅在此报表中使用的嵌入数据源。  
  
 在本教程中，您将使用嵌入数据源。 若要了解有关使用共享数据源的详细信息，请参阅[获取数据连接的备选方式（报表生成器）](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
#### <a name="to-create-an-embedded-data-source"></a>创建嵌入数据源  
  
1.  在“选择数据集”页上，选择“创建数据集”，然后单击“下一步”************。 将打开“选择数据源的连接”**** 页面。  
  
2.  单击 **“新建”**。 此时将打开 **“数据源属性”** 对话框。  
  
3.  在 "**名称**" 中，键入数据源的 "**产品销售额**"。  
  
4.  在“选择连接类型”中，确认已选择“Microsoft SQL Server”********。  
  
5.  在 "**连接字符串**" 中，键入以下文本，其中* \<servername>* 是实例的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]名称：  
  
    ```  
    Data Source=<servername>  
    ```  
  
     由于您将使用的查询会包含数据而不是从数据库检索数据，因此连接字符串不包含数据库名称。 有关详细信息，请参阅[教程先决条件&#40;报表生成器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
6.  单击 **“凭据”**。 输入访问外部数据源所需的凭据。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     返回至“选择数据源的连接”页****。  
  
8.  若要验证是否能连接到数据源，请单击“测试连接”****。  
  
     将显示消息“已成功地创建连接”。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 单击“下一步”  。  
  
##  <a name="1b-create-a-query-in-the-table-wizard"></a><a name="Query"></a>1b. 在表向导中创建查询  
 在报表中，可以使用具有预定义查询的共享数据集，也可以创建仅在报表中使用的嵌入数据集。 在本教程中，将创建一个嵌入数据集。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-create-a-query"></a>创建查询  
  
1.  在“设计查询”页中，关系查询设计器处于打开状态****。 在本教程中，您将使用基于文本的查询设计器。  
  
     单击 "**编辑为文本**"。 基于文本的查询设计器将显示查询窗格和结果窗格。  
  
2.  将以下 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询粘贴到“查询”框中****。  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
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
  
3.  在查询设计器工具栏上，单击 "**运行**（**！**）"。  
  
     该查询运行并显示 SalesDate、Subcategory、Product、Sales 和 Quantity 字段的结果集。  
  
     在结果集中，列标题基于查询中的名称。 在数据集中，列标题会成为字段名称并保存在报表中。 完成向导后，可以使用“报表数据”窗格查看数据集字段集合。  
  
4.  单击“下一步”  。  
  
##  <a name="1c-organize-data-into-groups-in-the-table-wizard"></a><a name="Groups"></a>1c. 在表向导中将数据组织到组中  
 在选择要进行分组的字段时，可以设计一个表格，其中的行和列显示了详细数据和聚合数据。  
  
#### <a name="to-organize-data-into-groups"></a>将数据组织到组中  
  
1.  在“排列字段”页上，将 Product 拖到“值”中********。  
  
2.  将 Quantity 拖到“值”中并将其置于 Product 下方****。  
  
     Quantity 由 Sum 函数（即数值字段的默认聚合函数）自动聚合。 值为 [Sum(Quantity)]。  
  
     可以打开下拉列表以查看其他可用聚合函数。 不要更改聚合函数。  
  
3.  将 Sales 拖到“值”中并将其置于 [Sum(Quantity)] 下方****。  
  
     Sales 由 Sum 函数聚合。 值为 [Sum(Sales)]。  
  
     步骤 1、2 和 3 指定要在表中显示的数据。  
  
4.  将 SalesDate 拖到“行组”**** 中。  
  
5.  将 Subcategory 拖到“行组”中并将其置于 SalesDate 下方****。  
  
     步骤 4 和 5 首先按日期组织字段的值，然后按照该日期的产品子类别组织字段的值。  
  
6.  单击“下一步”  。  
  
##  <a name="1d-add-subtotal-and-total-rows-in-the-table-wizard"></a><a name="Subtotals"></a>1d. 在表向导中添加小计行和合计行  
 创建组后，可以添加用于显示字段的聚合值的行并设置其格式。 可以选择是显示所有数据还是允许用户以交互方式展开和折叠已分组数据。  
  
#### <a name="to-add-subtotals-and-totals"></a>添加小计和总计  
  
1.  在“选择布局”页的“选项”下，确认已选择“显示小计和总计”************。  
  
2.  验证是否选择了“分块式，小计下方显示”****。  
  
     向导的“预览”窗格将显示包含有五行的表。 当您运行报表时，每行将按以下方式显示：  
  
    1.  第一行将对表重复一次以显示列标题。  
  
    2.  第二行将对销售订单中的每个行项重复一次并显示产品名称、订单数量和行总计。  
  
    3.  第三行将对每个销售订单重复一次以显示每个订单的小计。  
  
    4.  第四行将对每个订单日期重复一次以显示每天的小计。  
  
    5.  第五行将对表重复一次以显示总计。  
  
3.  清除“展开/折叠组”选项****。 在本教程中，创建的报表不会使用明细功能（用户可通过此功能来展开父组层次结构）来显示子组行和详细信息行。  
  
4.  单击“下一步”  。  
  
##  <a name="1e-choose-a-style-in-the-table-wizard"></a><a name="Style"></a>1e. 在表向导中选择样式  
 样式指定字形、颜色集和边框样式。  
  
#### <a name="to-specify-a-table-style"></a>指定表样式  
  
1.  在 "**选择样式**" 页的 "样式" 窗格中，选择 "海运"。  
  
     “预览”窗格将显示具有该样式的表的示例。  
  
2.  （可选）单击其他样式以查看应用了样式的示例。  
  
3.  单击“完成”  。  
  
 表将添加到设计图面中。 该表有 5 列、5 行。 “行组”窗格显示三个行组：SalesDate、Subcategory 和 Details。 详细信息数据是由数据集查询检索的所有数据。  
  
##  <a name="2-format-data-as-currency"></a><a name="FormatCurrency"></a>2. 将数据格式设置为货币  
 默认情况下，Sales 字段的汇总数据将显示总数。 请设置其格式，以使其显示货币形式的数字。 切换“占位符样式”，将格式化的文本框和占位符文本显示为示例值****。  
  
#### <a name="to-format-a-currency-field"></a>设置货币字段格式  
  
1.  单击 "**设计**" 切换到 "设计" 视图。  
  
2.  单击第二行（位于列标题行下）Sales 列的单元，然后向下拖动以选定包含 `[Sum(Sales)]`的所有单元。  
  
3.  在“开始”选项卡上的“数字”组中，单击“货币”按钮************。 单元会更改为显示已设置好格式的货币。  
  
     如果区域设置为“英语(美国)”，则默认示例文本为 [**$12,345.00**]。 如果看不到示例货币值，请在 "**数字**" 组中单击 "**占位符样式**"，然后单击 "**示例值**"。  
  
4.  单击 **“运行”** 以预览报表。  
  
 Sales 的汇总值会以货币形式显示。  
  
##  <a name="3-format-data-as-date"></a><a name="FormatDate"></a>3. 将数据格式设置为日期  
 默认情况下，SalesDate 字段会同时显示日期和时间信息。 您可以设置其格式，使其只显示日期。  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>将日期字段设置为默认格式  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击包含 `[SalesDate]`的单元格。  
  
3.  在功能区上，在 "**主页**" 选项卡上的 "**数字**" 组中，从下拉列表中选择 "**日期**"。  
  
     单元格将显示示例日期 **[1/31/2000]**。 如果看不到示例日期，请单击“数字”**** 组中的“占位符样式”****，然后单击“示例值”****。  
  
4.  单击 **“运行”** 以预览报表。  
  
 SalesDate 值将以默认日期格式显示。  
  
#### <a name="to-change-the-date-format-to-a-custom-format"></a>将日期格式更改为自定义格式  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击包含 `[SalesDate]`的单元格。  
  
3.  在 "**主页**" 选项卡上的 "**数字**" 组中，单击对话框启动器。  
  
     启动器是该组右侧角中的小箭头。 将打开“文本框属性”对话框****。  
  
4.  在“类别”窗格中，确认已选中“日期”****。  
  
5.  在“类型”窗格中，选择“2000 年 1 月 31 日”********。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     单元会显示示例日期 **[2000 年 1 月 31 日]**。  
  
7.  单击 **“运行”** 以预览报表。  
  
 SalesDate 值将显示月份名而非月份数字。  
  
##  <a name="4-change-column-widths"></a><a name="Width"></a>4. 更改列宽  
 默认情况下，表中的每个单元格都包含一个文本框。 在呈现页面时，文本框将垂直扩展以容纳文本。 在呈现的报表中，每个行将扩展到行中呈现的最高文本框的高度。 设计图面上的行的高度不会影响已呈现报表中的行的高度。  
  
 若要减少每个行占用的垂直空间量，请扩展列宽以容纳单个行的列中的文本框的预计内容。  
  
#### <a name="to-change-the-width-of-table-columns"></a>更改表的列宽  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击表，以便在此表的上方和旁边显示列控点和行控点。  
  
     沿此表的上方和一侧显示的灰色条状物就是列控点和行控点。  
  
3.  指向列控点之间的行，使光标变为双箭头。 拖动列，调整到所需大小。 例如，展开 Product 列，以便产品名称显示在一行中。  
  
4.  单击 **“运行”** 以预览报表。  
  
##  <a name="5-add-a-report-title"></a><a name="Title"></a>5. 添加报表标题  
 报表标题将出现在报表的顶部。 可以将报表标题置于报表表头中或置于表体顶部的文本框中（如果报表未使用表头）。 在本教程中，您将使用自动放置在表体顶部的文本框。  
  
 通过将不同的字体样式、大小和颜色应用于文本的短语和单个字符，可以进一步增强文本。 有关详细信息，请参阅[设置文本框中文本的格式（报表生成器和 SSRS）](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)。  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”****。  
  
2.  键入 **Product Sales**，然后在文本框外部单击。  
  
3.  右键单击包含 Product Sales 的文本框，然后单击“文本框属性”********。  
  
4.  在“文本框属性”**** 对话框中，单击“字体”****。  
  
5.  在“大小”**** 列表中，选择“18pt”****。  
  
6.  在“颜色”列表中，选择“青蓝色”********。  
  
7.  选择“粗体”****。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="6-save-the-report"></a><a name="Save"></a>6. 保存报表  
 将报表保存到报表服务器或计算机上。 如果不将报表保存到报表服务器上，则许多 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能（如报表部件和子报表）将不可用。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“最近使用的站点和服务器”**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为报表默认位置的报表文件夹的内容。  
  
4.  在“名称”中，用“Product Sales”替换默认名称********。  
  
5.  单击“保存”  。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>将报表保存到计算机上  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  依次单击“桌面”、“我的文档”或“我的电脑”，并浏览到要保存该报表的文件夹************。  
  
3.  在“名称”中，用“Product Sales”替换默认名称********。  
  
4.  单击“保存”  。  
  
##  <a name="7-export-the-report"></a><a name="Export"></a>7. 导出报表  
 可以将报表导出为不同的格式，如 Microsoft Excel 和以逗号分隔的值 (CSV)。 有关详细信息，请参阅[导出报表 &#40;报表生成器和 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)。  
  
 在本教程中，您将报表导出为 Excel 格式，并设置报表的属性以便为工作簿选项卡提供自定义名称。  
  
#### <a name="to-specify-the-workbook-tab-name"></a>指定工作簿选项卡名称  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击该报表的外部。  
  
3.  .在 "属性" 窗格中，找到 "InitialPageName" 属性并键入**Product Sales Excel**。  
  
    > [!NOTE]  
    >  如果 "属性" 窗格不可见，请单击功能区上的 "视图" 选项卡，然后单击 "**属性**"。  
  
#### <a name="to-export-a-report-to-excel"></a>将报表导出为 Excel 格式  
  
1.  单击 **“运行”** 以预览报表。  
  
2.  .在功能区上，单击 "**导出**"，然后单击 " **Excel**"。  
  
     此时会打开“另存为”**** 对话框。  
  
3.  浏览到 "**文档**" 文件夹。  
  
4.  在 "**文件名**" 文本框中，键入**Product Sales Excel**。  
  
5.  确认文件类型为 " **Excel 工作簿**"。  
  
6.  单击“保存”  。  
  
#### <a name="to-view-the-report-in-excel"></a>在 Excel 中查看报表  
  
1.  打开 "**文档**" 文件夹，然后双击 " **Product Sales**"。  
  
2.  验证工作簿选项卡的名称是否为 **Product Sales Excel**。  
  
## <a name="next-steps"></a>后续步骤  
 到此为止，我们结束了有关如何创建基本表格报表的演练。 有关表的详细信息，请参阅[表、矩阵和列表（报表生成器和 SSRS）](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [教程 &#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
