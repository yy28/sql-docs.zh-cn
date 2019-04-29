---
title: 内容类型 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 002dfef00f428f7fe87f3de06eb174e0566282c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853496"
---
# <a name="content-types-dmx"></a>内容类型 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  除了数据类型信息以外，数据挖掘算法还需要其他信息（如内容类型）才能正常工作。 内容类型可帮助算法确定对列中数据的处理方式。  
  
 每种算法可支持特定的内容类型。 例如，[!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 算法不能使用连续列。 若要在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 模型中使用连续列，必须对列中的数据进行离散化处理。 有些算法要求提供特定的内容类型才能正常工作。 例如，[!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法要求一个 Key Time 列来标识收集数据的时间。  
  
 内容的完整说明类型，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支持，请参阅[内容类型&#40;数据挖掘&#41;](../analysis-services/data-mining/content-types-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [数据挖掘扩展插件 (DMX) 参考](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
