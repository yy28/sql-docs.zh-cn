---
title: 类型元素 （操作） (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8b87ab109aaad0c40e1debb3a8ea84047b6e8f6b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039101"
---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的一种[操作](../../../analysis-services/scripting/objects/action-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Url*|在 Internet 浏览器中显示可变页。|  
|*html*|在 Internet 浏览器中执行 HTML 脚本。|  
|*声明专用纸*|执行 OLE DB 命令。|  
|*钻取*|检索钻取的行集。<br /><br /> 此值等同于*行集*和标识钻取操作。 它仅可以在操作上使用其[TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)值设置为*单元格*。|  
|*数据集*|检索数据集。|  
|*Rowset*|检索行集。|  
|*命令行*|在命令提示符处执行命令。|  
|*专有*|使用与此表中前面列出的接口不同的一个接口执行操作。|  
|*报告*|在 Internet 浏览器中显示可变页。<br /><br /> 此值等同于*Url*和标识报表操作。|  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [DrillThroughAction 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [ReportAction 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
