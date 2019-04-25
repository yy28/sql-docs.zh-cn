---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3b50db388151de1f5b99d8d9a3f48904e6d7c2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642959"
---
# <a name="writetext-method"></a>WriteText 方法
将一个指定的文本字符串写入[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *Data*  
 一个**字符串**值，该值包含要写入的字符中的文本。  
  
 *选项*  
 可选。 一个[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)值，该值指定是否必须在指定的字符串末尾写入行分隔符字符。  
  
## <a name="remarks"></a>备注  
 指定的字符串写入到**Stream**对象而无需任何干预空格或每个字符串之间的字符。  
  
 当前[位置](../../../ado/reference/ado-api/position-property-ado.md)设置为后面写入的数据的字符。 **WriteText**方法不会截断其余流中的数据。 如果你想要截断这些字符，调用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果过去的当前写入[EOS](../../../ado/reference/ado-api/eos-property.md)位置[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**Stream**将增加以包含新的任何字符，以及**EOS**将移动到新的最后一个字节中**Stream**。  
  
> [!NOTE]
>  **WriteText**方法使用文本流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 对于二进制流 (**类型**是**adTypeBinary**)，使用[编写](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Write 方法](../../../ado/reference/ado-api/write-method.md)
