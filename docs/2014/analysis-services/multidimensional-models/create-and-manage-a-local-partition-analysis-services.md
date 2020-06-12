---
title: 创建和管理本地分区（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- local partitions [Analysis Services]
- partitions [Analysis Services], local
- partitions [Analysis Services], creating
ms.assetid: eaa95278-9ce9-47d5-a6b6-1046e7076599
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7251f9e9422a79c214d27d913112a28ff43d56b1
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536207"
---
# <a name="create-and-manage-a-local-partition-analysis-services"></a>创建和管理本地分区 (Analysis Services)
  您可以为度量值组创建更多分区以提高处理性能。 通过多个分区，您可以跨本地以及远程服务器上对应数目的物理数据文件分配事实数据。 在 Analysis Services 中，可以独立和并行处理分区，从而可更好地控制服务器上的处理工作负荷。

 可以在模型设计期间在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中创建分区，或在部署解决方案后使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 XMLA 来创建分区。 建议您仅选择一种方法。 如果您交替使用这些工具，可能会发现，在随后从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 重新部署该解决方案时，在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中对已部署的数据库所进行的更改将被覆盖。

## <a name="before-you-start"></a>开始之前
 检查所用版本是否为 Business Intelligence 或 Enterprise。 Standard 版不支持多个分区。 若要检查版本，请在中右键单击服务器节点， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 然后选择 "**报表**" "  |  **常规**"。 有关功能可用性的详细信息，请参阅[SQL Server 2014 的各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。

 如果您想以后将分区合并，则从一开始就须知道各分区必须具有相同的聚合设计。 仅当分区具有相同的聚合设计和存储模式时，才能将分区合并。

> [!TIP]
>  浏览数据源视图 (DSV) 中的数据以了解要进行分区的数据的范围和深度。 例如，如果按日期进行分区，则可以对日期列进行排序以确定每个分区的上限和下限。

## <a name="choose-an-approach"></a>选择方法
 创建分区时的最重要问题是将数据分段，以便消除重复的行。 必须将数据存储在一个（仅一个）分区中以避免对任何行双重计数。 因此，通常按“日期”进行分区，这样就可以定义各分区间的清晰边界。

 您可以通过两种方法之一跨多个分区分配事实数据。 以下方法可用于将数据分段。

|方法|建议|
|---------------|---------------------|
|使用 SQL 查询将事实数据分段|分区可以来源于 SQL 查询。 处理期间，SQL 查询将会检索数据。 该查询的 WHERE 子句提供了对每个分区的数据进行分段的筛选器。 Analysis Services 自动生成查询，但是您必须填入 WHERE 子句以便正确对数据分段。<br /><br /> 这种方法的主要优点是可以方便地对单个源表的数据进行分区。 如果所有源数据都源自一个大型事实数据表，则您可以生成查询以将该数据筛选到不同分区中，而不必在数据源视图 (DSV) 中创建其他数据结构。<br /><br /> 此方法的一个缺点是使用查询会中断分区与 DSV 之间的绑定。 如果您随后在 Analysis Services 项目中更新 DSV（例如，向该事实数据表添加列），则必须手动为每个分区编辑这些查询以包括进新列。 接下来讨论的第二种方法没有这个缺点。|
|使用 DSV 中的表将事实数据分段|可以将分区绑定到 DSV 中的表、命名查询或视图。 作为分区的基础，所有这三项在功能上是等效的。 整个表、命名查询或视图都向单一分区提供所有数据。<br /><br /> 使用表、视图或命名查询会在 DSV 中放置所有数据选择逻辑，随着时间的推移更便于管理和维护。 此方法的一个重要优点是会保留表绑定。 如果随后对源表进行更新，则不必修改使用该源表的分区。 其次，所有表、命名查询和视图都位于一个公共工作区中，这就使更新更加方便，不必单独打开并编辑分区查询。|

## <a name="option-1-filter-a-fact-table-for-multiple-partitions"></a>方法 1：筛选多个分区的事实数据表
 若要创建多个分区，首先要修改默认分区的 **“源”** 属性。 默认情况下，将使用绑定到 DSV 中单个表的单个分区来创建度量值组。 在添加更多分区之前，必须首先修改原始分区以仅包含一部分事实数据。 随后可以继续创建其他分区以存储其余数据。

 对筛选器进行构造，使得数据不会在各分区中重复。 分区的筛选指定事实数据表中哪些数据应用于分区。 多维数据集中对于所有分区的筛选必须从事实数据表中提取互斥的数据集。 如果同一事实数据出现在多个分区中，则可能会对该事实数据双重计数。

1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中的解决方案资源管理器中，双击该多维数据集以在多维数据集设计器中将其打开，然后单击“分区”选项卡。****

2.  展开要添加分区的度量值组。 默认情况下，每个度量值组具有一个分区，此分区绑定到 DSV 中的事实数据表。

3.  在“源”列中，单击浏览 ( .) 按钮打开“分区源”对话框。

     ![“分区”窗格中的源列](../media/ssas-partitionsource.png "“分区”窗格中的源列")

4.  在“绑定类型”中，选择 **“查询绑定”**。 将自动显示用于选择数据的 SQL 查询。

5.  在底部的 WHERE 子句中，添加用于将此分区的数据分段的筛选器。

     WHERE 子句语法的示例如 `WHERE OrderDateKey >= '20060101'` 或 `WHERE OrderDateKey BETWEEN '20051001' AND '20051201'`。 有关其他示例，请参阅 [WHERE (Transact-SQL)](/sql/t-sql/queries/where-transact-sql)。

     请注意，下列筛选器在每个集合内是互斥的：

    |||
    |-|-|
    |第 1 集合：|"SaleYear" = 2012<br /><br /> "SaleYear" = 2013|
    |第 2 集合：|"Continent" = 'NorthAmerica'<br /><br /> "Continent" = 'Europe'<br /><br /> "Continent" = 'SouthAmerica'|
    |第 3 集合：|"Country" = 'USA'<br /><br /> "Country" = 'Mexico'<br /><br /> ("Country" <> 'USA' AND "Country" <> 'Mexico')|

6.  单击 **“检查”** 检查语法错误，然后单击 **“确定”**。

7.  重复前面的步骤以创建其余分区，每次修改 WHERE 子句都选择下一个数据切片。

8.  部署解决方案或对分区进行处理以加载数据。 请确保处理所有分区。

9. 浏览该多维数据集以验证是否返回了正确的数据。

 在您拥有一个使用多个度量值组的度量值组后，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中创建其他分区。 在一个度量值组下，右键单击“分区”文件夹，然后选择“新建分区”以启动向导。****

> [!NOTE]
>  您无需筛选分区中的数据，而是可以使用同一查询在 DSV 中创建命名查询，然后使分区基于该命名查询。

## <a name="option-2-use-tables-views-or-named-queries"></a>方法 2：使用表、视图或命名查询
 如果 DSV 以将事实数据组织到各个表中（例如，按年或按季度），则您可以基于某个表来创建分区，其中每个分区都具有自己的数据源表。 这基本上是对度量值组默认进行分区的方式，但是在具有多个分区时，您需要将原始分区细分为多个分区，并将每个新的分区映射到提供数据的数据源表。

 视图和命名查询在功能上与表是等效的，原因是所有三个对象都在 DSV 中进行定义，并使用“分区源”对话框中的“表绑定”选项绑定到分区。 您可以创建视图或命名查询以生成每个分区所需的数据段。 有关详细信息，请参阅[在数据源视图中定义命名查询 (Analysis Services)](define-named-queries-in-a-data-source-view-analysis-services.md)。

> [!IMPORTANT]
>  在 DSV 中手动为分区创建互斥的命名查询时，请确保分区的组合数据包含您希望包括在多维数据集中的度量值组中的所有数据。 请确保没有让默认分区基于该度量值组的整个表，否则，基于该查询的分区将会与基于完整表的查询有重叠部分。

1.  创建一个或多个命名查询以用作分区源。 有关详细信息，请参阅[在数据源视图中定义命名查询 (Analysis Services)](define-named-queries-in-a-data-source-view-analysis-services.md)。

     该命名查询必须基于与该度量值组关联的事实数据表。 例如，如果对 FactInternetSales 度量值组进行分区，则 DSV 中的命名查询必须在 FROM 语句中指定 FactInternetSales 表。

2.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中的解决方案资源管理器中，双击该多维数据集以在多维数据集设计器中将其打开，然后单击“分区”选项卡。****

3.  展开要添加分区的度量值组。

4.  单击 **“新建分区”** 以启动分区向导。 如果您使用绑定到该度量值组的事实数据表创建了命名查询，则应看到在上一步骤中创建的每个命名查询。

5.  在“指定源信息”中，选择在上一步骤中创建的一个命名查询。 如果您没有看到任何命名查询，则返回到 DSV，然后检查 FROM 语句。

6.  单击 **“下一步”** 接受每个后续页的默认值。

7.  在最后的“完成向导”页上，为分区提供一个描述性名称。

8.  单击“完成”。

9. 重复前面的步骤以创建其余分区，每次选择不同的命名查询以选择下一个数据切片。

10. 部署解决方案或对分区进行处理以加载数据。 请确保处理所有分区。

11. 浏览该多维数据集以验证是否返回了正确的数据。

## <a name="next-step"></a>后续步骤
 在为分区创建互斥查询时，应确保组合分区数据包含需要多维数据集包含的所有数据。

 在最后一个步骤中，通常需要删除基于表本身的默认分区（如果该分区仍存在），否则基于分区的查询将与基于完整表的查询重叠。

## <a name="see-also"></a>另请参阅
 [分区 &#40;Analysis Services 多维数据&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md) [远程分区](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)[在 ANALYSIS SERVICES 中合并分区 &#40;SSAS-多维&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)


