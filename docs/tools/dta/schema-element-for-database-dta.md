---
title: "数据库 (DTA) 的架构元素 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9d38648ceb144c20158888ca2f1040a1cae22db
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="schema-element-for-database-dta"></a>数据库的架构元素 (DTA)
  指定要优化的数据库的架构。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
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
  
  
