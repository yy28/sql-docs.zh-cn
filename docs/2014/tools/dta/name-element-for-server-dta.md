---
title: 服务器 (DTA) 的名称元素 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a63cce30a28daa0e990f11f86a7156df0bd7a7ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013654"
---
# <a name="name-element-for-server-dta"></a>服务器的名称元素 (DTA)
  包含要优化的数据库所在服务器的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|`string`，介于 1 到 255 个字符之间。|  
|**默认值**|无。|  
|**出现次数**|每个 **服务器** 元素必须出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[服务器元素&#40;DTA&#41;](server-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关如何使用该 **Name** 元素的示例，请参阅[服务器元素 (DTA)](server-element-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  