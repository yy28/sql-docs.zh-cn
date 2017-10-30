---
title: "NumericScale 属性 (ADO) |Microsoft 文档"
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
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 98f5c141f0cf9483ab7d527f46911a36257ced47
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="numericscale-property-ado"></a>NumericScale 属性 (ADO)
指示小数位数的数字值在[参数](../../../ado/reference/ado-api/parameter-object.md)或[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字节**值，该值指示的小数位数的数字的值数将会解决。  
  
## <a name="remarks"></a>注释  
 使用**NumericScale**属性来确定小数点右侧的位数将用于表示的数字值**参数**或**字段**对象。  
  
 有关**参数**对象， **NumericScale**属性为读/写。  
  
 有关**字段**对象， **NumericScale**是通常是只读的。 但是，新对于**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)， **NumericScale**为读/写之后才[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定的数据提供程序已经成功地添加新和**字段**通过调用[更新](../../../ado/reference/ado-api/update-method.md)方法[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[字段对象](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>另请参阅  
 [NumericScale 和精度属性示例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和精度属性示例 （VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [精度属性 (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)

