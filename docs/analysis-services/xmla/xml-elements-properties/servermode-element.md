---
title: ServerMode 元素 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 362e91994f4c195a6fe2d48a798444041d6855e8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="servermode-element"></a>ServerMode 元素
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  **ServerMode**服务器元素指定服务器操作中的模式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|（无）|  
|基数|0-1：仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 在下列模式之一下运行服务器：  
  
|“值”|Description|  
|-----------|-----------------|  
|*多维*|多维和数据挖掘模式|  
|*表格*|表格模式|  
|*SharePoint*|SharePoint 模式|  
  
## <a name="see-also"></a>另请参阅  
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  
