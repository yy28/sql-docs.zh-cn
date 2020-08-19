---
description: WriteText 方法
title: WriteText 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: rothja
ms.author: jroth
ms.openlocfilehash: b561c8d798236fa0c6df262e2fc2db4c4729cb90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441489"
---
# <a name="writetext-method"></a>WriteText 方法
向 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 对象写入指定的文本字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>参数  
 *Data*  
 一个 **字符串** 值，该值包含要写入的字符中的文本。  
  
 *选项*  
 可选。 一个 [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) 值，该值指定是否必须在指定字符串的末尾写入行分隔符。  
  
## <a name="remarks"></a>备注  
 将指定的字符串写入 **流** 对象，而不会在每个字符串之间插入空格或字符。  
  
 [当前位置设置为写入](../../../ado/reference/ado-api/position-property-ado.md)数据后的字符。 **WriteText**方法不会截断流中的其余数据。 如果要截断这些字符，请调用 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果写入超出当前[EOS](../../../ado/reference/ado-api/eos-property.md)位置，则会将**流**的[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)增加为包含任何新字符，而**EOS**会移动到**流**中的新最后一个字节。  
  
> [!NOTE]
>  **WriteText**方法用于文本流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)为**adTypeText**) 。 对于二进制流 (**类型** 为 **adTypeBinary**) ，请使用 [Write](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Write 方法](../../../ado/reference/ado-api/write-method.md)
