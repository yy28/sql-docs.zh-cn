---
title: "WritebackTableCreation 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: WritebackTableCreation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords: WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cc68c8d4d4a3cf02995a2effb8d523fc7b3ce722
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]确定是否将写回表创建期间[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)操作。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[处理](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 Analysis Services 实例上可用的对象的处理选项的详细信息，请参阅[处理多维模型 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 值**WritebackTableCreation**元素被限制为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*创建*|如果不存在写回表，则创建一个新表。 如果写回表已存在，则会出错。|  
|*CreateAlways*|创建一个新的写回表，并覆盖任何现有的写回表。|  
|*UseExisting*|如果已存在，请使用现有写回表。 如果写回表不存在，则会出错。|  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
