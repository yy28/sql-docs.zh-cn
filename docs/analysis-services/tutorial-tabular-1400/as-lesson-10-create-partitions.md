---
title: Analysis Services 教程课 10： 创建分区 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: 8dc8e91271451d3f24df95846f32af8dbd9ca346
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="create-partitions"></a>创建分区

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你创建分区将 FactInternetSales 表划分为较小可处理的逻辑部分 （刷新） 独立于其他分区。 默认情况下，在模型中包括每个表具有一个分区，其中包括所有表的列和行。 对于 FactInternetSales 表中，我们想要将数据划分按年;每个表的五年的一个分区。 然后，每个分区可独立进行处理。 若要了解详细信息，请参阅[分区](../tabular-models/partitions-ssas-tabular.md)。 
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课： [Lesson 9： 创建层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>创建分区  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>在 FactInternetSales 表中创建分区  
  
1.  在表格模型资源管理器，展开**表**，然后右键单击**FactInternetSales** > **分区**。  
  
2.  在分区管理器中，单击**复制**，然后将更改该名称与**FactInternetSales2010**。
  
    由于你想要包括在某个段，在一年 2010 中，只有这些行的分区必须修改的查询表达式。
  
4.  单击**设计**以打开查询编辑器中，然后单击**FactInternetSales2010**查询。

5.  在预览版中，单击中的向下箭头**OrderDate**列标题，然后单击**日期/时间筛选器** > **之间**。

    ![as-lesson10-query-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  在筛选行对话框中，在**显示行： OrderDate**，保留**是晚于或等于**，然后在日期字段中，输入**1/1/2010年**。 保留**和**运算符选择，然后选择**早**，然后在日期字段中，输入**2011 年 1 月 1 日**，然后单击**确定**。

    ![作为 lesson10-筛选器的行](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    请注意在查询编辑器中，在应用步骤中，你将看到另一个名为筛选行的步骤。 此筛选器是从 2010年选择仅订单日期。

8.  单击“导入” 。

    在分区管理器中，请注意现在的查询表达式具有其他行筛选子句。

    ![为 lesson10 查询](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    此语句指定此分区应只包括数据 OrderDate 处于 2010年日历年在行筛选的子句中指定这些行中。  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>为 2011 年份创建分区  
  
1.  在分区列表中，单击**FactInternetSales2010**分区所创建的并依次**复制**。  分区名称更改为**FactInternetSales2011**。 

    不需要使用查询编辑器来创建新的筛选的行子句。 因为你为 2010年创建一份查询，你需要做是 2011 在查询中进行细微更改。
  
2.  在**查询表达式**、 顺序为 2011 年包括仅这些行，将使用筛选行子句中的年此分区的**2011年**和**2012年**分别，如：  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>若要为 2012年、 2013年和 2014年创建分区。  
  
- 按照前面的步骤，为 2012年、 2013年和 2014，更改筛选行子句，以包含仅行，为该年中的年创建分区。 
  

## <a name="delete-the-factinternetsales-partition"></a>删除 FactInternetSales 分区

现在，每年已分区，可以删除 FactInternetSales 分区中;处理分区时选择所有的过程时，请阻止重叠。

#### <a name="to-delete-the-factinternetsales-partition"></a>要删除 FactInternetSales 分区

-  单击**FactInternetSales**分区，并依次**删除**。



## <a name="process-partitions"></a>处理分区  

在分区管理器中，请注意**最后一个处理**列对于每个新分区创建显示永远不会处理这些分区。 当创建分区时，应运行处理分区或处理表操作，以刷新这些分区中的数据。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>处理 FactInternetSales 分区  
  
1.  单击**确定**若要关闭分区管理器。  
  
2.  单击**FactInternetSales**表，然后单击**模型**菜单 >**过程** > **处理分区**。  
  
3.  在处理分区对话框中，验证**模式**设置为**处理默认值**。  
  
4.  在“处理”列中选中所创建的全部五个分区的复选框，然后单击“确定”。  

    ![作为-lesson10-处理的分区](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    如果系统提示输入模拟凭据，则输入 Windows 用户名称和你在第 2 课中指定的密码。  
  
    “数据处理”对话框将出现，并显示每个分区的处理详细信息。 您将注意到对于每个分区转移了不同的行数。 每个分区的 SQL 语句中的 WHERE 子句中指定的年包括仅这些行。 完成处理后，继续操作并关闭“数据处理”对话框。  
  
    ![作为 lesson10-过程-完成](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步是什么？

转到下一课：[课 11： 创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。 
