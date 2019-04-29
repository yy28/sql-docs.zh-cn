---
title: 放置属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 333b06ef76ae6407ca8a5605f1917dc0bb609aca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027823"
---
# <a name="position-property-ado"></a>Position 属性 (ADO)
指示当前位置[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**指定的偏移量，从一开始的流的当前位置的字节数的值。 默认值为 0，它表示流中的第一个字节。  
  
## <a name="remarks"></a>备注  
 可以移动到点流末尾之后的当前位置。 如果指定的流的末尾之外当前位置[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**Stream**对象会相应地增加。 在这种方式中添加任何新的字节数将为 null。  
  
> [!NOTE]
>  **位置**始终测量字节。 对于使用多字节字符集的文本流，用字符大小，以确定的字符数乘以位置。 例如，对于双字节字符集的第一个字符位于位置 0，位于位置 2，第三个字符的第二个字符在位置 4，依此类推。  
  
> [!NOTE]
>  负值不能用于更改中的当前位置**Stream**。 可用于仅正数和负数**位置**。  
  
> [!NOTE]
>  对于只读**Stream**对象，ADO 将不会返回错误，如果**位置**设置为值大于**大小**的**Stream**。 这不会更改的大小**Stream**，或更改**Stream**以任何方式的内容。 但是，执行此操作应避免，因为这会导致无意义**位置**值。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Charset 属性 (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
