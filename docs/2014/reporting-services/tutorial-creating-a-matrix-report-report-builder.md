---
title: 教程：生成矩阵报表（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f87c1188b0abd1b576da63412829464368275b0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098922"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>教程：生成矩阵报表（报表生成器）
  本教程教您如何基于示例销售数据创建基本矩阵报表。 该矩阵具有嵌套行组和列组，以及相邻列组。 您将学习如何设置列的格式以及旋转文本。 下图显示与您将创建的报表类似的报表。  
  
 ![rs_CreateMatixReportTutorial](../../2014/tutorials/media/rs-creatematixreporttutorial.gif "rs_CreateMatixReportTutorial")  
  
 您在本教程中将创建的报表的增强版本可用作示例 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 报表生成器报表。 有关下载此示例报表和其他内容的详细信息，请参阅[报表生成器示例报表](https://go.microsoft.com/fwlink/?LinkId=184851)。  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将学习如何执行以下操作：  
  
1.  [新表或矩阵向导创建矩阵报表和数据集](#CreateMatrix)  
  
2.  [组织数据并选择布局和样式的新表或矩阵向导](#Groups)  
  
3.  [数据格式](#FormatData)  
  
4.  [添加相邻列组](#AdjacentGroup)  
  
5.  [更改列宽](#Width)  
  
6.  [合并矩阵单元](#MergeCells)  
  
7.  [添加报表表头和报表标题](#HeaderTitle)  
  
8.  [保存报表](#Save)  
  
### <a name="other-optional-step"></a>其他可选步骤  
  
1.  [旋转文本框 270 度](#RotateTextBox)  
  
 估计的时间才能完成本教程中：20 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="CreateMatrix"></a> 1.使用新的表或矩阵向导创建矩阵报表和数据集  
 从**Getting Started**对话框在报表生成器中，选择共享的数据源、 创建嵌入数据集，然后在矩阵中显示的数据。  
  
> [!NOTE]  
>  在本教程中，由于查询已经包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
#### <a name="to-create-a-new-matrix"></a>创建新矩阵  
  
1.  单击 **“开始”** ，依次指向 **“程序”** 、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”** 。  
  
    > [!NOTE]  
    >  此时应显示 **“入门”** 对话框。 如果没有，从报表生成器按钮，单击**新建**。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击“表或矩阵向导”  。  
  
4.  在“选择数据集”页上，单击“创建数据集”   。  
  
5.  单击“下一步”  。  
  
6.  上**选择数据源的连接**页上，选择现有数据源或浏览到报表服务器，然后选择数据源。 如果没有可用数据源，或您无权访问报表服务器，您可以改用嵌入数据源。 有关创建嵌入的数据源的详细信息，请参阅[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
7.  单击“下一步”  。  
  
8.  在“设计查询”页上，单击“编辑为文本”   。  
  
9. 复制并将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. 单击“下一步”  。  
  
##  <a name="Groups"></a> 2.组织数据并选择布局和样式的新表或矩阵向导  
 使用此向导可提供用于显示数据的起始设计。 此向导中的预览窗格可帮助您在完成矩阵设计之前展现对数据进行分组的结果。  
  
#### <a name="to-organize-data-into-groups-and-choose-a-layout-and-style"></a>将数据组织到组中并选择布局和样式  
  
1.  在“排列字段”  页上，将 Territory 从“可用字段”  拖到“行组”  中。  
  
2.  将 SalesDate 拖到“行组”  中并将其放在 Territory 下面。  
  
     “行组”  中字段的列出顺序定义组层次结构。 步骤 1 和 2 首先按地区组织字段的值，然后按照销售日期组织字段的值。  
  
3.  将 Subcategory 拖到“列组”  中。  
  
4.  将 Product 拖到**列组**然后将其放 Subcategory 下面。  
  
     在列出字段的顺序**列组**定义组层次结构。  
  
     步骤 3 和 4 首先按子类别组织字段的值，然后按照产品组织字段的值。  
  
5.  将 Sales 拖到“值”  中。  
  
     将使用汇总数值字段的默认函数 Sum 函数对 Sales 进行汇总。  
  
6.  将 Quantity 拖到“值”中  。  
  
     Quantity 使用 Sum 函数进行汇总。  
  
     步骤 5 和 6 指定要在矩阵数据单元中显示的数据。  
  
7.  单击“下一步”  。  
  
8.  在“选择布局”页的“选项”下，确认已选择“显示小计和总计”   。  
  
9. 验证是否选择了“分块式，小计下方显示”  。  
  
10. 确认选择了“展开/折叠组”  选项。  
  
11. 单击“下一步”  。  
  
12. 在选择样式页，在样式窗格中，选择**盖板**。  
  
13. 单击 **“完成”** 。  
  
     矩阵将添加到设计图面中。 “行组”窗格显示两个行组：“Territory”和“SalesDate”。 “列组”窗格显示两个列组：“Subcategory”和“Product”。 详细信息数据是由数据集查询检索的所有数据。  
  
14. 单击 **“运行”** 以预览报表。  
  
 对于在特定日期销售的每个产品，该矩阵显示产品所属于的子类别以及销售地区。  
  
##  <a name="FormatData"></a> 3.设置数据格式  
 默认情况下，Sales 字段的汇总数据显示一般数字，而 SalesDate 字段则显示日期和时间信息。 设置 Sales 字段格式以便将数字显示为货币，并且设置 SalesDate 字段格式以便只显示日期。 切换“占位符样式”，将格式化的文本框和占位符文本显示为示例值  。  
  
#### <a name="to-format-fields"></a>设置字段格式  
  
1.  单击 **“设计”** 切换到设计视图。  
  
2.  按 Ctrl 键，然后选择包含 `[Sum(Sales)]`的九个单元。  
  
3.  在“主文件夹”  选项卡上的“数字”  组中，单击“货币”  。 单元会更改为显示已设置好格式的货币。  
  
     如果区域设置为“英语(美国)”，则默认示例文本为 [ **$12,345.00**]。 如果您看不到示例货币值，请单击**占位符样式**中**数字**组，然后依次**示例值**。  
  
4.  单击包含 `[SalesDate]`的单元格。  
  
5.  在中**数量**组中，从下拉列表中，选择**日期**。  
  
     单元格会显示示例日期 **[2000/1/31]** 。 如果看不到示例日期，请单击“数字”  组中的“占位符样式”  ，然后单击“示例值”  。  
  
6.  单击 **“运行”** 以预览报表。  
  
 日期值仅显示日期，销售值显示为货币。  
  
##  <a name="AdjacentGroup"></a> 4.添加相邻列组  
 您可以在父子关系中嵌套行组和列组，或者在同级关系中保持它们相邻。  
  
 添加与 Subcategory 列组相邻的列组，复制单元以便填充这个新的列组，然后使用表达式创建列组标题的值。  
  
#### <a name="to-add-an-adjacent-column-group"></a>添加相邻列组  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  右键单击包含 `[Subcategory]` 的单元，指向“添加组”  ，然后单击“右侧相邻”  。  
  
     此时将打开 **“Tablix 组”** 对话框。  
  
3.  在“分组依据”  列表中选择 SalesDate，然后单击“确定”  。  
  
     一个新的列组将添加到 Subcategory 列组的左侧。  
  
4.  右键单击新列组中包含 `[SalesDate],` 的单元，然后单击“表达式”  。  
  
5.  将以下表达式复制到“表达式”框中。  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
     该表达式从销售日期中提取工作日名称。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)。  
  
6.  右键单击 Subcategory 列组中包含 Total 的单元，然后单击“复制”  。  
  
7.  右键单击包含在步骤 5 中创建的表达式的单元紧下方的单元，然后单击“粘贴”  。  
  
8.  按 Ctrl 键。  
  
9. 在 Subcategory 组中，单击 Sales 列标题以及标题下的三个单元，右键单击，然后单击“复制”  。  
  
10. 将这四个单元粘贴到新列组中的四个空单元中。  
  
11. 单击 **“运行”** 以预览报表。  
  
 报表包括名为 Monday 和 Tuesday 的列。 数据集仅包含针对这两天的数据。  
  
> [!NOTE]  
>  如果数据包括了其他天，则报表也将包括这些天的相应列。 每个列都具有列标题`Sales`，以及按地区的销售总额。  
  
##  <a name="Width"></a> 5.更改列宽  
 包括矩阵的报表填充以水平方式展开，并且在运行时以垂直方式展开。 如果您计划将数据导出到用于打印报表的格式（例如 Microsoft Word 或 Adobe PDF），则控制水平展开将特别重要。 如果报表跨多页水平展开，则打印报表将很难理解。 为了尽量缩小水平展开，您可以将列的大小调整为宽度仅供无需换行就可以显示数据。 您还可以重命名列，以便其标题适合显示数据所需的宽度。  
  
#### <a name="to-rename-and-resize-the-columns"></a>重命名列和调整列的大小  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  选择距左侧最远的 Quantity 列中的文本，然后键入“QTY”  。  
  
     列标题现在是 QTY。  
  
3.  对于名为 Quantity 的其他列，重复执行步骤 2。 共有两个这样的列。  
  
4.  单击矩阵，以便在此矩阵的上方和旁边显示列控点和行控点。  
  
     沿此表的上方和一侧显示的灰色条状物就是列控点和行控点。  
  
5.  为了将最远的 QTY 列向左侧调整，请指向列控点之间的线条，使光标变为双箭头。 将列向左侧拖动，直到宽度为 1/2 英寸。  
  
     1/2 英寸的列宽足以显示数量了。  
  
6.  对于名为 QTY 的其他列，重复执行步骤 5。  
  
7.  单击 **“运行”** 以预览报表。  
  
 报表中包含数量的列现在名为 QTY，并且这些列更窄了。  
  
##  <a name="MergeCells"></a> 6.合并矩阵单元  
 角区域是矩阵的左上角。 根据矩阵中行组和列组的数目，角区域中单元的数目将有所不同。 在本教程中内置的矩阵在其角区域中具有四个单元。 单元按两行和两列排列，反映行和列组层次结构的深度。 这四个单元并不用于此报表，并且您要将它们合并为一个单元。  
  
#### <a name="to-merge-matrix-cells"></a>合并矩阵单元  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击矩阵，以便在此矩阵的上方和旁边显示列控点和行控点。  
  
3.  按 Ctrl 键，然后选择四个角单元。  
  
4.  右键单击单元格，然后单击**合并单元格**。  
  
5.  右键单击角单元格，然后依次**文本框属性**。  
  
6.  单击 **“填充”** 选项卡。  
  
7.  单击 (***fx***) 按钮**填充颜色**。  
  
8.  将以下表达式复制并粘贴到“表达式”框中。  
  
    ```  
    #96a4b2  
    ```  
  
     这是用于在“石板”样式中使用的蓝灰色的 RGB 十六进制值。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 单击 **“运行”** 以预览报表。  
  
 右上角的矩阵是单个单元，具有与行组和列组单元相同的颜色。  
  
##  <a name="HeaderTitle"></a> 7.添加报表表头和报表标题  
 报表标题将出现在报表的顶部。 可以将报表标题置于报表表头中或置于表体顶部的文本框中（如果报表未使用表头）。 在本教程中，您将删除报表顶部的文本框，并向表头中添加主题。  
  
#### <a name="to-add-a-report-header-and-report-title"></a>添加报表表头和报表标题  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击包含表体顶部的文本框**单击此项可添加标题**，然后按 Delete 键。  
  
3.  上**插入**选项卡的功能区中，单击**标头**，然后单击**添加标头**。  
  
     页眉将添加到表体的顶部。  
  
4.  在“插入”  选项卡中，单击“文本框”  ，然后将某一文本框拖到报表表头内。 使文本框大约 6 英寸长、3/4 英寸高，并且将其放置于表头的左侧。  
  
5.  在文本框中，键入“Sales by Territory, Subcategory, and Day”  。  
  
6.  选择您所键入的文本，右键单击，然后单击**文本属性**。  
  
    > [!NOTE]  
    >  若要一起设置多个字符的格式，这些字符必须是连续的。  
  
7.  在中**文本属性**对话框中，单击**字体**。  
  
8.  在中**字体**列表中，选择**Times New Roman**; 在**大小**选择**24 pt**中**颜色**选择**褐紫红色**，然后在**样式**选择**斜体**。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 单击 **“运行”** 以预览报表。  
  
 报表在表头中包含一个报表标题。  
  
##  <a name="Save"></a> 8.保存报表  
 您可以将报表保存到报表服务器、SharePoint 库或本地计算机。  
  
 在本教程中，将报表保存到报表服务器。 如果您没有对报表服务器的访问权限，则可以保存到您的计算机。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”** 。  
  
2.  单击 **“最近使用的站点和服务器”** 。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为默认报表位置的报表文件夹的内容。  
  
4.  在“名称”  中，用“SalesByTerritorySubcategory”  替换默认名称。  
  
5.  单击“保存”  。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>将报表保存到计算机上  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”** 。  
  
2.  单击 **“桌面”** 、 **“我的文档”** 或 **“我的电脑”** ，然后浏览到要将报表保存到的文件夹。  
  
3.  在“名称”  中，用“SalesByTerritorySubcategory”  替换默认名称。  
  
4.  单击“保存”  。  
  
##  <a name="RotateTextBox"></a> 9.（可选）将文本框旋转 270 度  
 具有矩阵的报表在运行时可以垂直方式和水平方式展开。 通过垂直旋转文本框或者旋转 270 度，您可以节约水平空间。 呈现的报表然后将更窄，并且如果导出到 Microsoft Word 之类的格式，报表将更有可能适合打印页面。  
  
 文本框还可以将文本显示为竖排（从上到下）。 有关详细信息，请参阅[文本框（报表生成器和 SSRS）](report-design/text-boxes-report-builder-and-ssrs.md)。  
  
#### <a name="to-rotate-text-box-270-degrees"></a>旋转文本框 270 度  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击包含 `[Territory].` 的单元。  
  
3.  在属性窗格中，找到 WritingMode 属性，并在其下拉列表中选择**Rotate270**。  
  
     如果“属性”窗格未打开，请单击功能区的“视图”  选项卡，然后选择“属性”  。  
  
4.  确认 CanGrow 属性设置为`True`。  
  
5.  将 Territory 列的大小调整为 1/2 英寸宽，并且删除列标题。  
  
6.  单击 **“运行”** 以预览报表。  
  
 地区名称垂直书写，从下到上。 Territory 行组的高度由地区名称的长度决定。  
  
## <a name="next-steps"></a>后续步骤  
 有关如何创建矩阵报表的教程到此结束。 有关矩阵报表的详细信息，请参阅[表、 矩阵和列表&#40;报表生成器和 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)，[矩阵&#40;报表生成器和 SSRS&#41;](report-design/create-a-matrix-report-builder-and-ssrs.md)， [Tablix 数据区域&#40;报表生成器和 SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md)，并[Tablix 数据区域单元、 行和列&#40;报表生成器&#41;和 SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
