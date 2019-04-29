---
title: 教程：创建钻取和主报表 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7168c8d3-cef5-4c4a-a0bf-fff1ac5b8b71
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1177dfb7260959940eb89a31dde740e290ab73f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650622"
---
# <a name="tutorial-creating-drillthrough-and-main-reports-report-builder"></a>教程：创建钻取和主报表 （报表生成器）
  本教程讲解如何创建两种类型的报表： 钻取报表和主报表。 这些报表中使用的示例销售数据的 Analysis Services 多维数据集检索。 下图显示了将创建的报表。  
  
 ![rs_DrillthroughCubeTutorial](../../2014/tutorials/media/rs-drillthroughcubetutorial.gif "rs_DrillthroughCubeTutorial")  
  
 下图显示了如何在字段中的值，游戏和玩具，钻取报表的标题中显示的主报表。 在钻取的数据与游戏和玩具产品类别。  
  
 ![rs_DrillthroughCubeTutorialParmExpr](../../2014/tutorials/media/rs-drillthroughcubetutorialparmexpr.gif "rs_DrillthroughCubeTutorialParmExpr")  
  
## <a name="what-you-will-learn"></a>学习内容  
 **钻取报表中您将学习如何：**  
  
1.  [从表或矩阵向导创建钻取矩阵报表和数据集](#DMatrixAndDataset)  
  
    1.  [指定数据连接](#DConnection)  
  
    2.  [创建 MDX 查询](#DMDXQuery)  
  
    3.  [按组样式组织数据](#DLayout)  
  
    4.  [添加小计和总计](#DTotals)  
  
    5.  [选择样式](#DStyle)  
  
2.  [数据格式设置为货币](#DFormat)  
  
3.  [将列添加到在迷你图中显示销售值](#DSparkline)  
  
4.  [添加包含产品类别名称的报表标题](#DReportTitle)  
  
5.  [更新参数属性](#DParameter)  
  
6.  [将报表保存到 SharePoint 库](#DSave)  
  
 **在主报表中您将学习如何：**  
  
1.  [从表或矩阵向导创建主矩阵报表和数据集](#MMatrixAndDataset)  
  
    1.  [指定数据连接](#MConnection)  
  
    2.  [创建 MDX 查询](#MMDXQuery)  
  
    3.  [将数据组织到组](#MLayout)  
  
    4.  [添加小计和总计](#MTotals)  
  
    5.  [选择样式](#MStyle)  
  
2.  [删除总计行](#MGrandTotal)  
  
3.  [配置用于钻取的文本框操作](#MDrillthrough)  
  
4.  [使用指示器替换数值](#MIndicators)  
  
5.  [更新参数属性](#MParameter)  
  
6.  [添加报表标题](#MTitle)  
  
7.  [将报表保存到 SharePoint 库](#MSave)  
  
8.  [运行主报表和钻取报表](#MRunReports)  
  
 估计的时间才能完成本教程中：30 分钟。  
  
## <a name="requirements"></a>要求  
 本教程需要访问 Contoso Sales 多维数据集。 此要求适用于钻取和主报表。 有关要求的详细信息，请参阅[教程的先决条件&#40;报表生成器&#41;](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="DMatrixAndDataset"></a> 1.从表或矩阵向导创建钻取报表  
 从入门对话框中，通过创建矩阵报表**表或矩阵向导**。 在向导中提供了两种模式： 报表设计和共享数据集设计。 在本教程中，将使用报表设计模式。  
  
#### <a name="to-create-a-new-report"></a>若要创建新的报表  
  
1.  单击**启动**，依次指向**程序**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**报表生成器**，然后单击**报表生成器**。  
  
     **Getting Started**对话框随即打开。 如果未显示，从**报表生成器**按钮，再单击**新建**。  
  
2.  在左窗格中，确认**新的报表**处于选中状态。  
  
3.  在右窗格中，确认**表或矩阵向导**处于选中状态。  
  
##  <a name="DConnection"></a> 1a. 指定数据连接  
 数据连接包含连接到外部数据源，如 Analysis Services 多维数据集所需的信息或[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库。 若要指定数据连接，可以使用来自报表服务器的共享的数据源或创建仅在此报表中使用的嵌入的数据源。 在本教程中，将使用嵌入的数据源。 若要了解有关使用共享的数据源的详细信息，请参阅[获取数据连接的备选方式&#40;报表生成器&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
#### <a name="to-create-an-embedded-data-source"></a>若要创建嵌入的数据源  
  
1.  上**选择数据集**页上，选择**创建数据集**，然后单击**下一步**。 **选择数据源的连接**页随即打开。  
  
2.  单击“新建” 。 **数据源属性**对话框随即打开。  
  
3.  在中**名称**，类型**Online and Reseller Sales Detail**作为数据源的名称。  
  
4.  在中**选择连接类型**，选择**Microsoft SQL Server Analysis Services**，然后单击**生成**。  
  
5.  在中**数据源**，验证数据源是否**Microsoft SQL Server Analysis Services (AdomdClient)**。  
  
6.  在中**服务器名称**，键入安装 Analysis Services 实例的服务器的名称。  
  
7.  在中**选择或输入数据库名称**，选择 Contoso 多维数据集。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 确认**连接字符串**包含以下语法：  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
     `<servername>`的实例的名称[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安装 Analysis services。  
  
10. 单击**凭据类型**。  
  
    > [!NOTE]  
    >  具体取决于如何在数据源上配置权限，可能需要更改默认身份验证选项。 有关详细信息，请参阅[安全性&#40;报表生成器&#41;](report-builder/security-report-builder.md)。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     **选择数据源的连接**页将出现。  
  
12. 若要验证是否可以连接到数据源，请单击**测试连接**。  
  
     消息**成功创建连接**出现。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. 单击 **“下一步”**。  
  
##  <a name="DMDXQuery"></a> 1b. 创建 MDX 查询  
 在报表中，可以使用共享数据集具有预定义的查询，或可以在报表中仅创建使用嵌入数据集。 在本教程中，您将创建嵌入数据集。  
  
#### <a name="to-create-query-filters"></a>若要创建查询筛选器  
  
1.  上**设计查询**页上，在元数据窗格中，单击该按钮 **（...）**.  
  
2.  在中**选择多维数据集**对话框中，单击销售，然后单击**确定**。  
  
    > [!TIP]  
    >  如果不想手动生成 MDX 查询，请单击![切换到设计模式](../analysis-services/media/rsqdicon-designmode.gif "切换到设计模式")图标，切换到查询模式的查询设计器中，粘贴到查询设计器中，已完成的 MDX 和然后继续执行中的步骤 6[创建数据集](#DSkip)。  
  
    ```  
    SELECT NON EMPTY { [Measures].[Sales Amount], [Measures].[Sales Return Amount] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS * [Product].[Product Subcategory Name].[Product Subcategory Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
    ```  
  
3.  在度量值组窗格中，展开 Channel，，然后将拖到通道名称**层次结构**筛选器窗格中的列。  
  
     维度名称 Channel 会自动添加到**维度**列。 不会更改**维度**或**运算符**列。  
  
4.  若要打开**筛选器表达式**列表中，单击中的向下箭头**筛选器表达式**列。  
  
5.  在筛选表达式列表中，展开**所有渠道**，单击**联机**，单击**分销商**，然后单击**确定**。  
  
     查询现在包含一个筛选器以只包括这些渠道：在线和分销商。  
  
6.  展开 Sales Territory 维度，然后将拖到 Sales Territory Group**层次结构**列 (下面**通道名称**)。  
  
7.  打开**筛选器表达式**列表中，展开**所有销售区域**，单击**北美**，然后单击**确定**。  
  
     查询现在具有一个筛选器以在北美包括仅销售。  
  
8.  在度量值组窗格中，展开 Date，，再将日历年到**层次结构**筛选器窗格中的列。  
  
     维度名称 Date 会自动添加到**维度**列。 不会更改**维度**或**运算符**列。  
  
9. 若要打开**筛选器表达式**列表中，单击中的向下箭头**筛选器表达式**列。  
  
10. 在筛选表达式列表中，展开**所有日期**，单击**2009 年度**，然后单击**确定**。  
  
     查询现在包含一个筛选器以包括仅日历 2009 年。  
  
#### <a name="to-create-the-parameter"></a>若要创建参数  
  
1.  展开 Product 维度，然后将拖到 Product Category Name 成员**层次结构**列下面**日历年**。  
  
2.  打开**筛选器表达式**列表中，单击**的所有产品**，然后单击**确定**。  
  
3.  单击**参数**复选框。 查询现在包含参数 ProductProductCategoryName。  
  
    > [!NOTE]  
    >  参数包含产品类别名称。 当您单击主报表中的产品类别名称时，其名称是通过使用此参数传递给钻取报表。  
  
###  <a name="DSkip"></a> 若要创建数据集  
  
1.  从 Channel 维度将 Channel Name 拖到数据窗格。  
  
2.  从产品维度中，将 Product Category Name 拖到数据窗格，然后将它放到通道名称的右侧。  
  
3.  从产品维度中，将 Product Subcategory Name 拖到数据窗格，然后将它放到产品类别名称的右侧。  
  
4.  在元数据窗格中，展开**度量值**，然后展开 Sales。  
  
5.  将 Sales Amount 度量值拖到数据窗格，然后将它放到 Product Subcategory Name 的右侧。  
  
6.  在查询设计器工具栏中，单击**运行 （！）**.  
  
7.  单击 **“下一步”**。  
  
##  <a name="DLayout"></a> 1c. 将数据组织到组  
 当选中对数据进行分组所依据的字段时，您可以设计显示详细信息和聚合的数据的矩阵具有行和列。  
  
#### <a name="to-organize-data-into-groups"></a>若要将数据组织到组  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  上**排列字段**页上，将为 Product_Subcategory_Name**行组**。  
  
    > [!NOTE]  
    >  在名称中的空格替换为下划线 (_)。 例如，Product Category Name 为 product_category_name。  
  
3.  将 channel_name 拖到**列组**。  
  
4.  拖动到 Sales_Amount**值**。  
  
     Sales_Amount 自动由 Sum 函数聚合数值字段的默认聚合。 该值为 `[Sum(Sales_Amount)]`。  
  
     若要查看其他可用聚合函数，请打开下拉列表 （不要更改聚合函数）。  
  
5.  拖动到 Sales_Return_Amount**值**，然后将它放下面`[Sum(Sales_Amount)]`。  
  
     步骤 4 和 5 指定要在矩阵中显示的数据。  
  
6.  单击 **“下一步”**。  
  
##  <a name="DTotals"></a> 1d. 添加小计和总计  
 创建组后，可以添加和设置字段的聚合值将显示的行的格式。 此外可以选择是显示所有数据还是允许用户展开和折叠已分组数据以交互方式。  
  
#### <a name="to-add-subtotals-and-totals"></a>若要添加小计和总计  
  
1.  上**选择布局**页面上，在**选项**，验证**显示小计和总计**处于选中状态。  
  
     向导预览窗格将显示一个矩阵，其中四个行。  
  
2.  单击 **“下一步”**。  
  
##  <a name="DStyle"></a> 1e。 选择样式  
 样式指定字体样式、 一组颜色和边框样式。  
  
#### <a name="to-specify-a-style"></a>指定样式  
  
1.  上**选择一种样式**页上，在样式窗格中，选择静态图像。  
  
2.  单击 **“完成”**。  
  
     表添加到设计图面。  
  
3.  若要预览报表，请单击**运行 （！）**.  
  
##  <a name="DFormat"></a> 2.数据格式设置为货币  
 应用货币格式到钻取报表中的销售额字段。  
  
#### <a name="to-format-data-as-currency"></a>若要设置数据的格式为货币  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  若要选择和一次设置多个单元格的格式，请按住 Ctrl 键，并选择包含数值销售数据的单元格。  
  
3.  上**主页**选项卡上，在**数量**组中，单击**货币**。  
  
##  <a name="DSparkline"></a> 3.添加要在迷你图中显示销售值的列  
 而不是显示为货币值的销售额和销售退货，报表在迷你图中显示的值。  
  
#### <a name="to-add-sparklines-to-columns"></a>将迷你图添加到列  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  在矩阵的总计组中，右键单击**Sales Amount**列中，单击**插入列**，然后单击**右**。  
  
     一个空列添加到右侧**Sales Amount**。  
  
3.  在功能区中，单击**矩形**，然后单击右侧的空单元格`[Sum(Sales_Amount)]`[Product_Subcategory] 行组中的单元格。  
  
4.  在功能区中，单击**迷你图**图标，然后单击添加了矩形的单元格。  
  
5.  在中**选择迷你图类型**对话框框中，确保**列**选择类型。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  右键单击迷你图。  
  
8.  在图表数据窗格中，单击**添加字段**图标，然后单击 Sales_Amount。  
  
9. 右键单击`Sales_Return_Amount`列，然后将列添加到它的右侧。  
  
10. 重复步骤 2 到 6。  
  
11. 右键单击迷你图。  
  
12. 在图表数据窗格中，单击**添加字段**图标，然后单击 Sales_Return_Amount。  
  
13. 若要预览报表，请单击**运行**。  
  
##  <a name="DReportTitle"></a> 4.添加包含产品类别名称的报表标题  
 报表标题显示在报表的顶部。 可以将报表标题置于报表表头或，如果报表不使用其中一个，在表体顶部的文本框中。 在本教程中，将使用自动放置在表体顶部的文本框。  
  
#### <a name="to-add-a-report-title"></a>若要添加报表标题  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  在设计图面上，单击**单击此项可添加标题**。  
  
3.  类型**Sales and Returns for Category:**。  
  
4.  右键单击，然后依次**创建占位符**。  
  
5.  单击 **(fx)** 右侧的按钮**值**列表。  
  
6.  在中**表达式**对话框中，在类别窗格中，单击**数据集**，然后在**值**列表中双击`First(Product_Category_Name)`。  
  
     **表达式**框包含以下表达式：  
  
    ```  
    =First(Fields!Product_Category_Name.Value, "DataSet1")  
    ```  
  
7.  若要预览报表，请单击**运行**。  
  
 报表标题中包含第一个产品类别的名称。 更高版本，此报表作为钻取报表运行后，产品类别名称将动态更改以反映被单击主报表中的产品类别的名称。  
  
##  <a name="DParameter"></a> 5.更新参数属性  
 默认情况下参数是可见的不适合于此报表。 将更新钻取报表的参数属性。  
  
#### <a name="to-hide-a-parameter"></a>若要隐藏参数  
  
1.  在报表数据窗格中，展开**参数**。  
  
2.  右键单击\@ProductProductCategoryName，然后单击**参数属性**。  
  
    > [!NOTE]  
    >  \@名称旁边的字符指示这是一个参数。  
  
3.  上**常规**选项卡上，单击**Hidden**。  
  
4.  在中**Prompt**框中，键入**Product Category**。  
  
    > [!NOTE]  
    >  因为参数隐藏的永远不会使用此提示。  
  
5.  （可选） 单击**可用值**并**默认值**和查看它们的选项。 不要更改这些选项卡上的任何选项。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="DSave"></a> 6.将报表保存到 SharePoint 库  
 可以将报表保存到 SharePoint 库、 报表服务器或您的计算机。 如果将报表保存到您的计算机，许多[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]功能，如报表部件和子报表不可用。 在本教程中，将报表保存到 SharePoint 库。  
  
#### <a name="to-save-the-report"></a>若要保存报表  
  
1.  从报表生成器按钮，单击**保存**。 **另存为报表**对话框随即打开。  
  
    > [!NOTE]  
    >  如果您正在重新保存报表，它是自动将其重新保存到以前的位置。 若要更改位置，请使用**另存为**选项。  
  
2.  若要显示最近使用的报表服务器和 SharePoint 站点的列表，请单击**最近使用的站点和服务器**。  
  
3.  选择或键入必须保存报表权限的 SharePoint 站点的名称。  
  
     SharePoint 库的 URL 具有以下语法：  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
4.  单击“保存” 。  
  
     **最近的站点和服务器**列出 SharePoint 站点上的库。  
  
5.  导航到用于保存报表的库。  
  
6.  在中**名称**框中，替换默认名称，并且**ResellerVSOnlineDrillthrough**。  
  
    > [!NOTE]  
    >  会将主报表保存到相同的位置。 如果你想要保存主报表和钻取报表到不同的站点或库，则必须更新的路径**转到报表**主报表中的操作。  
  
7.  单击“保存” 。  
  
##  <a name="MMatrixAndDataset"></a> 1.从表或矩阵向导创建新的报表  
 从**Getting Started**对话框框中，使用创建矩阵报表**表或矩阵向导**。  
  
#### <a name="to-create-a-new-report"></a>若要创建新的报表  
  
1.  单击**启动**，依次指向**程序**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**报表生成器**，然后单击**报表生成器**。  
  
2.  在中**Getting Started**对话框框中，确保**新报表**已选择，然后单击**表或矩阵向导**。  
  
##  <a name="MConnection"></a> 1a. 指定数据连接  
 您将添加到主报表的嵌入的数据源。  
  
#### <a name="to-create-an-embedded-data-source"></a>若要创建嵌入的数据源  
  
1.  上**选择数据集**页上，选择**创建数据集**，然后单击**下一步**。  
  
2.  单击“新建” 。  
  
3.  在中**名称**，类型**Online and Reseller Sales Main**作为数据源的名称。  
  
4.  在中**选择连接类型**，选择**Microsoft SQL Server Analysis Services**，然后单击**生成**。  
  
5.  在中**数据源**，验证数据源是否**Microsoft SQL Server Analysis Services (AdomdClient)**。  
  
6.  在中**服务器名称**，键入服务器的名称，其中的一个实例[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]安装。  
  
7.  在中**选择或输入数据库名称**，选择 Contoso 多维数据集。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 确认**连接字符串**包含以下语法：  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
10. 单击**凭据类型**。  
  
     具体取决于如何在数据源上配置权限，可能需要更改默认的身份验证。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 若要验证是否可以连接到数据源，请单击**测试连接**。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. 单击 **“下一步”**。  
  
##  <a name="MMDXQuery"></a> 1b. 创建 MDX 查询  
 接下来，创建嵌入数据集。 若要执行此操作，将使用查询设计器来创建筛选器、 参数和计算的成员以及数据集本身。  
  
#### <a name="to-create-query-filters"></a>若要创建查询筛选器  
  
1.  上**设计查询**页上，在元数据窗格中，在多维数据集部分中，单击省略号 **（...）**.  
  
2.  在中**选择多维数据集**对话框中，单击销售，然后单击**确定**。  
  
    > [!TIP]  
    >  如果不想手动生成 MDX 查询，请单击![切换到设计模式](../analysis-services/media/rsqdicon-designmode.gif "切换到设计模式")图标，切换到查询模式的查询设计器中，粘贴到查询设计器中，已完成的 MDX 和然后继续执行步骤 5 中[创建数据集](#MSkip)。  
  
    ```  
    WITH MEMBER [Measures].[Net QTY] AS [Measures].[Sales Quantity] -[Measures].[Sales Return Quantity] MEMBER [Measures].[Net Sales] AS [Measures].[Sales Amount] - [Measures].[Sales Return Amount] SELECT NON EMPTY { [Measures].[Net QTY], [Measures].[Net Sales] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGSQuery text: Code.  
    ```  
  
3.  在度量值组窗格中，展开 Channel，，然后将拖到通道名称**层次结构**筛选器窗格中的列。  
  
     维度名称 Channel 会自动添加到**维度**列。 不会更改**维度**或**运算符**列。  
  
4.  若要打开**筛选器表达式**列表中，单击中的向下箭头**筛选器表达式**列。  
  
5.  在筛选表达式列表中，展开**所有渠道**，单击**联机**并**分销商**，然后单击**确定**。  
  
     查询现在包含一个筛选器以只包括这些渠道：在线和分销商。  
  
6.  展开 Sales Territory 维度，然后将拖到 Sales Territory Group**层次结构**列下面**通道名称**。  
  
7.  打开**筛选器表达式**列表中，展开**所有销售区域**，单击**北美**，然后单击**确定**。  
  
     查询现在具有一个筛选器以在北美包括仅销售。  
  
8.  在度量值组窗格中，展开 Date，并拖动到日历年**层次结构**筛选器窗格中的列。  
  
     维度名称 Date 会自动添加到**维度**列。 不会更改**维度**或**运算符**列。  
  
9. 若要打开**筛选器表达式**列表中，单击中的向下箭头**筛选器表达式**列。  
  
10. 在筛选表达式列表中，展开**所有日期**，单击**2009 年度**，然后单击**确定**。  
  
     查询现在包含一个筛选器以包括仅日历 2009 年。  
  
#### <a name="to-create-the-parameter"></a>若要创建参数  
  
1.  展开 Product 维度，然后将拖到 Product Category Name 成员**层次结构**列下面**Sales Territory Group**。  
  
2.  打开**筛选器表达式**列表中，单击**的所有产品**，然后单击**确定**。  
  
3.  单击**参数**复选框。 查询现在包含参数 ProductProductCategoryName。  
  
#### <a name="to-create-calculated-members"></a>若要创建计算的成员  
  
1.  将光标置于计算成员窗格，右键单击，再单击**新建计算成员**。  
  
2.  在元数据窗格中，展开**度量值**，然后展开 Sales。  
  
3.  将为 Sales Quantity 度量值拖**表达式**框中，键入减号字符 （-），然后将拖到 Sales Return Quantity 度量值**表达式**框; 将它放在该减法运算字符。  
  
     下面的代码显示了该表达式：  
  
    ```  
    [Measures].[Sales Quantity] - [Measures].[Sales Return Quantity]  
    ```  
  
4.  在名称框中，键入**Net QTY**，然后单击**确定**。  
  
     计算成员窗格列出**Net QTY**计算的成员。  
  
5.  右键单击**计算成员**，然后单击**新建计算成员**。  
  
6.  在元数据窗格中，展开**度量值**，然后展开 Sales。  
  
7.  将为 Sales Amount 度量值拖**表达式**框中，键入减号字符 （-），然后将拖到 Sales Return Amount 度量值**表达式**框; 将它放到减号字符后面。  
  
     下面的代码显示了该表达式：  
  
    ```  
    [Measures].[Sales Amount] - [Measures].[Sales Return Amount]  
    ```  
  
8.  在中**名称**框中，键入**净销售额**，然后单击**确定**。计算成员窗格列出**净销售额**计算的成员。  
  
###  <a name="MSkip"></a> 若要创建数据集  
  
1.  从 Channel 维度将 Channel Name 拖到数据窗格。  
  
2.  从产品维度中，将 Product Category Name 拖到数据窗格，然后将它放到通道名称的右侧。  
  
3.  从**计算成员**，拖动`Net QTY`到数据窗格中，然后将它放到产品类别名称的右侧。  
  
4.  从计算成员，将 Net Sales 拖到数据窗格，然后将它放到右侧`Net QTY`。  
  
5.  在查询设计器工具栏中，单击**运行 （！）**.  
  
     查看查询结果集。  
  
6.  单击 **“下一步”**。  
  
##  <a name="MLayout"></a> 1c. 将数据组织到组  
 当选中对数据进行分组所依据的字段时，您可以设计显示详细信息和聚合的数据的矩阵具有行和列。  
  
#### <a name="to-organize-data-into-groups"></a>若要将数据组织到组  
  
1.  上**排列字段**页上，将为 Product_Category_Name**行组**。  
  
2.  将 channel_name 拖到**列组**。  
  
3.  拖动`Net_QTY`到**值**。  
  
     `Net_QTY` 由 Sum 函数聚合数值字段的默认自动聚合。 该值为 `[Sum(Net_QTY)]`。  
  
     若要查看其他可用聚合函数，请打开下拉列表。 不要更改聚合函数。  
  
4.  拖动`Net_Sales_Return`到**值**，然后进行以下`[Sum(Net_QTY)]`。  
  
     步骤 3 和 4 指定要在矩阵中显示的数据。  
  
##  <a name="MTotals"></a> 1d. 添加小计和总计  
 可以在报表中显示小计和总计。 在主报表中的数据将显示为指示器;完成向导后，将删除总计。  
  
#### <a name="to-add-subtotals-and-grand-totals"></a>若要添加小计和总计  
  
1.  上**选择布局**页面上，在**选项**，验证**显示小计和总计**处于选中状态。  
  
     向导预览窗格将显示一个矩阵，其中四个行。  当您运行报表时，每一行将显示如下所示：第一行是列组，第二行包含列标题，第三行包含产品类别数据 (`[Sum(Net_ QTY)]`和`[Sum(Net_Sales)]`，和第四个行包含总计。  
  
2.  单击 **“下一步”**。  
  
##  <a name="MStyle"></a> 1e。 选择样式  
 将石板样式应用于报表。 这是钻取报表使用的同一个样式。  
  
#### <a name="to-specify-a-style"></a>指定样式  
  
1.  上**选择一种样式**页上，在样式窗格中，选择静态图像。  
  
2.  单击 **“完成”**。  
  
3.  若要预览报表，请单击**运行**。  
  
##  <a name="MGrandTotal"></a> 2.删除总计行  
 数据值显示为指示器状态，包括列组总计。 删除显示总计的行。  
  
#### <a name="to-remove-the-grand-total-row"></a>若要删除总计行  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  单击总计行 （矩阵中的最后一行），右键单击，然后单击**删除行**。  
  
3.  若要预览报表，请单击**运行**。  
  
##  <a name="MDrillthrough"></a> 3.配置用于钻取的文本框操作  
 若要启用钻取，请在主报表中的文本框上指定的操作。  
  
#### <a name="to-enable-an-action"></a>若要启用操作  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  右键单击包含 Product_Category_Name 的单元格，然后单击**文本框属性**。  
  
3.  单击**操作**选项卡。  
  
4.  选择**转到报表。**  
  
5.  在中**指定报表**，单击**浏览**，然后找到名为 ResellerVSOnlineDrillthrough 的钻取报表。  
  
6.  若要添加参数以运行钻取报表，请单击**添加**。  
  
7.  在中**名称**列表中，选择 ProductProductCategoryName。  
  
8.  在中**值**，类型`[Product_Category_Name.UniqueName]`。  
  
     Product_category_name 是在数据集中的字段。  
  
    > [!IMPORTANT]  
    >  必须包括`UniqueName`属性因为钻取操作需要唯一值。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-format-the-drillthrough-field"></a>若要设置钻取字段的格式  
  
1.  右键单击包含的单元格`Product_Category_Name`，然后单击**文本框属性**。  
  
2.  单击**字体**选项卡。  
  
3.  在中**效果**列表中，选择**用下划线标出**。  
  
4.  在中**颜色**列表中，选择**蓝色**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  若要预览报表，请单击**运行**。  
  
 产品类别名称采用常见的链接格式 （蓝色并带有下划线）。  
  
##  <a name="MIndicators"></a> 4.使用指示器替换数值  
 使用指示器显示的数量和销售额的在线和分销商渠道的状态。  
  
#### <a name="to-add-an-indicator-for-net-qty-values"></a>若要添加 Net QTY 值的指示器  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  在功能区中，单击**矩形**图标，，然后单击在`[Sum(Net QTY)]`格中`[Product_Category_Name]`中的行组`Channel_Name`列组。  
  
3.  在功能区中，单击**指示器**图标，，然后单击该矩形内的。 **选择指示器类型**对话框将打开带有**方向**所选指示器。  
  
4.  单击**3 个符号**键入，然后依次**确定**。  
  
5.  右键单击该指示器和仪表数据窗格中，单击向下箭头旁边 **（未指定）**。 选择 `Net_QTY`。  
  
6.  重复步骤 2 到 5`[Sum(Net QTY)]`中的单元格`[Product_Category_Name]`内的行组**总**。  
  
#### <a name="to-add-an-indicator-for-net-sales-values"></a>若要添加 Net Sales 值的指示器  
  
1.  在功能区中，单击**矩形**图标，，然后单击内的`[Sum(Net_Sales)]`格中`[Product_Category_Name]`中的行组`Channel_Name`列组。  
  
2.  在功能区中，单击**指示器**图标，，然后单击该矩形内的。  
  
3.  单击**3 个符号**键入，然后依次**确定**。  
  
4.  右键单击该指示器和仪表数据窗格中，单击向下箭头旁边 **（未指定）**。 选择 `Net_Sales`。  
  
5.  重复步骤 1 到 4 用于`[Sum(Net_Sales)]`中的单元格`[Product_Category_Name]`内的行组**总**。  
  
6.  若要预览报表，请单击**运行**。  
  
##  <a name="MParameter"></a> 5.更新参数属性  
 默认情况下，参数是可见的不适合于此报表。 将更新参数属性以便使参数为内部。  
  
#### <a name="to-make-the-parameter-internal"></a>若要使参数为内部  
  
1.  在报表数据窗格中，展开**参数**。  
  
2.  右键单击`@ProductProductCategoryName,`，然后单击**参数属性**。  
  
3.  上**常规**选项卡上，单击**内部**。  
  
4.  （可选） 单击**可用值**并**默认值**选项卡，然后查看它们的选项。 不要更改这些选项卡上的任何选项。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="MTitle"></a> 6.添加报表标题  
 添加到主报表标题。  
  
#### <a name="to-add-a-report-title"></a>若要添加报表标题  
  
1.  在设计图面上，单击**单击此项可添加标题**。  
  
2.  类型**2009 Product Category Sales:Online and Reseller Category:**。  
  
3.  选择您键入的文本。  
  
4.  上**主页**选项卡的功能区中，在字体组中，选择**Times New Roman**字体**16pt**大小，并**加粗**和**斜体**样式。  
  
5.  若要预览报表，请单击**运行**。  
  
##  <a name="MSave"></a> 7.将主报表保存到 SharePoint 库  
 将主报表保存到 SharePoint 库。  
  
#### <a name="to-save-the-report"></a>若要保存报表  
  
1.  若要切换到设计视图，请单击**设计**。  
  
2.  从报表生成器按钮，单击**保存**。  
  
3.  （可选） 若要显示最近使用的报表服务器和 SharePoint 站点的列表，请单击**最近使用的站点和服务器**。  
  
4.  选择或键入必须保存报表权限的 SharePoint 站点的名称。 SharePoint 库的 URL 具有以下语法：  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
5.  导航到要保存报表的库。  
  
6.  在中**名称**，将使用默认名称为**ResellerVSOnlineMain**。  
  
    > [!IMPORTANT]  
    >  将主报表保存到保存钻取报表的同一位置。 若要保存主并钻取报表到其他站点或库，确认**转到报表**主报表中的操作指向正确的钻取报表的位置。  
  
7.  单击“保存” 。  
  
##  <a name="MRunReports"></a> 8.运行主报表和钻取报表  
 运行主报表，然后单击产品类别列以运行钻取报表中的值。  
  
#### <a name="to-run-the-reports"></a>若要运行报表  
  
1.  打开保存报表的 SharePoint 库。  
  
2.  双击 ResellerVSOnlineMain。  
  
     运行该报表，并显示产品类别销售信息。  
  
3.  单击**游戏和玩具**包含产品类别名称的列中的链接。  
  
     将运行钻取报表，显示仅游戏和玩具产品类别的值。  
  
4.  若要返回到主报表，请单击 Internet Explorer 返回按钮。  
  
5.  通过单击其名称 （可选） 浏览其他产品类别。  
  
## <a name="see-also"></a>请参阅  
 [教程&#40;报表生成器&#41;](report-builder-tutorials.md)  
  
  
