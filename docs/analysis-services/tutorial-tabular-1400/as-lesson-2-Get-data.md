---
title: Analysis Services 教程第 2 课：获取数据 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 01bf31c3d4f89b77ebdceae2e69d4054a578b03f
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685314"
---
# <a name="get-data"></a>获取数据

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，您使用**获取数据**要连接到 AdventureWorksDW 示例数据库，选择数据，预览并筛选器，并将导入到模型工作区。  
  
实质上，获取数据是 Power Query，提供用于连接到和重塑数据建模和分析大量的工具。 若要了解详细信息，请参阅[Power Query 文档](https://docs.microsoft.com/power-query/)。 

> [!NOTE]
> 任务和图像在本教程演示如何连接到的本地服务器上的 AdventureWorksDW2014 数据库。 在某些情况下，Azure SQL 数据仓库上的 AdventureWorksDW 数据库可能会显示不同的对象;但是，它们是完全相同。
  
学完本课的预计时间：**10 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 1 课：创建新的表格模型项目](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>创建连接  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>若要创建到 AdventureWorksDW 数据库的连接  
  
1.  在中**表格模型资源管理器**，右键单击**数据源** > **从数据源导入**。  
  
    这将启动**获取数据**，其中介绍了如何连接到数据源。 如果没有看到表格模型资源管理器，在**解决方案资源管理器**，双击**Model.bim**在设计器中打开模型。 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  在获取数据中，单击**数据库** > **SQL Server 数据库** > **Connect**。  
  
3.  在中**SQL Server 数据库**对话框中**服务器**，键入安装 AdventureWorksDW 数据库的服务器的名称，然后单击**Connect**。  

4.  当系统提示输入凭据，您需要指定 Analysis Services 用来连接到数据源导入和处理数据时的凭据。 在中**模拟模式**，选择**模拟帐户**，并输入凭据，然后单击**Connect**。 建议使用的帐户的密码不过期。

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > 使用 Windows 用户帐户和密码可提供用于连接到数据源的最安全方法。
  
5.  在导航器中，选择**AdventureWorksDW**数据库，然后依次**确定**。这将创建数据库的连接。 
  
6.  在导航器中，选择以下表的复选框：**DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，并**FactInternetSales**。  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
单击确定后，将打开查询编辑器。 在下一部分中，选择你想要导入的数据。

  
## <a name="filter-the-table-data"></a>表数据进行筛选  

AdventureWorksDW 示例数据库中的表具有不需要包括在模型中的数据。 如果可能，你想要筛选出不必要的数据以节省模型使用的内存中空间。 因此会在不导入到工作区数据库或模型数据库完成部署后筛选出某些从表的列。 
  
#### <a name="to-filter-the-table-data-before-importing"></a>若要导入之前筛选表数据  
  
1.  在查询编辑器中，选择**DimCustomer**表。 将显示数据源 （AdventureWorksDW 示例数据库） 中的 DimCustomer 表的视图。 
  
2.  （Ctrl + 单击） 的多选**SpanishEducation**， **FrenchEducation**， **SpanishOccupation**， **FrenchOccupation**，然后右键单击，然后依次**删除列**。 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    因为这些列的值与互联网销售分析无关，所以不需要导入这些列。 消除不必要的列可以使模型更小且更高效。  

    > [!TIP]
    > 如果犯错，可以通过删除中的一个步骤来备份**应用的步骤**。   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  通过在每个表中删除以下列筛选其余的表：  
    
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
  
      不删除任何列。
  
## <a name="Import"></a>Import the selected tables and column data  

现在，已预览并筛选掉不必要的数据，您可以导入您希望的数据的其余部分。 向导将导入表数据以及表之间的任何关系。 在模型中创建新的表和列并筛选出的数据将不导入。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>导入选择的表和列数据  
  
1.  检查所做选择。 如果一切看上去没什么问题，请单击**导入**。 数据处理对话框中显示的要导入数据从数据源到工作区数据库的状态。
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  单击 **“关闭”**。  

  
## <a name="save-your-model-project"></a>保存模型项目  

请务必经常保存模型项目。  
  
#### <a name="to-save-the-model-project"></a>保存模型项目  
  
-   单击**文件** > **保存所有**。  
  
## <a name="whats-next"></a>下一步是什么？

[第 3 课：标记为日期表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)。

  
  
