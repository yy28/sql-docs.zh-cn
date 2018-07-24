---
title: 架构数据库的元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 07b3e86c5329eac6685e6411b9abc8af55e64641
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984339"
---
# <a name="schema-element-for-database-dta"></a>数据库的架构元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  指定要优化的数据库的架构。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|描述|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|对于在 **Server** 元素下指定的 **Database** 元素，需要使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[服务器的数据库元素 (DTA)](../../tools/dta/database-element-for-server-dta.md)|  
|**子元素**|[架构的名称元素 (DTA)](../../tools/dta/name-element-for-schema-dta.md)<br /><br /> [架构的表元素 (DTA)](../../tools/dta/table-element-for-schema-dta.md)|  
  
## <a name="example"></a>示例  
 有关此元素的使用示例，请参阅[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
