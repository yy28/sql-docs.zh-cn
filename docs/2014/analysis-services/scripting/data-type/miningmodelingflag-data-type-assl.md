---
title: MiningModelingFlag 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningModelingFlag Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelingFlag
helpviewer_keywords:
- MiningModelingFlag data type
ms.assetid: aaa72ba8-051e-4b01-b1e9-9c8d83b8b752
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 32ee744bdfcd084c4be88511ecba025ca9a270de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128420"
---
# <a name="miningmodelingflag-data-type-assl"></a>MiningModelingFlag 数据类型 (ASSL)
  定义一个基元数据类型，表示的可用的建模标志[ModelingFlag](../objects/modelingflag-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|String（枚举）|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|InclusionThresholdSetting|  
|派生元素|[ModelingFlag](../objects/modelingflag-element-assl.md) ([ModelingFlags](../collections/modelingflags-element-assl.md)集合[MiningModelColumn](miningmodelcolumn-data-type-assl.md)或[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 标志名称可包含空格。 下表中列出了本机支持的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|无论列中的值为何，列均应建模为具有两种状态：缺少和非缺少。 对于值在事例间是稀疏的嵌套表，这一点特别有用。|  
|*不为 NULL*|该列不接受 NULL 值。|  
|*回归量*|列为事例的测试提供回归量值。|  
  
 如果实例上聚合第三方 OLE DB 或数据挖掘提供了可能使用其他提供程序特定标志[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 在 Analysis Management Objects (AMO) 对象模型中，有一个密切相关的元素：<xref:Microsoft.AnalysisServices.MiningModelingFlags>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  