---
title: "ServerMode 元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8145c7090e1c172fe210202e55078cb4bd404fcb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="servermode-element"></a>ServerMode 元素
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
  
  

