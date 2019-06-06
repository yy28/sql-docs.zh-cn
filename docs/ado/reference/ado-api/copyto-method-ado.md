---
title: CopyTo 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbfdff7c22152acfd0deb97a6e278bd5fd3f553f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698436"
---
# <a name="copyto-method-ado"></a>CopyTo 方法 (ADO)
复制指定的数目的字符或字节 (具体取决于[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)) 中[Stream](../../../ado/reference/ado-api/stream-object-ado.md)到另一个**Stream**对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parameters  
 *DestStream*  
 一个包含一种开放的引用的对象变量值**Stream**对象。 当前**Stream**复制到目标**Stream**指定的*DestStream*。 目标**Stream**已被打开。 如果不是，将发生运行时错误。  
  
> [!NOTE]
>  *DestStream*参数不能的代理**Stream**对象，因为这需要访问的专用接口上**Stream**不能为远程连接到的对象客户端。  
  
 *NumChars*  
 可选。 **整数**值，该值指定要从当前源中的位置复制的字节或字符数**Stream**到目标**Stream**。 默认值为-1，指定从当前位置到复制所有字符或字节[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>备注  
 此方法将指定的字符数或字节数，从当前指定的位置开始复制[位置](../../../ado/reference/ado-api/position-property-ado.md)属性。 如果指定的数量大于可用的之前的字节数**EOS**，然后仅字符或字节数从当前位置到**EOS**复制。 如果的值*NumChars*为-1，或省略，所有字符或字节从当前的位置开始都复制。  
  
 如果已存在的字符或目标流中的字节，所有内容，而只复制的结束位置的点保留，并且不被截断。 **位置**变得紧跟复制的最后一个字节的字节。 如果你想要这些字节截断，则调用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 **CopyTo**应该用于将数据复制到目标**Stream**与源相同的类型的**Stream** (其**类型**属性设置将这两个**adTypeText**和 / 或**adTypeBinary**)。 文本**Stream**对象，可以更改[字符集](../../../ado/reference/ado-api/charset-property-ado.md)属性设置的目标**Stream**从设置到另一个字符转换。 此外，文本**Stream**对象可以成功复制到二进制**Stream**对象，但二进制**Stream**对象不能复制到文本**Stream**对象。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
