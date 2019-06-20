---
title: 第 2 课：将数据添加 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e5a4d0ec80da5c29d513e74df1becca2d5cbb84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404869"
---
# <a name="lesson-2-add-data"></a>第 2 课：添加数据
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程中，你将在 SSDT 中使用表导入向导来连接到 AdventureWorksDW SQL 示例数据库，选择数据、 预览和筛选的数据，然后将数据导入到模型工作区。  
  
通过使用表导入向导，您可以从多种关系数据源导入数据：访问、 SQL、 Oracle、 Sybase、 Informix、 DB2、 Teradata 和的详细信息。 从上述关系数据源中的每个关系数据源导入数据的步骤与下面描述的步骤非常类似。 此外可以使用存储的过程选择数据。 若要了解有关导入数据以及你可以从导入的数据源的不同类型的详细信息，请参阅[数据源](../tabular-models/data-sources-supported-ssas-tabular.md)。  
  
估计的时间才能完成本课程中：**20 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 1 课：创建新的表格模型项目](lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>创建连接  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>若要创建连接到 AdventureWorksDW2014 数据库  
  
1.  在表格模型资源管理器，右键单击**数据源** > **从数据源导入**。  
  
    这将启动表导入向导，它将引导您设置与数据源的连接。 如果看不到表格模型资源管理器，双击**Model.bim**中**解决方案资源管理器**在设计器中打开模型。 
    
    ![as-tabular-lesson2-tme](media/as-tabular-lesson2-tme.png) 

    注意：如果要在 1400年兼容级别创建您的模型，您将看到新的获取数据体验，而不是表导入向导。 对话框将会显示以下，步骤稍有不同，但您将仍将能够跟着介绍一起操作。 
  
2.  在表导入向导中下,**关系数据库**，单击**Microsoft SQL Server** > **下一步**。  
  
3.  在“连接到 Microsoft SQL Server 数据库”  页的“友好的连接名称”  中，键入 **Adventure Works DB from SQL**。  
  
4.  在中**服务器名称**，键入安装了 AdventureWorksDW 数据库的服务器的名称。  
  
5.  在中**数据库名称**字段中，选择**AdventureWorksDW**，然后单击**下一步**。  
  
    ![as-tabular-lesson2-tiw-name](media/as-tabular-lesson2-tiw-name.png)
  
6.  在“模拟信息”  页中，需要指定在导入和处理数据时 Analysis Services 将用于连接数据源的凭据。 确认已选中“特定的 Windows 用户名和密码”  ，在“用户名”  和“密码”  中输入 Windows 登录凭据，然后单击“下一步”  。  
  
    > [!NOTE]  
    > 使用 Windows 用户帐户和密码可提供用于连接到数据源的最安全方法。 有关详细信息，请参阅[模拟](../tabular-models/impersonation-ssas-tabular.md)。  
  
7.  在“选择如何导入数据”  页中，确认已选中“从表和视图的列表中进行选择，以便选择要导入的数据”  。 需要从表和视图的列表中进行选择，因此，单击“下一步”  以便显示源数据库内所有源表的列表。  
  
8.  在中**选择表和视图**页上，选择以下表的复选框：**DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，并**FactInternetSales**。  
  
    **请不要**单击“完成”  。  
  
## <a name="FilterData"></a>Filter the table data  
要导入示例数据库中的 DimCustomer 表包含来自原始 SQL Server Adventure Works 数据库的数据的子集。 将筛选掉不需要导入您的模型时从 DimCustomer 表的列的更多。 如果可能，你将想要筛选出不会为了节省模型使用的内存中空间使用的数据。  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>导入之前对表数据进行筛选  
  
1.  选择的行**DimCustomer**表，并单击**预览并筛选**。 “预览所选表”  窗口将打开，其中显示“DimCustomer”源表中的所有列。  
  
2.  清除位于以下各列顶部的复选框：**SpanishEducation**， **FrenchEducation**， **SpanishOccupation**， **FrenchOccupation**。 

    ![as-tabular-lesson2-tiw-clear](media/as-tabular-lesson2-tiw-clear.png)
  
    因为这些列的值与互联网销售分析无关，所以不需要导入这些列。 消除不必要的列将使您的模型，更小且更高效。  
  
3.  确认已选中所有其他列，然后单击“确定”  。  
  
    请注意，单词**应用的筛选器**此时将显示在**筛选器详细信息**中的列**DimCustomer**行; 如果单击该链接将会看到的文本说明您刚刚应用的筛选器。  
    
    ![as-tabular-lesson2-applied-filters](media/as-tabular-lesson2-applied-filters.png)
    
  
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
现在，已预览并筛选掉不必要的数据，您可以导入您希望的数据的其余部分。 向导将导入表数据以及表之间的任何关系。 在模型中创建新的表和列并不会导入已筛选掉的数据。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>导入选择的表和列数据  
  
1.  检查所做选择。 如果一切看上去没什么问题，请单击**完成**。  
  
    导入数据时，该向导会显示已提取的行的数量。 导入完所有数据之后，将显示一条指示成功的消息。  
    
    ![as-tabular-lesson2-success](media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > 若要查看在导入的表之间自动创建的关系，请在“数据准备”  行上单击“详细信息”  。 
  
2.  单击 **“关闭”** 。  
  
    该向导将关闭并且模型设计器现在显示在导入的表。 
  
## <a name="save-your-model-project"></a>保存模型项目  
请务必经常保存模型项目。  
  
#### <a name="to-save-the-model-project"></a>保存模型项目  
  
-   单击**文件** > **保存所有**。  
  
## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 3 课：标记为日期表](lesson-3-mark-as-date-table.md)。

  
  
