---
title: 别名元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fb37f0a7393b6055621e9575aef3c20a50313ff9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032398"
---
# <a name="aliases-element-assl"></a>Aliases 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的集合[别名](../../../analysis-services/scripting/properties/alias-element-assl.md)与关联的元素[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)元素  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Account>  
      ...  
   <Aliases>  
      <Alias>...</Alias>  
      </Aliases>  
      ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无（集合）|  
|默认值|无（集合）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|子元素|[别名](../../../analysis-services/scripting/properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 对父级的对应的元素**别名**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另请参阅  
 [帐户元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
