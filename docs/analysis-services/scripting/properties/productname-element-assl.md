---
title: ProductName 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 55dac0fb7f1ec69d023e1c98ff16f32023100b65
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="productname-element-assl"></a>ProductName 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的实例的只读的产品名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]关联[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Server>  
      ...  
      <ProductName>...</ProductName>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **ProductName**元素提供对与实例关联的产品的名称的只读访问权限[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 对应于的父元素**ProductName**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
