---
title: Read 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b5bbc04c94d491c096db047d574cc3b5fd8ee38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156628"
---
# <a name="read-method"></a>Read 方法
从二进制文件中读取指定的字节数[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parameters  
 *NumBytes*  
 可选。 一个**长**值，该值指定要从文件中读取的字节数或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值**adReadAll**，这是默认设置。  
  
## <a name="return-value"></a>返回值  
 **读**方法读取指定的数目的字节数或从整个流**Stream**对象并返回生成的数据作为**变体**。  
  
## <a name="remarks"></a>备注  
 如果*变量*个以上的字节数会留在**Stream**，返回剩余的字节。 读取的数据不填充以匹配指定的长度*变量*。 如果不有任何留下供读取的字节，则返回值为 null 的变体。 **读取**不能用于向后读取。  
  
> [!NOTE]
>  *变量*始终测量字节。 文本**Stream**对象 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)
