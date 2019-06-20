---
title: Analysis Services 教程第 10 课：创建分区 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 91b0fb17ae785098e54358132daa91c04c7f3e5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148962"
---
# <a name="create-partitions"></a>创建分区

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你创建分区来将 FactInternetSales 表划分为较小的逻辑部分，可以处理 （刷新） 独立于其他分区。 默认情况下，在模型中包括的每个表具有一个分区，其中包括所有表的列和行。 对于 FactInternetSales 表中，我们想要将数据划分按年份;为每个表的五年的一个分区。 然后，每个分区可独立进行处理。 若要了解详细信息，请参阅[分区](../tabular-models/partitions-ssas-tabular.md)。 
  
估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 9 课：创建层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>创建分区  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>若要在 FactInternetSales 表中创建分区  
  
1.  在表格模型资源管理器，展开**表**，然后右键单击**FactInternetSales** > **分区**。  
  
2.  在分区管理器中，单击**副本**，然后将更改为名称**FactInternetSales2010**。
  
    由于您希望分区只包含这些行在一段时间，为 2010 年，您必须修改查询表达式。
  
4.  单击**设计**以打开查询编辑器中，然后单击**FactInternetSales2010**查询。

5.  在预览版中，单击中的向下箭头**OrderDate**列标题，然后单击**日期/时间筛选器** > **之间**。

    ![as-lesson10-query-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  在筛选行对话框中，在**显示行，其中：OrderDate**，保留**是晚于或等于**，然后在日期字段中，输入**2010 年 1 月 1 日**。 将保留**并**运算符选择，然后选择**早**，然后在日期字段中，输入**2011 年 1 月 1 日**，然后单击**确定**。

    ![as-lesson10-filter-rows](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    请注意，在查询编辑器中，在应用的步骤，你将看到名为筛选的行的另一个步骤。 此筛选器是仅选择订单日期 2010 年。

8.  单击“导入” 。

    在分区管理器中，请注意，查询表达式现在具有附加的 Filtered Rows 子句。

    ![as-lesson10-query](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    此语句指定此分区应只包含的数据行，orderdate 对应处于 filtered 的 rows 子句中指定的 2010年日历年中的位置。  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>为 2011 年份创建分区  
  
1.  在分区列表中，单击**FactInternetSales2010**分区所创建的然后依次**副本**。  将分区名称更改为**FactInternetSales2011**。 

    不需要使用查询编辑器创建新的 filtered 的 rows 子句。 由于为 2010年创建查询的副本，您需要做是 2011 年在查询中进行了细微的改动。
  
2.  在**查询表达式**中，为了使此分区包含 2011 年份的那些行，将为与 Filtered Rows 子句中的年份**2011年**并**2012年**，分别所示：  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>若要为 2012年、 2013年和 2014年中创建分区。  
  
- 按照前面的步骤，为 2012年、 2013年和 2014 年更改 Filtered Rows 子句来只包含该年的行中的年份创建分区。 
  

## <a name="delete-the-factinternetsales-partition"></a>删除 FactInternetSales 分区

现在，每年的已分区，可以删除 FactInternetSales 分区;处理分区时选择所有的进程时阻止重叠。

#### <a name="to-delete-the-factinternetsales-partition"></a>若要删除 FactInternetSales 分区

-  单击**FactInternetSales**分区，然后依次**删除**。



## <a name="process-partitions"></a>处理分区  

请注意，在分区管理器中，**最后一个处理**列对于每个新分区创建显示这些分区从未处理。 在创建分区时，应运行在处理分区或处理表操作以刷新这些分区中的数据。  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>处理 FactInternetSales 分区  
  
1.  单击**确定**以关闭分区管理器。  
  
2.  单击**FactInternetSales**表，然后单击**模型**菜单 >**过程** > **处理分区**。  
  
3.  在处理分区对话框中，验证是否**模式下**设置为**处理默认值**。  
  
4.  在“处理”列中选中所创建的全部五个分区的复选框，然后单击“确定”。  

    ![as-lesson10-process-partitions](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    如果系统提示输入模拟凭据，则输入 Windows 用户名和第 2 课中指定的密码。  
  
    “数据处理”对话框将出现，并显示每个分区的处理详细信息。 您将注意到对于每个分区转移了不同的行数。 每个分区包括 SQL 语句中的 WHERE 子句中指定的年份的那些行。 完成处理后，继续操作并关闭“数据处理”对话框。  
  
    ![as-lesson10-process-complete](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>下一步是什么？

请转到下一课：[第 11 课：创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。 
