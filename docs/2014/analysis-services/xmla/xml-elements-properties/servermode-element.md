---
title: ServerMode 元素 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b329f9882b9eff2adf1a79041ea83c51a627f15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239447"
---
# <a name="servermode-element"></a>ServerMode 元素
  `ServerMode` 服务器元素指定服务器的运行模式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|（无）|  
|基数|0-1：仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Server](../../scripting/objects/server-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在下列模式之一下运行服务器：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*多维*|多维和数据挖掘模式|  
|*表格*|表格模式|  
|*SharePoint*|SharePoint 模式|  
  
## <a name="see-also"></a>请参阅  
 [Server](../../scripting/objects/server-element-assl.md)  
  
  
