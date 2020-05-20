---
title: AppendChunk 方法（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ebf6f52e4c2ac9cc4875db26e633457915c0a5e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762936"
---
# <a name="appendchunk-method-ado"></a>AppendChunk 方法 (ADO)
将数据追加到大文本或二进制数据[字段](../../../ado/reference/ado-api/field-object.md)，或追加到[参数](../../../ado/reference/ado-api/parameter-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>参数  
 *object*  
 一个**字段**或**参数**对象。  
  
 *Data*  
 一个包含要追加到对象的数据的**变量**。  
  
## <a name="remarks"></a>备注  
 对**字段**或**参数**对象使用**AppendChunk**方法，以使用较长的二进制或字符数据填充它。 在系统内存有限的情况下，可以使用**AppendChunk**方法在部分中而不是完整地操作长值。  
  
## <a name="field"></a>字段  
 如果**字段**对象的[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)属性中的**adFldLong**位设置为**true**，则可以对该字段使用**AppendChunk**方法。  
  
 **Field**对象上的第一个**AppendChunk**调用将数据写入字段，并覆盖任何现有数据。 后续**AppendChunk**调用将添加到现有数据。 如果要将数据追加到一个字段，然后设置或读取当前记录中另一个字段的值，则 ADO 会假定您已完成将数据追加到第一个字段。 如果再次对第一个字段调用**AppendChunk**方法，则 ADO 会将调用解释为新的**AppendChunk**操作，并覆盖现有数据。 访问不是第一个**记录集**对象的克隆的其他[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中的字段将不会中断**AppendChunk**操作。  
  
 如果对**字段**对象调用**AppendChunk**时没有当前记录，则会发生错误。  
  
> [!NOTE]
>  **AppendChunk**方法不对[记录对象（ADO）](../../../ado/reference/ado-api/record-object-ado.md)对象的**字段**对象进行操作。 它不执行任何操作，并将生成运行时错误。  
  
## <a name="parameter"></a>参数  
 如果**参数**对象的**Attributes**属性中的**adParamLong**位设置为**true**，则可以对该参数使用**AppendChunk**方法。  
  
 **参数**对象上的第一个**AppendChunk**调用将数据写入参数，并覆盖任何现有数据。 后续**AppendChunk**对**参数**对象的调用将添加到现有参数数据。 传递 null 值的**AppendChunk**调用会丢弃所有参数数据。  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>另请参阅  
 [AppendChunk 和 GetChunk 方法示例（VB）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法示例（VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Attributes 属性（ADO）](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
