---
title: Precision 属性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 26da0367e494bd74253b904393a2dad62308a608
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931631"
---
# <a name="precision-property-ado"></a>Precision 属性 (ADO)
指示[参数](../../../ado/reference/ado-api/parameter-object.md)对象或数值[字段](../../../ado/reference/ado-api/field-object.md)对象中数值的精度度。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**字节**值，该值指示用于表示值的最大位数。  
  
## <a name="remarks"></a>备注  
 使用 "**精度**" 属性可确定用于表示数值**参数**或**字段**对象的值的最大位数。  
  
 值在**参数**对象上是可读/写的。  
  
 对于**字段**对象，**精度**通常为只读。 但是，对于已附加到[记录](../../../ado/reference/ado-api/record-object-ado.md)的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**字段**对象，**精度**仅在指定了**字段**的[值](../../../ado/reference/ado-api/value-property-ado.md)属性并且数据提供程序已通过调用**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法成功添加了新**字段**之后才是只读的。  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>另请参阅  
 [NumericScale 和 Precision 属性示例（VB）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 属性示例（VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 属性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
