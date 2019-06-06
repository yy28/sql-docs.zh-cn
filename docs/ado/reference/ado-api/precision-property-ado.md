---
title: Precision 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 59bfebe5885d0f18811b6b6c8df0f12634ed316f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703247"
---
# <a name="precision-property-ado"></a>Precision 属性 (ADO)
指示中数值的精度的程度[参数](../../../ado/reference/ado-api/parameter-object.md)对象或对数值[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字节**值，该值指示用于表示值的最大位数。  
  
## <a name="remarks"></a>备注  
 使用**精度**属性来确定用于表示数值的值的最大位数**参数**或**字段**对象。  
  
 值为读/写 on**参数**对象。  
  
 有关**字段**对象，**精度**是通常是只读的。 但是，新对于**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)，**精度**为读/写仅后[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定并且数据提供程序已成功添加新**字段**通过调用[更新](../../../ado/reference/ado-api/update-method.md)的方法**字段**集合。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>请参阅  
 [NumericScale 和 Precision 属性示例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 属性示例 （VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 属性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
