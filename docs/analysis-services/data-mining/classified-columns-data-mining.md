---
title: 分类列 （数据挖掘） |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9fcd5aac5f5384f62b4fe4cd53f480ac70f69a63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="classified-columns-data-mining"></a>已分类列（数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  定义已分类列时，在挖掘结构中创建当前列和另一个列之间的关系。 指定为已分类列的挖掘结构列中的数据包含描述挖掘结构中另一个列的值的分类信息。  
  
 例如，假定有两个包含数值数据的列：其中 [Yearly Purchases] 列包含特定日历年每个客户每年的总购买量，[Standard Deviations] 列则包含这些值的标准偏差。 在此例中，可以指定 [Yearly Purchases] 列为已分类列，模型将在分析中使用此关系。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的算法不支持使用已分类列，此功能用于创建自定义算法中。  
  
## <a name="defining-a-classified-column"></a>定义已分类列  
 已分类列的数据类型必须为 **Long** 或 **Double**。  
  
 以下列表说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持的已分类列内容类型。  
  
 **PROBABILITY**  
 列内的值是相关值的概率，是介于 0 和 1 之间的数字。  
  
 **VARIANCE**  
 列内的值是相关值的方差。  
  
 **STDEV**  
 列内的值是相关值的标准偏差。  
  
 **PROBABILITY_VARIANCE**  
 列内的值是相关值概率的方差。  
  
 **PROBABILITY_STDEV**  
 列内的值是相关值概率的标准偏差。  
  
 **Support**  
 列内的值是相关值的权重或事例复制因子。  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [挖掘结构 & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [数据类型 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  
