---
title: CopyTo 方法 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 368385864bf9cb5e0497e9acd3bf40e6e468b8bc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="copyto-method-ado"></a>CopyTo 方法 (ADO)
将复制指定的字符或字节数 (具体取决于[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)) 中[流](../../../ado/reference/ado-api/stream-object-ado.md)到另一个**流**对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parameters  
 *DestStream*  
 一个包含向打开的引用的对象变量值**流**对象。 当前**流**复制到目标**流**指定的*DestStream*。 目标**流**必须已被打开。 如果没有，则会发生运行时错误。  
  
> [!NOTE]
>  *DestStream*参数不可能的代理**流**对象，因为这需要访问权限的专用接口上**流**无法远程访问的对象客户端。  
  
 *Numchar*  
 選擇性。 **整数**值，该值指定的字节或字符从当前源中的位置复制数**流**到目标**流**。 默认值为 1，它指定从当前位置复制所有字符或字节[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>注释  
 此方法会复制指定的字符或从当前指定的位置开始的字节数[位置](../../../ado/reference/ado-api/position-property-ado.md)属性。 如果指定的数量的可用之前的字节数超过了**EOS**，然后仅字符或字节从当前位置到**EOS**复制。 如果值*Numchar*为 1，或省略，所有复制的字符或从当前的位置开始的字节。  
  
 如果存在字符或目标流中的字节，超出复制的结尾处的位置的所有内容保持状态，并不会被截断。 **位置**变得紧跟复制的最后一个字节的字节。 如果要进行截断操作这些字节，调用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 **CopyTo**应该用于将数据复制到目标**流**与源相同的类型的**流**(其**类型**属性设置不这两个**adTypeText**和 / 或**adTypeBinary**)。 文本**流**对象，你可以更改[Charset](../../../ado/reference/ado-api/charset-property-ado.md)属性设置的目标**流**若要从一个字符设置为另一个翻译。 此外，文本**流**对象可以成功复制到二进制**流**对象，但二进制**流**对象不能复制到文本**流**对象。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
