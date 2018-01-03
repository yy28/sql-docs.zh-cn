---
title: "GetChunk 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords: GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b6f0aed8689fb17b4cc5750c2b6b6b1f966e8c2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="getchunk-method-ado"></a>GetChunk 方法 (ADO)
返回所有或较大的文本或二进制数据的内容的一部分，[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>返回值  
 返回**Variant**。  
  
#### <a name="parameters"></a>Parameters  
 *Size*  
 A**长**等于的字节或你想要检索的字符数的表达式。  
  
## <a name="remarks"></a>Remarks  
 使用**GetChunk**方法**字段**要检索其长二进制或字符数据的部分或全部对象。 在系统内存有限的情况下，你可以使用**GetChunk**方法，以操作部分，而不是较长的值。  
  
 数据的**GetChunk**调用返回分配给*变量*。 如果*大小*大于剩余的数据， **GetChunk**方法仅返回的剩余数据而无需填充*变量*用空格。 如果该字段为空， **GetChunk**方法返回一个 null 值。  
  
 每个后续**GetChunk**呼叫会检索数据从何处开始以前**GetChunk**调用中断。 但是，如果你从一个字段，然后您设置或读取的当前记录中的另一个字段的值在检索数据，ADO 假定完第一个字段从检索数据。 如果调用**GetChunk**上再次，第一个字段 ADO 的方法将解释为新的调用**GetChunk**操作并开始读取数据的起始位置。 访问在其他字段[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)不是克隆的第一个对象**记录集**对象将不会打乱**GetChunk**操作。  
  
 如果**adFldLong**中位[属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性**字段**对象设置为**True**，你可以使用**GetChunk**该字段的方法。  
  
 如果没有最新记录时你使用**GetChunk**方法**字段**对象时，发生错误 3021 （最新记录）。  
  
> [!NOTE]
>  **GetChunk**方法不对上进行操作**字段**的对象[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。 它不会执行任何操作，并将生成运行时错误。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [AppendChunk 和 GetChunk 方法示例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法示例 （VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 方法 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
