---
title: 编写方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84e10e8edb6cca3c4e56ac1dd0106b3c641af872
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945906"
---
# <a name="write-method"></a>Write 方法
将二进制数据写入[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parameters  
 *Buffer*  
 一个**变体**，其中包含要写入的字节数组。  
  
## <a name="remarks"></a>备注  
 将指定的字节写入到**Stream**不包含每个字节之间的任何干预空格的对象。  
  
 当前[位置](../../../ado/reference/ado-api/position-property-ado.md)设置为以下写入的数据的字节。 **编写**方法不会截断其余流中的数据。 如果你想要这些字节截断，则调用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果过去的当前写入[EOS](../../../ado/reference/ado-api/eos-property.md)位置，[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**Stream**将增加以包含任何新的字节数，以及**EOS**将移动在新的最后一个字节到**Stream**。  
  
> [!NOTE]
>  **编写**方法使用二进制流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**)。 对于文本流 (**类型**是**adTypeText**)，使用[WriteText](../../../ado/reference/ado-api/writetext-method.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
