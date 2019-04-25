---
title: 第 10 课：创建分区 |Microsoft Docs
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d43432a53eb2321c3707f4034e244752a5c368ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468638"
---
# <a name="lesson-10-create-partitions"></a>第 10 课：创建分区
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程中，将创建独立于其他分区来将 FactInternetSales 表划分为较小的逻辑部分，可以处理 （刷新） 分区。 默认情况下，在模型中包括的每个表具有一个分区，其中包括所有表的列和行。 对于 FactInternetSales 表中，我们想要将数据划分按年份;为每个表的五年的一个分区。 然后，每个分区可独立进行处理。 若要了解详细信息，请参阅[分区](../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 9 课：创建层次结构](../analysis-services/lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>创建分区  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建分区  
  
1.  在表格模型资源管理器，展开**表**，右键单击**FactInternetSales** > **分区**。  
  
2.  在分区管理器对话框中，单击**复制**。  
  
3.  在中**分区名称**，将名称更改为**FactInternetSales2010**。  
  
    > [!TIP]  
    > 请注意，显示使用源中的列名称 （检查） 的模型表中包含这些列的表预览窗口中的列名称。 这是因为“表预览”窗口显示源表（而非模型表）中的列。  
  
4.  选择**SQL**正上方的预览窗口以打开 SQL 语句编辑器右侧的按钮。  
  
    因为您希望分区只包含特定期间内的那些行，所以您必须包含 WHERE 子句。 您只能通过使用 SQL 语句创建 WHERE 子句。  
  
5.  在中**SQL 语句**字段中，通过复制并粘贴以下语句替换现有语句：  
  
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
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>为 2011 年份创建分区  
  
1.  在分区列表中，单击**FactInternetSales2010**分区你刚刚创建，然后依次**副本**。  
  
2.  在中**分区名称**，类型**FactInternetSales2011**。  
  
3.  在 SQL 语句中，要使分区只包含 2011 年份的这些行，请将 WHERE 子句替换为以下内容：  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2012-year"></a>为 2012 年份创建分区  
  
- 按照上面的步骤，使用以下 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2013-year"></a>为 2013 年份创建分区  
  
- 按照上面的步骤，使用以下 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>若要为 2014 年份创建分区  
  
- 按照上面的步骤，使用以下 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>删除 FactInternetSales 分区
现在，每年的已分区，可以删除 FactInternetSales 分区。 处理分区时选择所有过程时，这可以防止重叠。
#### <a name="to-delete-the-factinternetsales-partition"></a>若要删除 FactInternetSales 分区
-  单击 FactInternetSales 分区，然后单击**删除**。



## <a name="process-partitions"></a>处理分区  
请注意，在分区管理器中，**最后一个处理**列对于每个新的分区只需创建这些分区从未处理的显示。 当您创建新分区时，您应运行“处理分区”或“处理表”操作以刷新这些分区中的数据。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>处理 FactInternetSales 分区  
  
1.  单击**确定**以关闭分区管理器对话框。  
  
2.  单击**FactInternetSales**表，然后单击**模型**菜单 >**过程** > **处理分区**。  
  
3.  在处理分区对话框中，验证是否**模式下**设置为**处理默认值**。  
  
4.  在“处理”列中选中所创建的全部五个分区的复选框，然后单击“确定”。  

    ![as-tabular-lesson10-process-partitions](../analysis-services/media/as-tabular-lesson10-process-partitions.png)
  
    如果系统提示输入模拟凭据，则输入 Windows 用户名和第 2 课中指定的密码。  
  
    “数据处理”对话框将出现，并显示每个分区的处理详细信息。 您将注意到对于每个分区转移了不同的行数。 这是因为，每个分区值包含您在 SQL 语句的 WHERE 子句中指定的年份的那些行。 完成处理后，继续操作并关闭“数据处理”对话框。  
  
    ![as-tabular-lesson10-process-complete](../analysis-services/media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 11 课：创建角色](../analysis-services/lesson-11-create-roles.md)。 
