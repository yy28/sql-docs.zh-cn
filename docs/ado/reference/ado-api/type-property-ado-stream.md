---
title: 类型属性 (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9b996ba4bedbb4ccf1ccb0453e4da33e09206a18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938230"
---
# <a name="type-property-ado-stream"></a>Type 属性（ADO 流）
指示中包含的数据类型[Stream](../../../ado/reference/ado-api/stream-object-ado.md) （二进制或文本）。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)值，该值指定中包含的数据类型**Stream**对象。 默认值是**adTypeText**。 但是，如果最初编写到新的二进制数据，则为空**Stream**，则**类型**将变为**adTypeBinary**。  
  
## <a name="remarks"></a>备注  
 **类型**属性为读/写，仅当当前位于开头时才**Stream** ([位置](../../../ado/reference/ado-api/position-property-ado.md)为 0)，并在任何其他位置以只读的。  
  
 **类型**属性确定应使用哪些方法用于读取和写入**Stream**。 文本**流**，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)并[WriteText](../../../ado/reference/ado-api/writetext-method.md)。 有关二进制**流**，使用[读取](../../../ado/reference/ado-api/read-method.md)并[编写](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [RecordType 属性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 属性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
