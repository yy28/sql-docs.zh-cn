---
title: ImpersonationInfoSecurity 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 757f96c00ab9041a8d85950e7603ec49bf21b1a8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031768"
---
# <a name="impersonationinfosecurity-element-assl"></a>ImpersonationInfoSecurity 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含只读的值，该值指示是否已对中提供的安全凭据进行任何更改[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationInfoSecurity>...</ImpersonationInfoSecurity>  
  
</ImpersonationInfo>...  
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
|父元素|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*PasswordRemoved*|密码信息已从提供的安全凭据中删除。|  
|*保持不变*|未对提供的安全凭据进行更改。|  
  
 对应于的允许值为枚举**ImpersonationInfoSecurity**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ImpersonationInfoSecurity>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
