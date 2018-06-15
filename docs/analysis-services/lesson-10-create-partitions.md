---
title: 第 11 课： 创建分区 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d738649ea357b172975505ff7993b56181ce0b4f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34018754"
---
# <a name="lesson-10-create-partitions"></a>第 10 课： 创建分区
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程中，你将创建独立于其他分区将 FactInternetSales 表划分为较小可处理的逻辑部分 （刷新） 的分区。 默认情况下，您包括在模型中的每个表都具有一个包含表的所有列和行的分区。 对于 FactInternetSales 表中，我们想要将数据划分按年;每个表的五年的一个分区。 然后，每个分区可独立进行处理。 若要了解详细信息，请参阅[分区](../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课： [Lesson 9： 创建层次结构](../analysis-services/lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>创建分区  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>在 FactInternetSales 表中创建分区  
  
1.  在表格模型资源管理器，展开**表**，右键单击**FactInternetSales** > **分区**。  
  
2.  在分区管理器对话框中，单击**复制**。  
  
3.  在**分区名称**，名称更改为**FactInternetSales2010**。  
  
    > [!TIP]  
    > 请注意显示 （已选中） 与源中的列名称的模型表中包含这些列的表预览窗口中的列名称。 这是因为“表预览”窗口显示源表（而非模型表）中的列。  
  
4.  选择**SQL**正上方的预览窗口以打开 SQL 语句编辑器右侧的按钮。  
  
    因为您希望分区只包含特定期间内的那些行，所以您必须包含 WHERE 子句。 您只能通过使用 SQL 语句创建 WHERE 子句。  
  
5.  在**SQL 语句**字段中，通过复制并粘贴以下语句替换现有语句：  
  
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
  
1.  在分区列表中，单击**FactInternetSales2010**分区你刚刚创建，并依次**复制**。  
  
2.  在**分区名称**，类型**FactInternetSales2011**。  
  
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
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>若要创建为 2014 年的分区  
  
- 按照上面的步骤，使用以下 WHERE 子句。 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>删除 FactInternetSales 分区
现在，每年已分区，你可以删除 FactInternetSales 分区。 这样可防止重叠时处理分区时选择所有的过程。
#### <a name="to-delete-the-factinternetsales-partition"></a>要删除 FactInternetSales 分区
-  单击 FactInternetSales 分区，然后单击**删除**。



## <a name="process-partitions"></a>处理分区  
在分区管理器中，请注意**最后一个处理**为每个新的列分区只需创建的显示永远不会处理这些分区。 当您创建新分区时，您应运行“处理分区”或“处理表”操作以刷新这些分区中的数据。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>处理 FactInternetSales 分区  
  
1.  单击**确定**以关闭分区管理器对话框。  
  
2.  单击**FactInternetSales**表，然后单击**模型**菜单 >**过程** > **处理分区**。  
  
3.  在处理分区对话框中，验证**模式**设置为**处理默认值**。  
  
4.  在“处理”列中选中所创建的全部五个分区的复选框，然后单击“确定”。  

    ![作为-表格-lesson10-处理的分区](../analysis-services/media/as-tabular-lesson10-process-partitions.png)
  
    如果系统提示输入模拟凭据，则输入 Windows 用户名称和你在第 2 课中指定的密码。  
  
    “数据处理”对话框将出现，并显示每个分区的处理详细信息。 您将注意到对于每个分区转移了不同的行数。 这是因为，每个分区值包含您在 SQL 语句的 WHERE 子句中指定的年份的那些行。 完成处理后，继续操作并关闭“数据处理”对话框。  
  
    ![作为表格-lesson10-过程-完成](../analysis-services/media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步是什么？
转到下一课：[课 11： 创建角色](../analysis-services/lesson-11-create-roles.md)。 
