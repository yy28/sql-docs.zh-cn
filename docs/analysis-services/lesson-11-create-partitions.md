---
title: "第 11 课：创建分区 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 11 课：创建分区
在本课中，您将创建分区，以便将 Internet Sales 表划分为可独立于其他分区进行处理（刷新）的更小逻辑部分。 默认情况下，您包括在模型中的每个表都具有一个包含表的所有列和行的分区。 对于 Internet Sales 表，我们希望按年份划分数据；一个分区对应于表中的每个五年。  然后，每个分区可独立进行处理。 若要了解详细信息，请参阅[分区（SSAS 表格）](../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
学完本课的估计时间：**15 分钟**  
  
## 先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课：[第 10 课：创建层次结构](../analysis-services/lesson-10-create-hierarchies.md)。  
  
## 创建分区  
  
#### 在 Internet Sales 表中创建分区  
  
1.  在模型设计器中，依次单击“Internet Sales”表、“表”菜单和“分区”。  
  
    “分区管理器”对话框将打开。  
  
2.  在“分区管理器”对话框的“分区”列表中，单击“Internet Sales”分区。  
  
3.  在“分区名称”中，将名称更改为 **Internet Sales 2010**。  
  
    > [!TIP]  
    > 在继续执行下一步之前，您将注意到“表预览”窗口中的列名显示模型表中包含的、但其列名来自源中的这些列（已勾选）。 这是因为“表预览”窗口显示源表（而非模型表）中的列。  
  
4.  选择位于预览窗口右侧上方的“查询编辑器”按钮。  
  
    因为您希望分区只包含特定期间内的那些行，所以您必须包含 WHERE 子句。 您只能通过使用 SQL 语句创建 WHERE 子句。  
  
5.  在“SQL 语句”字段中，通过粘贴以下语句替换现有语句：  
  
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
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    此语句指定分区应包含以下行中的所有数据：对于这些行，OrderDate 对应于在 WHERE 子句中指定的 2010 日历年。  
  
6.  单击 **“验证”**。  
  
  
#### 为 2011 年份创建分区  
  
1.  在“分区”列表中，单击刚才创建的“Internet Sales 2010”分区，然后单击“复制”。  
  
2.  在“分区名称”中，键入 **Internet Sales 2011**。  
  
3.  在 SQL 语句中，要使分区只包含 2011 年份的这些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### 为 2012 年份创建分区  
  
1.  在“分区管理器”对话框中，单击“复制”。  
  
2.  在“分区名称”中，键入 **Internet Sales 2012**。  
  
3.  在 SQL 语句中，要使分区只包含 2012 年份的这些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### 为 2013 年份创建分区  
  
1.  在“分区管理器”对话框中，单击“新建”。  
  
2.  在“分区名称”中，键入 **Internet Sales 2013**。  
  
3.  在 SQL 语句中，要使分区只包含 2013 年份的这些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### 在“Internet Sales”表中为 2014 年份创建分区  
  
1.  在“分区管理器”对话框中，单击“新建”。  
  
2.  在“分区名称”中，键入 **Internet Sales 2014**。  
  
3.  在 SQL 语句中，要使分区只包含 2014 年份的这些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  
  
## 处理分区  
在“分区管理器”对话框中，请注意，对于刚才创建的每个新分区，分区名称旁边会有一个星号 (**\***)。 这指示尚未处理（刷新）分区。 当您创建新分区时，您应运行“处理分区”或“处理表”操作以刷新这些分区中的数据。  
  
#### 处理 Internet Sales 分区  
  
1.  单击“确定”关闭“分区管理器”对话框。  
  
2.  在模型设计器中，单击“Internet Sales”表，然后单击“模型”菜单，指向“处理”（刷新），然后单击“处理分区”。  
  
3.  在“处理分区”对话框中，确认“模式”已设置为“处理默认值”。  
  
4.  在“处理”列中选中所创建的全部五个分区的复选框，然后单击“确定”。  
  
    如果系统提示您输入模拟凭据，则输入您在第 2 课的第 6 步中指定的 Windows 用户名和密码。  
  
    “数据处理”对话框将出现，并显示每个分区的处理详细信息。 您将注意到对于每个分区转移了不同的行数。 这是因为，每个分区值包含您在 SQL 语句的 WHERE 子句中指定的年份的那些行。 完成处理后，继续操作并关闭“数据处理”对话框。  
  
  
  
## 后续步骤  
若要继续学习本教程，请转到下一课：[第 12 课：创建角色](../analysis-services/lesson-12-create-roles.md)。  
  
  
  
