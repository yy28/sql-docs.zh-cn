---
title: StreamReadEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 33cb0b24806b0b4568a1d7eabc5a55aab4a9872b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759593"
---
# <a name="streamreadenum"></a>StreamReadEnum
指定是应从[流](../../../ado/reference/ado-api/stream-object-ado.md)对象中读取整个流还是下一行。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|默认。 从当前位置开始，将流中的所有字节读入[eos](../../../ado/reference/ado-api/eos-property.md)标记。 这是具有二进制流的唯一有效**StreamReadEnum**值（[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)为**adTypeBinary**）。|  
|**adReadLine**|-2|读取流中的下一行（由[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性指定）。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[Read 方法](../../../ado/reference/ado-api/read-method.md)|[ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)|
