---
title: "数据类型 （数据挖掘） |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
caps.latest.revision: 47
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8caea228dd0ddd646c90b7e5661a8d4fd2b4a722
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="data-types-data-mining"></a>数据类型（数据挖掘）
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中创建挖掘模型或挖掘结构时，必须为挖掘结构中的每一列定义数据类型。 数据类型告知分析引擎数据源中的数据是数值还是文本以及应如何处理数据。 例如，如果数据源中包含数值数据，则可以指定是将数字作为整数处理还是使用小数位数来处理。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持挖掘结构列的以下数据类型：  
  
|数据类型|支持的内容类型|  
|---------------|-----------------------------|  
|**Text**|Cyclical、Discrete、Discretized、Key Sequence、Ordered 和 Sequence|  
|**Long**|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence 和 Time<br /><br /> Classified|  
|**Boolean**|Cyclical、Discrete 和 Ordered|  
|**双精度**|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence 和 Time<br /><br /> Classified|  
|**日期**|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time 和 Ordered|  
  
> [!NOTE]  
>  只有第三方算法支持 Time 和 Sequence 内容类型。 支持 Cyclical 和 Ordered 内容类型，但大多数算法将它们视为离散值，不会进行特殊处理。  
  
 该表还显示了每种数据类型支持的内容类型。  
  
 内容类型特定于数据挖掘，你可以自定义在挖掘模型中处理或计算数据的方式。 例如，即使列中包含数字，你可能还是需要将其作为离散值进行建模。 如果列中包含数字，你还可以指定它们是装箱还是离散化，或者指定模型是否将它们作为连续值处理。 因此，内容类型对模型有极大的影响... 有关所有内容类型列表的信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
> [!NOTE]  
>  在其他机器学习系统中，你可能会遇到以下术语：名义数据、因素或类别、序号数据或序列数据。 通常，这些术语与内容类型相对应。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，数据类型仅指定存储的值类型，不指定其在模型中的用法。  
  
## <a name="specifying-a-data-type"></a>指定数据类型  
 如果直接使用数据挖掘扩展插件 (DMX) 创建挖掘模型，则可以在定义该模型时定义每一列的数据类型，同时 Analysis Services 将创建对应的包含指定数据类型的挖掘结构。 如果通过使用向导创建挖掘模型或挖掘结构，Analysis Services 将建议一种数据类型，或者您可以从列表中选择一种数据类型。  
  
## <a name="changing-a-data-type"></a>更改数据类型  
 如果更改某一列的数据类型，则必须始终重新处理挖掘结构以及基于该结构的所有挖掘模型。 有时候，如果更改数据类型，则可能无法再在特定的模型中使用该列。 在这种情况下，Analysis Services 将在您重新处理该模型时引发一个错误，或者将处理该模型但忽略该特定列。  
  
## <a name="see-also"></a>另请参阅  
 [内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)   
 [内容类型 (DMX)](../../dmx/content-types-dmx.md)   
 [数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [数据类型 &#40; DMX &#41;](../../dmx/data-types-dmx.md)   
 [挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)   
 [挖掘结构列](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  

