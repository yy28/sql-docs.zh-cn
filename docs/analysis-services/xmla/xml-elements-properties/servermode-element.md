---
title: ServerMode 元素 |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: af2c8d12e2861993474a093b2385f393924f2f67
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
