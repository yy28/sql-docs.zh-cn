---
title: 类型元素 （操作） (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (Action)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 534cdf99-1edf-4490-9eaa-61f189a19434
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d71abdd26cea5fa03c8e70f882f893878a70969a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026623"
---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
  包含的一种[操作](../objects/action-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Url*|在 Internet 浏览器中显示可变页。|  
|*Html*|在 Internet 浏览器中执行 HTML 脚本。|  
|*Statement*|执行 OLE DB 命令。|  
|*钻取*|检索钻取的行集。<br /><br /> 此值等同于*行集*和标识钻取操作。 它仅可以在操作上使用其[TargetType](targettype-element-assl.md)值设置为*单元格*。|  
|*数据集*|检索数据集。|  
|*Rowset*|检索行集。|  
|*命令行*|在命令提示符处执行命令。|  
|*专有*|使用与此表中前面列出的接口不同的一个接口执行操作。|  
|*报告*|在 Internet 浏览器中显示可变页。<br /><br /> 此值等同于*Url*和标识报表操作。|  
  
 对应于的父元素`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [DrillThroughAction 数据类型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [ReportAction 数据类型&#40;ASSL&#41;](../data-type/reportaction-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  