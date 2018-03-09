---
title: "第 2 课： 添加数据 |Microsoft 文档"
ms.custom: 
ms.date: 06/19/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 05a93e001f4b5deb7be0aa3367ad74278e90d70a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-2-add-data"></a>第 2 课：添加数据
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程中，你将在 SSDT 中使用表导入向导以连接到 AdventureWorksDW SQL 示例数据库，选择数据、 预览和筛选的数据，然后将数据导入到模型工作区。  
  
通过使用“表导入向导”，可以导入来自多种关系数据源的数据：Access、SQL、Oracle、Sybase、Informix、DB2、Teradata 等。 从上述关系数据源中的每个关系数据源导入数据的步骤与下面描述的步骤非常类似。 此外可以使用存储的过程选择数据。 若要了解有关导入数据和可以从导入的数据源的不同类型的详细信息，请参阅[数据源](../analysis-services/tabular-models/data-sources-ssas-tabular.md)。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必备条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课： [第 1 课：创建新的表格模型项目](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>创建连接  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>若要创建的连接 AdventureWorksDW2014 数据库  
  
1.  在表格模型资源管理器，右键单击**数据源** > **从数据源导入**。  
  
    这将启动表导入向导，指导您完成设置过程与数据源的连接。 如果看不到表格模型资源管理器中，双击**Model.bim**中**解决方案资源管理器**以在设计器中打开该模型。 
    
    ![作为-表格的第 2 课-时间](../analysis-services/media/as-tabular-lesson2-tme.png) 

    注意： 如果你要在 1400年兼容级别创建您的模型，你将看到新的获取数据体验，而不是表导入向导。 该对话框将显示从下面的步骤稍有不同，但你将仍然能够沿用。 
  
2.  在表导入向导中，在**关系数据库**，单击**Microsoft SQL Server** > **下一步**。  
  
3.  在“连接到 Microsoft SQL Server 数据库”页的“友好的连接名称”中，键入 **Adventure Works DB from SQL**。  
  
4.  在**服务器名称**，键入安装 AdventureWorksDW 数据库的服务器的名称。  
  
5.  在**数据库名称**字段中，选择**AdventureWorksDW**，然后单击**下一步**。  
  
    ![为表格的第 2 课-tiw-名称](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  在“模拟信息”页中，需要指定在导入和处理数据时 Analysis Services 将用于连接数据源的凭据。 确认已选中“特定的 Windows 用户名和密码”，在“用户名”和“密码”中输入 Windows 登录凭据，然后单击“下一步”。  
  
    > [!NOTE]  
    > 使用 Windows 用户帐户和密码可提供用于连接到数据源的最安全方法。 有关详细信息，请参阅[模拟](../analysis-services/tabular-models/impersonation-ssas-tabular.md)。  
  
7.  在“选择如何导入数据”页中，确认已选中“从表和视图的列表中进行选择，以便选择要导入的数据”。 需要从表和视图的列表中进行选择，因此，单击“下一步”以便显示源数据库内所有源表的列表。  
  
8.  在“选择表和视图”页中，选中以下各表的复选框：“DimCustomer”、“DimDate”、“DimGeography”、“DimProduct”、“DimProductCategory”、“DimProductSubcategory”和“FactInternetSales”。  
  
    **请不要**单击“完成”。  
  
## <a name="FilterData"></a>Filter the table data  
您正从示例数据库导入 DimCustomer 表包含从原始的 SQL Server Adventure Works 数据库的数据的子集。 你将筛选出不需要时导入模型中 DimCustomer 表的列的更多。 如果可能，你将想要筛选出不以保存模型使用的内存中空间使用的数据。  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>导入之前对表数据进行筛选  
  
1.  选择的行**DimCustomer**表，并依次**预览和筛选**。 “预览所选表”窗口将打开，其中显示“DimCustomer”源表中的所有列。  
  
2.  清除此复选框，在下面的列的顶部： **SpanishEducation**， **FrenchEducation**， **SpanishOccupation**， **FrenchOccupation**. 

    ![作为-表格的第 2 课-tiw-清除](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    因为这些列的值与互联网销售分析无关，所以不需要导入这些列。 消除不必要的列会使您的模型，较小且更高效。  
  
3.  确认已选中所有其他列，然后单击“确定”。  
  
    请注意单词**应用的筛选器**现在都显示在**筛选器详细信息**中的列**DimCustomer**行; 如果单击该链接，你将看到的文本说明只需应用的筛选器。  
    
    ![作为-表格的第 2 课-已应用的筛选器](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  通过针对每个表中的以下各列清除复选框，筛选其余的表：  
    
    **DimDate**
    
      |“列”|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |“列”|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |“列”|  
      |-----------|  
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
  
    **DimProductCategory**
  
      |“列”|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |“列”|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |“列”|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
现在，预览并筛选出不必要的数据后，你可以导入所需数据执行操作的其余的部分。 向导将导入表数据以及表之间的任何关系。 在模型中创建新表和列和筛选出的数据将不导入。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>导入选择的表和列数据  
  
1.  检查所做选择。 如果一切看上去没有问题，请单击**完成**。  
  
    导入数据时，该向导会显示已提取的行的数量。 导入完所有数据之后，将显示一条指示成功的消息。  
    
    ![作为-表格的第 2 课-成功](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > 若要查看在导入的表之间自动创建的关系，请在“数据准备”行上单击“详细信息”。 
  
2.  单击 **“关闭”**。  
  
    向导将关闭，并且模型设计器现在将显示你导入的表。 
  
## <a name="save-your-model-project"></a>保存您的模型项目  
请务必经常保存您的模型项目。  
  
#### <a name="to-save-the-model-project"></a>保存模型项目  
  
-   Click **File** > **Save All**.  
  
## <a name="whats-next"></a>下一步是什么？
转到下一课：[第 3 课： 标记为日期表](../analysis-services/lesson-3-mark-as-date-table.md)。

  
  
