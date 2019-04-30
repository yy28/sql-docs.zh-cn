---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26ccabf3e73a67c14e7201f26e4ebf739a6352cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311855"
---
# <a name="streamreadenum"></a>StreamReadEnum
指定是否应从读取整个流或下一行[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|默认值。 读取所有字节流，从当前的位置及更高版本[EOS](../../../ado/reference/ado-api/eos-property.md)标记。 这是唯一有效**StreamReadEnum**值，该值具有二进制流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**)。|  
|**adReadLine**|-2|从流中读取下一行 (由[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Read 方法](../../../ado/reference/ado-api/read-method.md)|[ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)|
