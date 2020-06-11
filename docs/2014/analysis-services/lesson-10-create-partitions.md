---
title: 第11课：创建分区 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 545c6f45339047d3a632f9e18d69108f3c8b5111
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543579"
---
# <a name="lesson-11-create-partitions"></a>第 11 课：创建分区
  在本课中，您将创建分区，以便将 Internet Sales 表划分为可独立于其他分区进行处理（刷新）的更小逻辑部分。 默认情况下，模型中包含的每个表都有一个分区，其中包含表的所有列和行。 对于 Internet Sales 表，我们希望按年份划分数据;每个表的5年的一个分区。  然后，每个分区可独立进行处理。 若要了解详细信息，请参阅[分区（SSAS 表格）](tabular-models/partitions-ssas-tabular.md)。  
  
 学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课程中的任务之前，应该已完成上一课： [第 10 课：创建层次结构](lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>创建分区  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>在 Internet Sales 表中创建分区  
  
1.  在模型设计器中，依次单击“Internet Sales”**** 表、“表”**** 菜单和“分区”****。  
  
     “分区管理器”**** 对话框将打开。  
  
2.  在 "**分区管理器**" 对话框的 "**分区**" 中，单击 " **Internet 销售**" 分区。  
  
3.  在 "**分区名称**" 中，将名称更改为 `Internet Sales 2005` 。  
  
    > [!TIP]  
    >  在继续执行下一步之前，您将注意到“表预览”窗口中的列名显示模型表中包含的、但其列名来自源中的这些列（已勾选）。 这是因为“表预览”窗口显示源表（而非模型表）中的列。  
  
4.  选择位于预览窗口右侧上方的“查询编辑器”**** 按钮。  
  
     因为您希望分区只包含特定期间内的那些行，所以您必须包含 WHERE 子句。 您只能通过使用 SQL 语句创建 WHERE 子句。  
  
5.  在“SQL 语句”**** 字段中，通过粘贴以下语句替换现有语句：  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2005-01-01 00:00:00') AND ([OrderDate] < N'2006-01-01 00:00:00'))  
    ```  
  
     本语句指定分区应包含以下行中的所有数据：对于这些行，OrderDate 对应于在 WHERE 子句中指定的 2005 日历年。  
  
6.  单击 **“验证”** 。  
  
     请注意，此时将显示一条警告，指出某些列在源中不存在。 这是因为在[第3课：重命名列](rename-columns.md)时，在模型中将 Internet Sales 表中的这些列重命名为不同于源中相同列。  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>在 Internet Sales 表中创建2006年的分区  
  
1.  在 "**分区管理器**" 对话框的 "**分区**" 中，单击 `Internet Sales 2005` 刚创建的分区，然后**复制**。  
  
2.  在 "**分区名称**" 中，键入 `Internet Sales 2006` 。  
  
3.  在 SQL 语句中，要使分区只包含2006年的那些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>在 Internet Sales 表中创建2007年的分区  
  
1.  在“分区管理器”**** 对话框中，单击“复制”****。  
  
2.  在 "**分区名称**" 中，键入 `Internet Sales 2007` 。  
  
3.  在 "**切换到**" 中，选择 "**查询编辑器**"。  
  
4.  在 SQL 语句中，要使分区只包含2007年的那些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>在 Internet Sales 表中创建2008年的分区  
  
1.  在“分区管理器”**** 对话框中，单击“新建”****。  
  
2.  在 "**分区名称**" 中，键入 `Internet Sales 2008` 。  
  
3.  在 "**切换到**" 中，选择 "**查询编辑器**"。  
  
4.  在 SQL 语句中，要使分区只包含2008年的那些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>在 Internet Sales 表中为 2009 年份创建分区  
  
1.  在“分区管理器”**** 对话框中，单击“新建”****。  
  
2.  在 "**分区名称**" 中，键入 `Internet Sales 2009` 。  
  
3.  在 "**切换到**" 中，选择 "**查询编辑器**"。  
  
4.  在 SQL 语句中，要使分区只包含 2009 年份的这些行，请将 WHERE 子句替换为：  
  
    ```  
    WHERE (([OrderDate] >= N'2009-01-01 00:00:00') AND ([OrderDate] < N'2010-01-01 00:00:00'))  
    ```  
  
## <a name="process-partitions"></a>处理分区  
 在“分区管理器”**** 对话框中，请注意，对于刚才创建的每个新分区，分区名称旁边会有一个星号 (**\***)。 这指示尚未处理（刷新）分区。 当您创建新分区时，您应运行“处理分区”或“处理表”操作以刷新这些分区中的数据。  
  
#### <a name="to-process-internet-sales-partitions"></a>处理 Internet Sales 分区  
  
1.  单击“确定”**** 关闭“分区管理器”**** 对话框。  
  
2.  在模型设计器中，单击“Internet Sales”**** 表，然后单击“模型”**** 菜单，指向“处理”****（刷新），然后单击“处理分区”****。  
  
3.  在“处理分区”**** 对话框中，确认“模式”**** 已设置为“处理默认值”****。  
  
4.  选中创建的五个分区中每个分区的“处理”列中的复选框，并单击“确定”。********  
  
     如果系统提示您输入模拟凭据，则输入您在第 2 课的第 6 步中指定的 Windows 用户名和密码。  
  
     然后，将出现 "**数据处理**" 对话框，并显示每个分区的进程详细信息。 请注意，为每个分区传输的行数不同。 这是因为，每个分区值包含您在 SQL 语句的 WHERE 子句中指定的年份的那些行。 对于 2010 年份没有数据。  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课： [第 12 课：创建角色](lesson-11-create-roles.md)。  
  
  
