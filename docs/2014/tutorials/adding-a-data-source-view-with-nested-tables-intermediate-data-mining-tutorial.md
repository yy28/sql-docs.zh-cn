---
title: 添加数据源视图使用嵌套表 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70db9a9ff6ed8aa5c9a960ae40009369341b99b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068037"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>添加带有嵌套表的数据源视图（数据挖掘中级教程）
  要创建市场篮模型，您必须使用支持关联数据的数据源视图。 该数据源视图还将用于顺序分析和聚类分析方案。  
  
 此数据源视图是不同于你可能已经处理的因为它包含的其他人*嵌套的表*。 一个*嵌套的表*是包含有关事例表中单个行的信息的多个行的表。 例如，如果您的模型分析客户的购买行为，您通常会使用对于每个客户都包含一个唯一行的表作为事例表。 但是，每个客户都可能有多个购买行为，您可能希望分析购买的顺序或者经常一起购买的产品。 若要在您的模型中以逻辑方式表示这些购买行为，您需要在该数据源视图中添加另一个表来列出每个客户的购买行为。  
  
 该嵌套购买表与客户表具有多对一的关系。 该嵌套表可能包含对应每个客户的多个行，每个行包含已购买的单件产品，还可能包含有关购买顺序、订购时的价格或任何促销手段等其他信息。 您可以使用嵌套表中的信息作为模型的输入，或者作为可预测属性。  
  
 在本课程中，您将执行以下任务：  
  
-   添加到数据源视图[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]数据源。  
  
-   将事例表和嵌套表添加到此视图中。  
  
-   在事例表和嵌套表之间指定多对一关系。  
  
    > [!NOTE]  
    >  . 按照所述步骤执行很重要，这样可以正确指定事例表和嵌套表之间的关系，并且可以避免在处理模型时出现错误。  
  
-   定义如何在模型中使用数据列。  
  
 了解如何使用用例和嵌套的表，以及如何选择嵌套的表键的详细信息，请参阅[嵌套表&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)。  
  
### <a name="to-add-a-data-source-view"></a>添加数据源视图  
  
1.  在解决方案资源管理器中右键单击**数据源视图**，然后选择**新数据源视图**。  
  
     系统将打开数据源视图向导。  
  
2.  在“欢迎使用数据源视图向导”页中，单击“下一步”。  
  
3.  上**选择数据源**页面上，在**关系数据源**，选择[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]在数据挖掘基础教程中创建的数据源。 单击“下一步” 。  
  
4.  上**选择表和视图**页上，选择以下表，然后单击右箭头以将其包含在新的数据源视图：  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  单击“下一步” 。  
  
6.  上**完成向导**页上，默认情况下，数据源视图命名为[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。 将名称更改为`Orders`，然后单击**完成**。  
  
     打开数据源视图设计器和`Orders`数据源视图将显示。  
  
### <a name="to-create-a-relationship-between-tables"></a>若要创建表之间的关系  
  
1.  在数据源视图设计器中，定位 vAssocSeqLineItems 表和 vAssocSeqOrders 表，使其水平对齐，并且 vAssocSeqLineItems 表在左，vAssocSeqOrders 表在右。  
  
2.  选择**OrderNumber** vAssocSeqLineItems 表中的列。  
  
3.  将列拖到 vAssocSeqOrders 表，并将其放**OrderNumber**列。  
  
    > [!IMPORTANT]  
    >  请确保要拖动**OrderNumber**列从 vAssocSeqLineItems 嵌套表，前者代表联接的多方 vAssocSeqOrders 事例表，前者代表联接的一方。  
  
     一个新*多对一的关系*vAssocSeqLineItems 和 vAssocSeqOrders 表之间现在存在。 如果您已正确联接表，则数据源视图应如下所示：  
  
     ![对嵌套和事例表的预期的多对一联接](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "嵌套和事例表的预期的多对一联接")  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建市场篮结构和模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘中级教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [挖掘结构&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [挖掘模型&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
