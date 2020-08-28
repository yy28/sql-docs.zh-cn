---
description: StreamReadEnum
title: StreamReadEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: d9f685a80d822950a159ddb3fbc9f148489a723e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988468"
---
# <a name="streamreadenum"></a>StreamReadEnum
指定是应从 [流](./stream-object-ado.md) 对象中读取整个流还是下一行。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|默认。 从当前位置开始，将流中的所有字节读入 [eos](./eos-property.md) 标记。 这是 ([类型](./type-property-ado-stream.md)为**adTypeBinary**) 的二进制流唯一有效的**StreamReadEnum**值。|  
|**adReadLine**|-2|读取 [LineSeparator](./lineseparator-property-ado.md) 属性) 指定的 (流中的下一行。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [Read 方法](./read-method.md)  
    :::column-end:::
    :::column:::
        [ReadText 方法](./readtext-method.md)  
    :::column-end:::
:::row-end:::