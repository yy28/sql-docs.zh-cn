---
title: "AppendChunk 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 812566487a453d806e1defcd7b2b7977e5f1935f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="appendchunk-method-ado"></a>AppendChunk 方法 (ADO)
将数据追加到较大文本或二进制数据[字段](../../../ado/reference/ado-api/field-object.md)，或[参数](../../../ado/reference/ado-api/parameter-object.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parameters  
 *对象*  
 A**字段**或**参数**对象。  
  
 *数据*  
 A **Variant** ，其中包含要追加到对象的数据。  
  
## <a name="remarks"></a>注释  
 使用**AppendChunk**方法**字段**或**参数**填充长二进制或字符数据的对象。 在系统内存有限的情况下，你可以使用**AppendChunk**方法，以操作部分而不是较长的值。  
  
## <a name="field"></a>字段  
 如果**adFldLong**中位[属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性**字段**对象设置为**true**，你可以使用**AppendChunk**该字段的方法。  
  
 第一个**AppendChunk**上调用**字段**对象将数据写入该字段中，覆盖任何现有数据。 后续**AppendChunk**调用添加到现有数据。 如果将数据追加到一个字段，然后设置或读取的当前记录中的另一个字段的值，ADO 假定您已完成了将数据追加到第一个字段。 如果调用**AppendChunk**上再次，第一个字段 ADO 的方法将解释为新的调用**AppendChunk**操作，并覆盖现有数据。 访问在其他字段[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)不是克隆的第一个对象**记录集**对象将不会打乱**AppendChunk**操作。  
  
 如果没有最新记录时你调用**AppendChunk**上**字段**对象，将会出错。  
  
> [!NOTE]
>  **AppendChunk**方法不对上进行操作**字段**的对象[记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)对象。 它不会执行任何操作，并将生成运行时错误。  
  
## <a name="parameter"></a>参数  
 如果**adParamLong**中位**属性**属性**参数**对象设置为**true**，你可以使用**AppendChunk**为该参数的方法。  
  
 第一个**AppendChunk**上调用**参数**对象将数据写入参数，覆盖任何现有数据。 后续**AppendChunk**上调用**参数**对象添加到现有的参数数据。 **AppendChunk**传递 null 值的调用放弃所有参数数据。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>另请参阅  
 [AppendChunk 和 GetChunk 方法示例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法示例 （VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)

