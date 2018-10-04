---
title: 键入元素 (Action) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af38eb6a60e8e54ecfc4ac5bb4fb05faeab69feb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168417"
---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
  包含的类型[操作](../objects/action-element-assl.md)元素。  
  
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
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Url*|在 Internet 浏览器中显示可变页。|  
|*Html*|在 Internet 浏览器中执行 HTML 脚本。|  
|*Statement*|执行 OLE DB 命令。|  
|*钻取*|检索钻取的行集。<br /><br /> 此值等同于*行集*，可标识钻取操作。 它只能是在操作上使用它的[TargetType](targettype-element-assl.md)值设置为*单元格*。|  
|*数据集*|检索数据集。|  
|*Rowset*|检索行集。|  
|*命令行*|在命令提示符处执行命令。|  
|*专有*|使用与此表中前面列出的接口不同的一个接口执行操作。|  
|*报告*|在 Internet 浏览器中显示可变页。<br /><br /> 此值等同于*Url*和标识报告操作。|  
  
 父级对应的元素`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [DrillThroughAction 数据类型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [ReportAction 数据类型&#40;ASSL&#41;](../data-type/reportaction-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
