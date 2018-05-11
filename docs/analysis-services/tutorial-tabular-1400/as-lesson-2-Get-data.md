---
title: Analysis Services 教程第 2 课： 获取数据 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb7c9b19950036baff8dbe4dd52447040cd9a571
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="get-data"></a>获取数据

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你使用**获取数据**要连接到 AdventureWorksDW 示例数据库，选择数据、 预览和筛选器，并将导入模型工作区。  
  
通过使用获取数据，你可以从各种源导入数据。 此外可以使用 Power 查询 M 公式表达式查询数据或[本机 SQL 查询表达式](../tabular-models/ssas-import-query.md)。

> [!NOTE]
> 任务和在本教程中的图像显示连接到本地服务器上的 AdventureWorksDW2014 数据库。 在某些情况下，Azure SQL 数据仓库上的 AdventureWorksDW 数据库可能会显示不同的对象;但是，它们是完全相同。
  
学完本课的估计时间：**10 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[第 1 课： 创建新的表格模型项目](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>创建连接  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>若要创建到 AdventureWorksDW 数据库的连接  
  
1.  在**表格模型资源管理器**，右键单击**数据源** > **从数据源导入**。  
  
    这将启动**获取数据**，引导你通过连接到数据源。 如果你看不到表格模型资源管理器，在**解决方案资源管理器**，双击**Model.bim**以在设计器中打开该模型。 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  获取数据，在单击**数据库** > **SQL Server 数据库** > **连接**。  
  
3.  在**SQL Server 数据库**对话框，请在**服务器**，键入安装 AdventureWorksDW 数据库的服务器的名称，然后单击**连接**。  

4.  当系统提示输入凭据，你需要指定 Analysis Services 用于连接到数据源导入和处理数据时的凭据。 在**模拟模式**，选择**模拟帐户**，然后输入凭据，，然后单击**连接**。 建议你使用的帐户的密码不过期其中。

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > 使用 Windows 用户帐户和密码可提供用于连接到数据源的最安全方法。
  
5.  在导航器中，选择**AdventureWorksDW**数据库，并依次**确定**。这将创建数据库的连接。 
  
6.  在导航器中，选择以下各表的复选框： **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，和**FactInternetSales**。  

    ![作为-第 2 课-选择的表](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
单击确定后，将打开查询编辑器。 在下一步的部分中，选择你想要导入的数据。

  
## <a name="filter-the-table-data"></a>筛选的表数据  

AdventureWorksDW 示例数据库中的表具有无需在模型中包括的数据。 如果可能，你想要筛选出不必要的数据，以节省内存中模型使用的空间。 你筛选出某些表中的列以便它们在未导入到工作区数据库或 model 数据库后已部署的不同而不同。 
  
#### <a name="to-filter-the-table-data-before-importing"></a>若要在导入之前筛选的表数据  
  
1.  在查询编辑器中，选择**DimCustomer**表。 将显示在数据源 （AdventureWorksDW 示例数据库） DimCustomer 表的视图。 
  
2.  多重选择 （Ctrl + 单击） **SpanishEducation**， **FrenchEducation**， **SpanishOccupation**， **FrenchOccupation**，右键单击，然后再单击**删除列**。 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    因为这些列的值与互联网销售分析无关，所以不需要导入这些列。 消除不必要的列使您的模型，更小、 更有效。  

    > [!TIP]
    > 如果犯错，你可以通过删除中的一个步骤中备份**应用步骤**。   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  通过在每个表中删除以下各列筛选对其他表：  
    
    **DimDate**
    
      |列|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |列|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |列|  
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
  
      |列|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |列|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      不删除任何列。
  
## <a name="Import"></a>导入所选的表和列数据  

现在，预览并筛选出不必要的数据后，你可以导入所需数据执行操作的其余的部分。 向导将导入表数据以及表之间的任何关系。 在模型中创建新表和列和筛选出的数据将不导入。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>导入选择的表和列数据  
  
1.  检查所做选择。 如果一切看上去没有问题，请单击**导入**。 数据处理对话框中显示的数据导入从你的数据源到工作区数据库的状态。
  
    ![作为第 2 课成功](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  单击 **“关闭”**。  

  
## <a name="save-your-model-project"></a>保存您的模型项目  

请务必经常保存您的模型项目。  
  
#### <a name="to-save-the-model-project"></a>保存模型项目  
  
-   Click **File** > **Save All**.  
  
## <a name="whats-next"></a>下一步是什么？

[第 3 课： 将标记为日期表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)。

  
  
