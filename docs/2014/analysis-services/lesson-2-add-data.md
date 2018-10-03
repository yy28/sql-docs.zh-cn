---
title: 第 2 课： 添加数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d2ffda70d3af46434886a7f2878ce238d3190905
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049347"
---
# <a name="lesson-2-add-data"></a>第 2 课：添加数据
  在本课程中，您将使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的“表导入向导”连接到 AdventureWorksDW SQL 数据库，选择数据，预览并筛选数据，然后将数据导入到模型工作区中。  
  
 通过使用“表导入向导”，可以导入来自多种关系数据源的数据：Access、SQL、Oracle、Sybase、Informix、DB2、Teradata 等。 从上述关系数据源中的每个关系数据源导入数据的步骤与下面描述的步骤非常类似。 此外，还可以使用存储过程选择数据。  
  
 若要了解有关导入数据以及可从中导入的不同数据源类型的详细信息，请参阅[数据源（SSAS 表格）](data-sources-ssas-tabular.md)。  
  
 学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课： [第 1 课：创建新的表格模型项目](lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>创建连接  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2012-database"></a>创建到 AdventureWorksDW2012 数据库的连接  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”菜单，然后单击“从数据源导入”。  
  
     这将启动“表导入向导”，它将引导您设置与数据源的连接。 如果“从数据源导入”处于灰显状态，则在“解决方案资源管理器”中双击“Model.bim”，以便在设计器中打开模型。  
  
2.  在“表导入向导”的“关系数据库”下，单击“Microsoft SQL Server”，然后单击“下一步”。  
  
3.  在中**连接到 Microsoft SQL Server 数据库**页上，在**友好的连接名称**，类型`Adventure Works DB from SQL`。  
  
4.  在“服务器名称”中，键入安装了 AdventureWorksDW 数据库的服务器的名称。  
  
5.  在“数据库名称”字段中，单击向下箭头并选择“AdventureWorksDW”，然后单击“下一步”。  
  
6.  在“模拟信息”页中，需要指定在导入和处理数据时 Analysis Services 将用于连接数据源的凭据。 确认已选中“特定的 Windows 用户名和密码”，在“用户名”和“密码”中输入 Windows 登录凭据，然后单击“下一步”。  
  
    > [!NOTE]  
    >  使用 Windows 用户帐户和密码可提供用于连接到数据源的最安全方法。 有关详细信息，请参阅[模拟（SSAS 表格）](tabular-models/impersonation-ssas-tabular.md)。  
  
7.  在“选择如何导入数据”页中，确认已选中“从表和视图的列表中进行选择，以便选择要导入的数据”。 需要从表和视图的列表中进行选择，因此，单击“下一步”以便显示源数据库内所有源表的列表。  
  
8.  在“选择表和视图”页中，选中以下各表的复选框：“DimCustomer”、“DimDate”、“DimGeography”、“DimProduct”、“DimProductCategory”、“DimProductSubcategory”和“FactInternetSales”。  
  
9. 我们希望为模型中的表提供更易理解的名称。 单击“友好名称”列中对应于“DimCustomer”的单元格。 通过从 DimCustomer 中删除“Dim”重命名此表。  
  
10. 重命名其他表：  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |DimDate|date|  
    |DimGeography|Geography|  
    |DimProduct|Product|  
    |DimProductCategory|Product Category|  
    |DimProductSubcategory|Product Subcategory|  
    |FactInternetSales|Internet Sales|  
  
     **请不要**单击“完成”。  
  
 现在已连接到数据库，选择了要导入的表，并向表提供了友好名称，请转到下一部分：[导入之前对表数据进行筛选](#FilterData)。  
  
##  <a name="FilterData"></a> 表数据进行筛选  
 您正在从数据库中导入的 DimCustomer 表包含来自原始 SQL Server Adventure Works 数据库的数据子集。 您将从 DimCustomer 表中筛选掉一些不必要的列。 如果可能，您希望筛选掉将不使用的数据，以便节省模型使用的内存中空间。  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>导入之前对表数据进行筛选  
  
1.  选择“Customer”表中的行，然后单击“预览并筛选”。 “预览所选表”窗口将打开，其中显示“DimCustomer”源表中的所有列。  
  
2.  清除位于以下各列顶部的复选框：  
  
    |Customer|  
    |--------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
     因为这些列的值与互联网销售分析无关，所以不需要导入这些列。 消除不必要的列将使您的模型变小。  
  
3.  确认已选中所有其他列，然后单击“确定”。  
  
     请注意，“Customer”行的“筛选器详细信息”列中现将显示“应用的筛选器”文字；如果单击该链接，将会看到刚才应用的筛选器的文字说明。  
  
4.  通过针对每个表中的以下各列清除复选框，筛选其余的表：  
  
    |date|  
    |----------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |Geography|  
    |---------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |Product|  
    |-------------|  
    |**SpanishProductName**|  
    |**FrenchProductName**|  
    |**FrenchDescription**|  
    |**ChineseDescription**|  
    |**ArabicDescription**|  
    |**HebrewDescription**|  
    |**ThaiDescription**|  
    |**GermanDescription**|  
    |**JapaneseDescription**|  
    |**TurkishDescription**|  
  
    |Product Category|  
    |----------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |Product Subcategory|  
    |-------------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |--------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
 既然您已预览并筛选掉了不必要的数据，您可以导入数据了。 转到下一部分： **导入选择的表和列数据**。  
  
##  <a name="Import"></a> 导入所选的表和列数据  
 现在您可以导入所选数据。 向导将导入表数据以及表之间的任何关系。 将使用您指定的友好名称在模型中创建新表和列，并且不会导入您筛选掉的数据。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>导入选择的表和列数据  
  
1.  检查所做选择。 如果一切都看上去没什么问题，则单击“完成”。  
  
     导入数据时，该向导会显示已提取的行的数量。 导入完所有数据之后，将显示一条指示成功的消息。  
  
    > [!TIP]  
    >  若要查看在导入的表之间自动创建的关系，请在“数据准备”行上单击“详细信息”。  
  
2.  单击 **“关闭”**。  
  
     该向导将关闭并且模型设计器将可见。 每个表都已作为新的选项卡添加到模型设计器中。  
  
## <a name="save-the-model-project"></a>保存模型项目  
 请务必经常保存模型项目。  
  
#### <a name="to-save-the-model-project"></a>保存模型项目  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“文件”菜单，然后单击“全部保存”。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本教程，请转到下一课： [第 3 课：重命名列](rename-columns.md)。  
  
  
