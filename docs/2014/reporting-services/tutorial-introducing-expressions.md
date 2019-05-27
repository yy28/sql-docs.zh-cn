---
title: 教程：表达式简介 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79563abac2c6a9ed64dff93667ff3d3966b70bc5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098847"
---
# <a name="tutorial-introducing-expressions"></a>教程：表达式简介
  表达式帮助您创建功能强大、灵活的报表。 本教程指导您创建和实现使用常用函数和运算符的表达式。 将使用**表达式**对话框可以编写表达式的连接名称值、 查找中单独的数据集中的值显示不同的图片基于字段值，等等。  
  
 报表是一个条纹形式的报表，用白色和彩色交替显示行颜色。 报表包括用于选择非白色行的颜色的参数。  
  
 下图显示与您将创建的报表类似的报表。  
  
 ![rs_ExpressionsTutorial](../../2014/tutorials/media/rs-expressionstutorial.gif "rs_ExpressionsTutorial")  
  
##  <a name="BackToTop"></a> 您将学习  
 在本教程中，您将学习如何执行下列操作：  
  
1.  [从表或矩阵向导创建表报表和数据集](#Setup)  
  
2.  [更新默认名称分别为数据源和数据集](#UpdateNames)  
  
3.  [显示名字首字母和姓氏](#Concatenate)  
  
4.  [使用图像显示性别](#Gender)  
  
5.  [查找 CountryRegion 名称](#Lookup)  
  
6.  [计算自上次采购后的天数](#Count)  
  
7.  [使用指示器显示销售情况对比](#Indicator)  
  
8.  [使"绿色图条"报表的报表](#GreenBar)  
  
### <a name="other-optional-steps"></a>其他可选步骤  
  
-   [日期列的格式](#DateFormat)  
  
-   [添加报表标题](#Title)  
  
-   [保存报表](#Save)  
  
 估计的时间才能完成本教程中：30 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="Setup"></a> 1.使用表向导或矩阵向导创建表报表和数据集  
 创建表报表、数据源和数据集。 在设计表的布局时，将只包含若干字段。 完成向导后，您将手动添加列。 使用该向导可以方便地对表进行布局和应用样式。  
  
> [!NOTE]  
>  在本教程中，由于查询包含了数据值，因此它不需要外部数据源。 这样，查询就会非常长。 在业务环境中，查询不会包含数据。 本教程中的查询仅供学习使用。  
  
> [!NOTE]  
>  在本教程中，将向导的多个步骤合并为一个过程。 有关如何转到报表服务器、选择数据源和创建数据集的分步说明，请参阅本系列教程中的第一个教程：[教程：生成基本表报表（报表生成器）](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)。  
  
#### <a name="to-create-a-new-table-report"></a>创建新的表报表  
  
1.  单击**启动**，依次指向**程序**，单击[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**报表生成器**，然后单击**报表生成器**。  
  
     此时将显示 **“入门”** 对话框。  
  
    > [!NOTE]  
    >  如果**Getting Started**对话框不会出现，从**报表生成器**按钮，再单击**新建**。  
  
    > [!NOTE]  
    >  如果想要使用报表生成器的 ClickOnce 版本，打开报表管理器，然后单击**报表生成器**，或转到 SharePoint 站点的 Reporting Services 内容类型如启用了报表，并单击**报表生成器报表**上**新的文档**菜单上的**文档**选项卡上的共享的文档库。  
  
2.  在左窗格中，确认已选中 **“新建报表”** 。  
  
3.  在右窗格中，单击“表或矩阵向导”。  
  
4.  在“选择数据集”页上，单击“创建数据集”。  
  
5.  单击“下一步” 。  
  
6.  在“选择数据源的连接”页上，选择类型为“SQL Server”的数据源。 从列表中选择一个数据源或浏览到报表服务器以选择一个数据源。  
  
7.  单击“下一步” 。  
  
8.  在“设计查询”页上，单击“编辑为文本”。  
  
9. 将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Unknown' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2010-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2010-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2010-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2010-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2010-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2010-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2010-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2010-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2010-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2010-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2010-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2010-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2010-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2010-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2010-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2010-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2010-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    ```  
  
     该查询指定列名称，这些名称包括出生日期、名字、姓氏、省/市/自治区、国家/地区标识符、性别和年初至今的采购信息。  
  
10. 在查询设计器工具栏中，单击“运行”(**!**)。 结果集显示 20 行的数据，包括以下列：“FirstName”、“LastName”、“StateProvince”、“CountryRegionID”、“Gender”、“YTDPurchase”和“LastPurchase”。  
  
11. 单击“下一步” 。  
  
12. 在“排列字段”页上，将以下字段按指定顺序从“可用字段”列表拖到“值”列表。  
  
    -   StateProvince  
  
    -   CountryRegionID  
  
    -   LastPurchase  
  
    -   YTDPurchase  
  
     因为 CountryRegionID 和 YTDPurchase 包含数值数据，所以，SUM 聚合将默认应用于这两个字段。  
  
    > [!NOTE]  
    >  FirstName 和 LastName 字段不包括在内。 您将在后面的步骤中添加这两个字段。  
  
13. 在中**值**列表中，右键单击`CountryRegionID`然后单击**总和**选项。  
  
     Sum 不再应用于 CountryRegionID。  
  
14. 在“值”列表中，右键单击“YTDPurchase”，然后单击“Sum”选项。  
  
     Sum 不再应用于 YTDPurchase。  
  
15. 单击“下一步” 。  
  
16. 在“选择布局”页上，单击“下一步”。  
  
17. 上**选择一种样式**页上，单击**盖板**，然后单击**完成**。  
  
##  <a name="UpdateNames"></a> 2.更新数据源和数据集的默认名称  
  
#### <a name="to-update-the-default-name-of-the-data-source"></a>更新数据源的默认名称  
  
1.  在“报表数据”窗格中，展开“数据源”。  
  
2.  右键单击“DataSource1”，然后单击“数据源属性”。  
  
3.  在“名称”框中，键入“ExpressionsDataSource”  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-update-the-default-name-of-the-dataset"></a>更新数据集的默认名称  
  
1.  在“报表数据”窗格中，展开“数据集”。  
  
2.  右键单击“DataSet1”，然后单击“数据集属性”。  
  
3.  在“名称”框中，键入 **Expressions**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Concatenate"></a> 3.显示名字、首字母和姓氏  
 在表达式中使用 **Left** 函数和 **Concatenate** (**&**) 运算符（其计算结果为包括首字母和姓氏的名称）。 你可以逐步生成表达式，也可以跳过一些步骤，将表达式从教程复制/粘贴到“表达式”对话框中。  
  
#### <a name="to-add-the-name-column"></a>添加 Name 列  
  
1.  右键单击“StateProvince”列，指向“插入列”，然后单击“左”。  
  
     一个新列添加到“StateProvince”列的左侧。  
  
2.  单击新列的标题，然后键入 **Name**  
  
3.  右键单击“Name”列的数据单元，然后单击“表达式”。  
  
4.  在“表达式”对话框中，展开“常见函数”，然后单击“文本”。  
  
5.  在“项”列表中，双击“左”。  
  
     将 **Left** 函数添加到表达式中。  
  
6.  在“类别”列表中，单击“字段(表达式)”。  
  
7.  在“值”列表中，双击 **FirstName**。  
  
8.  键入 **, 1)**  
  
     此表达式将从 **FirstName** 值提取一个字符，从左侧开始计数。  
  
9. 键入 **&" "&**  
  
10. 在“值”列表中，双击 **LastName**。  
  
     完成的表达式： `=Left(Fields!FirstName.Value, 1) &" "& Fields!LastName.Value`  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 单击 **“运行”** 以预览报表。  
  
##  <a name="Gender"></a> 4.使用图像显示性别  
 使用图像可以显示人员的性别，并且通过使用第三个图像标识未知性别值。 您将向报表添加三个隐藏的图像和一个用于显示这些图像的新列，然后基于“性别”字段的值确定在列中显示的图像。  
  
 在使报表成为条纹形式报表时，若要将颜色应用于包含图像的表单元，需要添加一个矩形，然后将图像添加到该矩形。 您需要使用矩形，因为背景色可以应用于矩形，但不能应用于图像。  
  
 本教程使用随 Windows 一起安装的图像，但您可以使用任何可用的图像。 您将使用嵌入图像，但这些图像无需安装在本地计算机或报表服务器上。  
  
#### <a name="to-add-images-to-the-report-body"></a>向报表正文添加图像  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  在功能区的“插入”选项卡上，单击“图像”，然后在表下面的报表正文中单击。  
  
     将打开“图像属性”对话框。  
  
3.  单击“导入”并导航到 C:\Users\Public\Public Pictures\Sample Pictures。  
  
4.  单击“Penguins.JPG”，然后单击“打开”。  
  
     在“图像属性”对话框中，单击“可见性”，然后单击“隐藏”选项。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  重复执行第 2 步到第 5 步，但选择 Koala.JPG。  
  
7.  重复执行第 2 步到第 5 步，但选择 Tulips.JPG。  
  
#### <a name="to-add-the-gender-column"></a>添加 Gender 列  
  
1.  右键单击“名称”列，指向“插入列”，然后单击“右”。  
  
     一个新列添加到 **Name** 列的右侧。  
  
2.  单击新列的标题，然后键入 **Gender**  
  
#### <a name="to-add-a-rectangle"></a>添加矩形  
  
-   在功能区的“插入”选项卡上，单击“矩形”，然后在 **Gender** 列的数据单元中单击。  
  
     将在该单元中添加一个矩形。  
  
#### <a name="to-add-an-image-to-the-rectangle"></a>向矩形添加图像  
  
1.  在矩形中右键单击，指向“插入”，然后单击“图像”。  
  
2.  在“图像属性”对话框中，单击“使用此图像”旁的向下箭头，然后选择添加的图像之一，例如 Penguins.JPG。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-use-images-to-show-gender"></a>若要使用图像显示性别  
  
1.  右键单击 **Gender** 列的数据单元中的图像，然后单击“图像属性”。  
  
2.  在“图像属性”对话框中，单击“使用此图像”文本框旁边的表达式 **fx**按钮。  
  
3.  在“表达式”对话框中，展开“常见函数”，然后单击“程序流”。  
  
4.  在“项”列表中，双击“Switch”。  
  
5.  在“类别”列表中，单击“字段(表达式)”。  
  
6.  在“值”列表中，双击 **Gender**。  
  
7.  键入 **="Male", "Koala",**  
  
8.  在“值”列表中，双击 **Gender**。  
  
9. 键入 **="Female", "Penguins",**  
  
10. 在“值”列表中，双击 **Gender**。  
  
11. 键入 **="Unknown", "Tulips")**  
  
     完成的表达式： `=Switch(Fields!Gender.Value ="Male", "Koala",Fields!Gender.Value ="Female","Penguins",Fields!Gender.Value ="Unknown","Tulips")`  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. 再次单击“确定”以关闭“图像属性”对话框。  
  
14. 单击 **“运行”** 以预览报表。  
  
##  <a name="Lookup"></a> 5.查找 CountryRegion 名称  
 创建 CountryRegion 数据集，使用“Lookup”函数显示国家/地区的名称，而非国家/地区的标识符。  
  
#### <a name="to-create-the-countryregion-dataset"></a>创建 CountryRegion 数据集  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  在“报表数据”窗格中，单击“新建”，然后单击“数据集”。  
  
3.  单击“使用在我的报表中嵌入的数据集”。  
  
4.  在“数据源”列表中，选择“ExpressionsDataSource”。  
  
5.  在“名称”框中，键入“CountryRegion”  
  
6.  确保已选择“文本”查询类型，然后单击“查询设计器”。  
  
7.  单击 **“编辑为文本”**。  
  
8.  复制并将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. 单击 **“运行”** (**!**) 以运行查询。  
  
     查询结果是国家/地区标识符和名称。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 再次单击“确定”以关闭“数据集属性”对话框。  
  
#### <a name="to-look-up-values-in-the-countryregion-dataset"></a>查找 CountryRegion 数据集中的值  
  
1.  单击**Country Region ID**列标题，删除文本：ID。  
  
2.  右键单击“Country Region”列的数据单元，然后单击“表达式”。  
  
3.  删除表达式，开头的等号 (=) 除外。  
  
     剩余表达式为： `=`  
  
4.  在“表达式”对话框中，展开“常见函数”，然后单击“杂项”。  
  
5.  在“项”列表中，双击“Lookup”。  
  
6.  在“类别”列表中，单击“字段(表达式)”。  
  
7.  在中**值**列表中，双击`CountryRegionID`。  
  
8.  如果鼠标光标不是紧接 `CountryRegionID.Value` 之后，请将光标置于其后。  
  
9. 删除右括号，然后键入 **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**  
  
     完成的表达式： `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
     该 **Lookup** 函数的语法指定对 CountryRegion 数据集中的 CountryRegionID 和 ID 进行查找，返回 CountryRegion 值（该值也在 CountryRegion 数据集中）。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. 单击 **“运行”** 以预览报表。  
  
##  <a name="Count"></a> 6.计算自上次采购后的天数  
 添加一列，然后使用**现在**函数或`ExecutionTime`购买了内置全局变量计算某人的最后一个至今的天数。  
  
#### <a name="to-add-the-days-ago-column"></a>添加 Days Ago 列  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  右键单击“Last Purchase”列，指向“插入列”，然后单击“右”。  
  
     一个新列将添加到“Last Purchase”列的右侧。  
  
3.  在列标题中，键入“Days Ago”  
  
4.  右键单击“Days Ago”列的数据单元格，然后单击“表达式”。  
  
5.  在“表达式”对话框中，展开“常见函数”，然后单击“日期和时间”。  
  
6.  在“项”列表中，双击 **DateDiff**。  
  
7.  如果鼠标光标不是紧接 `DateDiff(` 之后，请将光标置于其后。  
  
8.  键入 **"d",**  
  
9. 在“类别”列表中，单击“字段(表达式)”。  
  
10. 在“值”列表中，双击 **LastPurchase**。  
  
11. 如果鼠标光标不是紧接 `Fields!LastPurchase.Value` 之后，请将光标置于其后。  
  
12. 键入 **,**  
  
13. 在“类别”列表中，再次单击“日期和时间”。  
  
14. 在“项”列表中，双击 **Now**。  
  
    > [!WARNING]  
    >  在生产报表中，不应在报表呈现过程中会多次计算的表达式中（例如，在报表的详细信息行中）使用 **Now** 函数。 **Now** 的值随行变化，不同的值会影响表达式的计算结果，这将导致结果略微不一致。 应改用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供的 `ExecutionTime` 全局变量。  
  
15. 如果鼠标光标不是紧接 `Now(` 之后，请将光标置于其后。  
  
16. 删除左括号，然后键入 **)**  
  
     完成的表达式： `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Indicator"></a> 7.使用指示器显示销售情况对比  
 添加新列并使用指示器显示某个人的年度截止到现在 (YTD) 采购量是高于还是低于平均 YTD 采购量。 **Round** 函数从值中去掉小数部分。  
  
 该指示器及其状态的配置需要许多步骤。 如果需要，在"配置指示器"过程中，可以跳过一些步骤，并复制/粘贴到本教程中已完成的表达式**表达式**对话框。  
  
#### <a name="to-add-the--or---avg-sales-column"></a>添加 + or - AVG Sales 列  
  
1.  右键单击“YTD Purchase”列，指向“插入列”，然后单击“右”。  
  
     将一个新列添加到“YTD Purchase”列的右侧。  
  
2.  单击该列的标题，然后键入 **+ or - AVG Sales**  
  
#### <a name="to-add-an-indicator"></a>添加指示器  
  
1.  在功能区的“插入”选项卡上，单击“指示器”，然后在 **+ or - AVG Sales** 列的数据单元中单击。  
  
     “选择指示器类型”对话框即会打开。  
  
2.  在图标集的“方向”组中，单击由三个灰色箭头构成的图标集。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-configure-the-indicator"></a>配置指示器  
  
1.  右键单击指示器，单击“指示器属性”，然后单击“值和状态”。  
  
2.  单击“值”文本框旁边的表达式“fx”按钮。  
  
3.  在“表达式”对话框中，展开“常见函数”，然后单击 **Math**。  
  
4.  在“项”列表中，双击 **Round**。  
  
5.  在“类别”列表中，单击“字段(表达式)”。  
  
6.  在“值”列表中，双击 **YTDPurchase**。  
  
7.  如果鼠标光标不是紧接 `Fields!YTDPurchase.Value` 之后，请将光标置于其后。  
  
8.  键入 **-**  
  
9. 再次展开“常见函数”，然后单击 **Aggregate**。  
  
10. 在“项”列表中，双击 **Avg**。  
  
11. 在“类别”列表中，单击“字段(表达式)”。  
  
12. 在“值”列表中，双击 **YTDPurchase**。  
  
13. 如果鼠标光标不是紧接 `Fields!YTDPurchase.Value` 之后，请将光标置于其后。  
  
14. 键入 **, "Expressions"))**  
  
     完成的表达式： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. 在“状态度量单位”框中，选择“数字”。  
  
17. 在具有向下箭头的行中，单击“起始”值的文本框右侧的 **fx**按钮。  
  
18. 在“表达式”对话框中，展开“常见函数”，然后单击 **Math**。  
  
19. 在“项”列表中，双击 **Round**。  
  
20. 在“类别”列表中，单击“字段(表达式)”。  
  
21. 在“值”列表中，双击 **YTDPurchase**。  
  
22. 如果鼠标光标不是紧接 `Fields!YTDPurchase.Value` 之后，请将光标置于其后。  
  
23. 键入 **-**  
  
24. 再次展开“常见函数”，然后单击 **Aggregate**。  
  
25. 在“项”列表中，双击 **Avg**。  
  
26. 在“类别”列表中，单击“字段(表达式)”。  
  
27. 在“值”列表中，双击 **YTDPurchase**。  
  
28. 如果鼠标光标不是紧接 `Fields!YTDPurchase.Value` 之后，请将光标置于其后。  
  
29. 键入 **, "Expressions")) < 0**  
  
     完成的表达式： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. 在“结束”值的文本框中，键入 **0**  
  
32. 单击具有水平方向箭头的行，然后单击“删除”。  
  
33. 在具有向上箭头的行的“起始”框中，键入 **0**  
  
34. 单击“结束”值的文本框右侧的 **fx** 按钮。  
  
35. 在中**表达式**对话框框中，创建表达式： `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. 再次单击“确定”以关闭“指示器属性”对话框。  
  
38. 单击 **“运行”** 以预览报表。  
  
##  <a name="GreenBar"></a> 8.使"绿色图条"报表的报表  
 使用参数指定要应用于报表的交替行的颜色，使报表成为条纹形式的报表。  
  
#### <a name="to-add-a-parameter"></a>添加参数  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  在“报表数据”窗格中，右键单击“参数”，然后单击“添加参数”。  
  
     此时将打开 **“报表参数属性”** 对话框。  
  
3.  在“提示符”下，键入“选择颜色”  
  
4.  在“名称”中，键入 **RowColor**  
  
5.  在左窗格中单击“可用值”。  
  
6.  单击“指定值”。  
  
7.  单击 **“添加”**。  
  
8.  在中**标签**框中，键入：**黄色**  
  
9. 在“值”框中，键入 **Yellow**  
  
10. 单击 **“添加”**。  
  
11. 在“标签”框中，键入“绿色”  
  
12. 在“值”框中，键入“淡绿色”  
  
13. 单击 **“添加”**。  
  
14. 在“标签”框中，键入“蓝色”  
  
15. 在“值”框中，键入“浅蓝色”  
  
16. 单击 **“添加”**。  
  
17. 在“标签”框中，键入“粉色”  
  
18. 在“值”框中，键入 **Pink**  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-apply-alternating-colors-to-detail-rows"></a>将交替颜色应用于详细信息行  
  
1.  单击功能区上的“视图”选项卡，确认选中了“属性”。  
  
2.  按住 Shift 键单击“Name”列的数据单元。  
  
3.  逐一单击行中的其他单元。  
  
4.  在“属性”窗格中，单击 **BackgroundColor**。  
  
     如果“属性”窗格按类别列出属性，则“BackgroundColor”在“填充”类别下。  
  
5.  单击向下箭头，然后单击“表达式”。  
  
6.  在“表达式”对话框中，展开“常见函数”，然后单击“程序流”。  
  
7.  在“项”列表中，双击“IIf”。  
  
8.  展开“常见函数”，然后单击“Aggregate”。  
  
9. 在“项”列表中，双击“RunningValue”。  
  
10. 在“类别”列表中，单击“字段(表达式)”。  
  
11. 在“值”列表中，双击 **FirstName**。  
  
12. 如果鼠标光标不是紧接 `Fields!FirstName.Value` 之后，请将光标置于其后并键入 **,**  
  
13. 展开“常见函数”，然后单击“Aggregate”。  
  
14. 在“项”列表中，双击“Count”。  
  
15. 如果鼠标光标不是紧接 `Count(` 之后，请将光标置于其后。  
  
16. 删除左的括号，然后键入 **，"Expressions")**  
  
    > [!NOTE]  
    >  Expressions 是要对其数据行进行计数的数据集的名称。  
  
17. 展开“运算符”，然后单击“算术”。  
  
18. 在“项”列表中，双击“Mod”。  
  
19. 如果鼠标光标不是紧接 `Mod` 之后，请将光标置于其后。  
  
20. 键入 **2 =0,**  
  
    > [!IMPORTANT]  
    >  请确保在键入数值 2 之前包含一个空格。  
  
21. 单击“参数”，在“值”列表中，双击“RowColor”。  
  
22. 如果鼠标光标不是紧接 `Parameters!RowColor.Value` 之后，请将光标置于其后。  
  
23. 键入 **，"White")**  
  
     完成的表达式： `=IIf(RunningValue(Fields!FirstName.Value,Count, "Expressions") Mod 2 =0, Parameters!RowColor.Value, "White")`  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="run-the-report"></a>运行报表  
  
1.  如果不是在“开始”选项卡上，请单击“开始”返回到设计视图。  
  
2.  单击 **“运行”**。  
  
3.  在“选择颜色”下拉列表中，选择报表上非白色条的颜色。  
  
4.  单击 **“查看报表”**。  
  
     该报表呈现，报表行交替呈现您所选的背景。  
  
##  <a name="DateFormat"></a> （可选）日期列的格式  
 设置包含日期的“Last Purchase”列的格式。  
  
#### <a name="to-format-date-column"></a>若要设置日期列的格式  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  右键单击“Last Purchase”列的数据单元，然后单击“文本框属性”。  
  
3.  在“文本框属性”对话框中，依次单击“数字”、“日期”和类型“2000/1/31”**\***。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Title"></a> （可选）添加报表标题  
 为报表添加标题。  
  
#### <a name="to-add-a-report-title"></a>添加报表标题  
  
1.  在设计图面上，单击“单击以添加标题”。  
  
2.  键入 **Sales Comparison Summary**，然后在文本框外部单击。  
  
3.  右键单击包含 **Sales Comparison Summary** 的文本框，然后单击“文本框属性”。  
  
4.  在“文本框属性”对话框中，单击“字体”。  
  
5.  在“大小”列表中，选择“18pt”。  
  
6.  在“颜色”列表中，选择“灰色”。  
  
7.  选择“粗体”和“斜体”。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> （可选）保存报表  
 您可以将报表保存到报表服务器、SharePoint 库或本地计算机。 有关详细信息，请参阅[保存报表（报表生成器）](report-builder/saving-reports-report-builder.md)。  
  
 在本教程中，将报表保存到报表服务器。 如果您没有对报表服务器的访问权限，则可以保存到您的计算机。  
  
#### <a name="to-save-the-report-to-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“最近使用的站点和服务器”**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为默认报表位置的报表文件夹的内容。  
  
4.  在“名称”中，用“Sales Comparison Summary”替换默认名称。  
  
5.  单击“保存” 。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-to-your-computer"></a>将报表保存到计算机  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“桌面”**、 **“我的文档”** 或 **“我的电脑”**，然后浏览到要将报表保存到的文件夹。  
  
3.  在“名称”中，用“Sales Comparison Summary”替换默认名称。  
  
4.  单击“保存” 。  
  
## <a name="see-also"></a>请参阅  
 [表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)   
 [指标&#40;报表生成器和 SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)   
 [图像、文本框、矩形和线条（报表生成器和 SSRS）](report-design/rectangles-and-lines-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](report-design/tables-report-builder-and-ssrs.md)   
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
