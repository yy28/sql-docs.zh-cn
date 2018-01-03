---
title: "StreamReadEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: StreamReadEnum
helpviewer_keywords: StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d70ab8ad7ecae932688c652667d4d0d2a303239
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="streamreadenum"></a>StreamReadEnum
指定是否应从读取整个流或下一行[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|默认值。 读取所有字节从流中，从当前位置及以上版本[EOS](../../../ado/reference/ado-api/eos-property.md)标记。 这是仅有的有效**StreamReadEnum**与二进制数据流的值 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**)。|  
|**adReadLine**|-2|从流中读取下一行 (由[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Read 方法](../../../ado/reference/ado-api/read-method.md)|[ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)|
