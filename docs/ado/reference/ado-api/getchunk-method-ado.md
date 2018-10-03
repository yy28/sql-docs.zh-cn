---
title: GetChunk 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 538ccfd71375521bf0ba035ccfa55746c4d76af9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602505"
---
# <a name="getchunk-method-ado"></a>GetChunk 方法 (ADO)
返回所有或大文本或二进制数据的内容的一部分，[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>返回值  
 返回**变体**。  
  
#### <a name="parameters"></a>Parameters  
 *Size*  
 一个**长**等于的字节数或你想要检索的字符数的表达式。  
  
## <a name="remarks"></a>备注  
 使用**GetChunk**方法**字段**要检索其长二进制或字符数据的部分或全部对象。 在系统内存有限的情况下，你可以使用**GetChunk**方法来操作部分，而不是很长的值。  
  
 数据的**GetChunk**调用返回分配给*变量*。 如果*大小*大于剩余数据**GetChunk**方法仅返回的其余数据而无需填充*变量*具有空白空间。 如果该字段为空， **GetChunk**方法将返回 null 值。  
  
 每个后续**GetChunk**调用会检索数据从何处开始以前**GetChunk**离开的调用。 但是，如果要从一个字段，然后您设置或读取的当前记录中的另一个字段的值来检索数据，ADO 假定你已完成从第一个字段中检索数据。 如果您调用**GetChunk**同样，第一个字段 ADO 方法将解释为一个新的调用**GetChunk**操作并开始读取数据的起始位置。 访问其他字段[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)不是第一个克隆的对象**记录集**对象不会破坏**GetChunk**操作。  
  
 如果**adFldLong**位[特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性**字段**对象设置为**True**，可以使用**GetChunk**为该字段的方法。  
  
 如果没有最新记录时使用**GetChunk**方法**字段**对象时，会发生错误 3021 （最新记录）。  
  
> [!NOTE]
>  **GetChunk**方法不对上进行操作**字段**的对象[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。 它不会执行任何操作，并将产生运行时错误。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [AppendChunk 和 GetChunk 方法示例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法示例 （VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 方法 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
