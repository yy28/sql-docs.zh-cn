---
description: CopyTo 方法 (ADO)
title: " (ADO) 的 CopyTo 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fbb9fc1c9d6f2a86a6f047b20962e5513798a26e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444359"
---
# <a name="copyto-method-ado"></a>CopyTo 方法 (ADO)
根据[流](../../../ado/reference/ado-api/stream-object-ado.md)中的[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)) 将指定数量的字符或字节 (复制到另一个**流**对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>参数  
 *DestStream*  
 一个对象变量值，该值包含对打开的 **流** 对象的引用。 当前**流**将复制到由*DestStream*指定的目标**流**中。 目标 **流** 必须已打开。 否则，将发生运行时错误。  
  
> [!NOTE]
>  *DestStream*参数可能不是**stream**对象的代理，因为这需要访问无法远程访问客户端的**流**对象上的专用接口。  
  
 *NumChars*  
 可选。 一个 **整数** 值，指定要从源 **流** 中的当前位置复制到目标 **流**的字节数或字符数。 默认值为-1，指定将所有字符或字节从当前位置复制到 [EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>备注  
 此方法从 [位置](../../../ado/reference/ado-api/position-property-ado.md) 属性指定的当前位置开始复制指定数量的字符或字节。 如果指定的数字大于在 **eos**之前的可用字节数，则仅复制当前位置到 **eos** 之间的字符或字节。 如果 *NumChars* 的值为-1 或省略，则会复制从当前位置开始的所有字符或字节。  
  
 如果目标流中存在现有字符或字节，则不会保留副本结束点之外的所有内容，并且不会被截断。 **位置** 成为紧接最后复制的字节之后的字节。 如果要截断这些字节，请调用 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 **CopyTo**应用于将数据复制到与源**流**具有相同类型的目标**流** (它们的**类型**属性设置既是**adTypeText** ，要么都是**adTypeBinary**) 。 对于文本**流**对象，可以更改目标**流**的[字符集](../../../ado/reference/ado-api/charset-property-ado.md)属性设置，以将其从一个字符集转换到另一个字符集。 此外，文本 **流** 对象可以成功复制到二进制 **流** 对象，但不能将二进制 **流** 对象复制到文本 **流** 对象中。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
