---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bd88a62a46bae523904b308d011ebe956e02497
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="streamreadenum"></a>StreamReadEnum
指定是否应从读取整个流或下一行[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|默认值。 读取所有字节从流中，从当前位置及以上版本[EOS](../../../ado/reference/ado-api/eos-property.md)标记。 这是仅有的有效**StreamReadEnum**与二进制数据流的值 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**)。|  
|**adReadLine**|-2|从流中读取下一行 (由[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Read 方法](../../../ado/reference/ado-api/read-method.md)|[ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)|
