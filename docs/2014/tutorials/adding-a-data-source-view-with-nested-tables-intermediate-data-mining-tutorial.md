---
title: 添加具有嵌套表的数据源视图（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62822771"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>添加带有嵌套表的数据源视图（数据挖掘中级教程）
  要创建市场篮模型，您必须使用支持关联数据的数据源视图。 该数据源视图还将用于顺序分析和聚类分析方案。  
  
 此数据源视图不同于你可能使用的其他数据源视图，因为它包含*嵌套表*。 *嵌套表*是一个表，其中包含有关事例表中单个行的多个行信息。 例如，如果您的模型分析客户的购买行为，您通常会使用对于每个客户都包含一个唯一行的表作为事例表。 但是，每个客户都可能有多个购买行为，您可能希望分析购买的顺序或者经常一起购买的产品。 若要在您的模型中以逻辑方式表示这些购买行为，您需要在该数据源视图中添加另一个表来列出每个客户的购买行为。  
  
 该嵌套购买表与客户表具有多对一的关系。 该嵌套表可能包含对应每个客户的多个行，每个行包含已购买的单件产品，还可能包含有关购买顺序、订购时的价格或任何促销手段等其他信息。 您可以使用嵌套表中的信息作为模型的输入，或者作为可预测属性。  
  
 在本课程中，您将执行以下任务：  
  
-   您可以向[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]数据源中添加数据源视图。  
  
-   将事例表和嵌套表添加到此视图中。  
  
-   在事例表和嵌套表之间指定多对一关系。  
  
    > [!NOTE]  
    >  . 按照所述步骤执行很重要，这样可以正确指定事例表和嵌套表之间的关系，并且可以避免在处理模型时出现错误。  
  
-   定义如何在模型中使用数据列。  
  
 有关使用事例表和嵌套表以及如何选择嵌套表键的详细信息，请参阅[&#40;Analysis Services 数据挖掘&#41;的嵌套表](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)。  
  
### <a name="to-add-a-data-source-view"></a>添加数据源视图  
  
1.  在解决方案资源管理器中，右键单击 "**数据源视图**"，然后选择 "**新建数据源视图**"。  
  
     系统将打开数据源视图向导。  
  
2.  在“欢迎使用数据源视图向导”**** 页上，单击“下一步”****。  
  
3.  在 "**选择数据源**" 页的 "**关系数据源**" 下， [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]选择在基础数据挖掘教程中创建的数据源。 单击 **下一步**。  
  
4.  在 "**选择表和视图**" 页上，选择下表，然后单击右箭头将它们包含在新的数据源视图中：  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  单击 **下一步**。  
  
6.  在 "**完成向导**" 页上，默认将数据源视图命名为[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。 将名称更改为`Orders`，然后单击 "**完成**"。  
  
     数据源视图设计器随即打开`Orders` ，并显示数据源视图。  
  
### <a name="to-create-a-relationship-between-tables"></a>创建表之间的关系  
  
1.  在数据源视图设计器中，定位 vAssocSeqLineItems 表和 vAssocSeqOrders 表，使其水平对齐，并且 vAssocSeqLineItems 表在左，vAssocSeqOrders 表在右。  
  
2.  选择 vAssocSeqLineItems 表中的**OrderNumber**列。  
  
3.  将该列拖到 "vAssocSeqOrders" 表中，并将其放到 " **OrderNumber** " 列。  
  
    > [!IMPORTANT]  
    >  请确保将**OrderNumber**列从 vAssocSeqLineItems 嵌套表中拖出，后者表示联接的多方，后者表示联接的一方。  
  
     VAssocSeqLineItems 表和 vAssocSeqOrders 表之间现在存在新的*多对一关系*。 如果您已正确联接表，则数据源视图应如下所示：  
  
     ![嵌套表和事例表之间需要的多对一联接](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "嵌套表和事例表之间需要的多对一联接")  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建市场篮结构和模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [中级数据挖掘教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [挖掘结构 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [挖掘模型（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
