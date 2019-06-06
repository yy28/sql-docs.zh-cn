---
title: AppendChunk 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e4b7b7a97af9059e944d2d2d9e7d19afedf4234d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696412"
---
# <a name="appendchunk-method-ado"></a>AppendChunk 方法 (ADO)
将数据追加到大文本或二进制数据[字段](../../../ado/reference/ado-api/field-object.md)，或设置为[参数](../../../ado/reference/ado-api/parameter-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parameters  
 *object*  
 一个**字段**或**参数**对象。  
  
 *Data*  
 一个**变体**，其中包含要追加到对象的数据。  
  
## <a name="remarks"></a>备注  
 使用**AppendChunk**方法**字段**或**参数**要用长二进制或字符数据填充对象。 在系统内存有限的情况下，你可以使用**AppendChunk**方法来操作部分而不是很长的值。  
  
## <a name="field"></a>字段  
 如果**adFldLong**位[特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性**字段**对象设置为**true**，可以使用**AppendChunk**为该字段的方法。  
  
 第一个**AppendChunk**上调用**字段**对象将数据写入到字段中，覆盖任何现有数据。 后续**AppendChunk**调用添加到现有数据。 如果将数据追加到的一个字段，然后设置或读取的当前记录中的另一个字段的值，ADO 将假定您已完成了将数据追加到第一个字段。 如果您调用**AppendChunk**同样，第一个字段 ADO 方法将解释为一个新的调用**AppendChunk**操作，并覆盖现有数据。 访问其他字段[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)不是第一个克隆的对象**记录集**对象不会破坏**AppendChunk**操作。  
  
 如果没有当前记录调用时**AppendChunk**上**字段**对象时，出现错误。  
  
> [!NOTE]
>  **AppendChunk**方法不对上进行操作**字段**的对象[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)对象。 它不会执行任何操作，并将产生运行时错误。  
  
## <a name="parameter"></a>参数  
 如果**adParamLong**位**特性**属性**参数**对象设置为**true**，可以使用**AppendChunk**为该参数的方法。  
  
 第一个**AppendChunk**上调用**参数**对象将数据写入到参数，覆盖任何现有数据。 后续**AppendChunk**上调用**参数**对象添加到现有的参数数据。 **AppendChunk**调用传递 null 值的放弃所有参数数据。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>请参阅  
 [AppendChunk 和 GetChunk 方法示例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法示例 （VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
