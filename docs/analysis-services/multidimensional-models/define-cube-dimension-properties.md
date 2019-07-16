---
title: 定义多维数据集维度属性 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4401055a15afe73a1f33ee43354f7ee45f887a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178752"
---
# <a name="define-cube-dimension-properties"></a>定义多维数据集维度属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  多维数据集维度是多维数据集中的数据库维度实例。 一个数据库维度可用于多个多维数据集，多个多维数据集维度可基于单个数据库维度。 下表说明了多维数据集维度的属性。  
  
|属性|描述|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|控制 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的聚合设计器如何设计聚合。 此属性可以有下列值：<br /><br /> **Full**：在多维数据集中的每个聚合都必须包括所有成员。<br /><br /> **无**：多维数据集的任何聚合都能不包括所有成员。 这是默认值。<br /><br /> **Unrestricted**：聚合设计器不作任何限制。<br /><br /> **Default**：与不受限制的相同的功能。|  
|**说明**|为该级别提供一个说明性名称。|  
|**DimensionID**|包含数据库维度的唯一标识符 (ID)。|  
|**HierarchyUniqueNameStyle**|确定如何为包含在多维数据集维度中的层次结构生成唯一名称。 此属性可以有下列值：<br /><br /> **IncludeDimensionName**：<br />                    包括维度的名称，将其作为层次结构名称的一部分。 这是默认值。<br /><br /> **ExcludeDimensionName**：<br />                    维度的名称不作为层次结构名称的一部分。|  
|**ID**|包含多维数据集维度的唯一标识符。|  
|**MemberUniqueNameStyle**|确定如何为包含在多维数据集维度中的层次结构的成员生成唯一的名称。 此属性可以有下列值：<br /><br /> **Native**：<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动确定成员的唯一名称。 这是默认值。<br /><br /> **NamePath**： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将生成由每个级别的名称和成员的标题组成的复合名称。|  
|**名称**|包含多维数据集维度的友好名称。 默认情况下，多维数据集维度与数据库维度同名，除非已经定义了另一个同名的多维数据集维度。|  
|**Visible**|确定多维数据集维度是否是可见的。 默认值是 **True**秒。|  
  
## <a name="see-also"></a>请参阅  
 [维度（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
