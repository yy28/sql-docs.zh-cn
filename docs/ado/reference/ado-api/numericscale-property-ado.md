---
title: NumericScale 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38d283e8fedb90ed5a99143090bc6a077efa8512
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932109"
---
# <a name="numericscale-property-ado"></a>NumericScale 属性 (ADO)
指示中的数值小数位数[参数](../../../ado/reference/ado-api/parameter-object.md)或[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字节**值，该值指示的哪些数字值的小数位数将被解析。  
  
## <a name="remarks"></a>备注  
 使用**NumericScale**属性来确定将使用小数点右侧的位数来表示数字的值**参数**或**字段**对象。  
  
 有关**参数**对象， **NumericScale**属性为读/写。  
  
 有关**字段**对象， **NumericScale**是通常是只读的。 但是，新对于**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)， **NumericScale**为读/写之后才[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定并且数据提供程序已成功添加新**字段**通过调用[更新](../../../ado/reference/ado-api/update-method.md)方法[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[字段对象](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>请参阅  
 [NumericScale 和 Precision 属性示例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 属性示例 （VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Precision 属性 (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
