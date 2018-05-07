---
title: MiningModelingFlag 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7d000f7efa4fc0355c8359b87931caeb0cbafa12
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="miningmodelingflag-data-type-assl"></a>MiningModelingFlag 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个基元数据类型，表示的可用的建模标志[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|String（枚举）|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|無|  
|派生元素|[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) ([ModelingFlags](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)集合[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)或[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>注释  
 标志名称可包含空格。 下表中列出了本机支持的值。  
  
|“值”|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|无论列中的值为何，列均应建模为具有两种状态：缺少和非缺少。 对于值在事例间是稀疏的嵌套表，这一点特别有用。|  
|*不为 NULL*|该列不接受 NULL 值。|  
|*回归量*|列为事例的测试提供回归量值。|  
  
 如果实例上聚合第三方 OLE DB 或数据挖掘提供了可能使用其他提供程序特定标志[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 在 Analysis Management Objects (AMO) 对象模型中，有一个密切相关的元素：<xref:Microsoft.AnalysisServices.MiningModelingFlags>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
