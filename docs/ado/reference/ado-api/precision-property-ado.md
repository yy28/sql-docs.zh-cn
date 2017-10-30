---
title: "精度属性 (ADO) |Microsoft 文档"
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
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce6c07fa24f146664ffe5433869e4edf45abdd69
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="precision-property-ado"></a>精度属性 (ADO)
表示的数字值在精度程度[参数](../../../ado/reference/ado-api/parameter-object.md)对象或对数值[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字节**值，该值指示最多的用来表示值的位数。  
  
## <a name="remarks"></a>注释  
 使用**精度**属性来确定用于表示的数字值的数字的最大数**参数**或**字段**对象。  
  
 值为读/写上**参数**对象。  
  
 有关**字段**对象，**精度**是通常是只读的。 但是，新对于**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)，**精度**为仅读/写后[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定的数据提供程序已经成功地添加新和**字段**通过调用[更新](../../../ado/reference/ado-api/update-method.md)方法**字段**集合。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>另请参阅  
 [NumericScale 和精度属性示例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和精度属性示例 （VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 属性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)

