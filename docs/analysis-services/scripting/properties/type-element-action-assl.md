---
title: "类型元素 （操作） (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (Action)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 534cdf99-1edf-4490-9eaa-61f189a19434
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62735cdcc160bccf6b90ed2c26b269b8b3d1d3eb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
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
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Url*|在 Internet 浏览器中显示可变页。|  
|*Html*|在 Internet 浏览器中执行 HTML 脚本。|  
|*Statement*|执行 OLE DB 命令。|  
|*钻取*|检索钻取的行集。<br /><br /> 此值等同于*行集*和标识钻取操作。 它仅可以在操作上使用其[TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)值设置为*单元格*。|  
|*数据集*|检索数据集。|  
|*行集*|检索行集。|  
|*命令行*|在命令提示符处执行命令。|  
|*专有*|使用与此表中前面列出的接口不同的一个接口执行操作。|  
|*报告*|在 Internet 浏览器中显示可变页。<br /><br /> 此值等同于*Url*和标识报表操作。|  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [DrillThroughAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [ReportAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

