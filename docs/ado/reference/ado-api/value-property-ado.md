---
title: Value 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 68bde5e78c746579bcb34166469569fb594c129f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710277"
---
# <a name="value-property-ado"></a>Value 属性 (ADO)

指示分配给的值[字段](../../../ado/reference/ado-api/field-object.md)，[参数](../../../ado/reference/ado-api/parameter-object.md)，或[属性](../../../ado/reference/ado-api/property-object-ado.md)对象。
  
## <a name="settings-and-return-values"></a>设置和返回值

设置或返回**变体**值，该值指示对象的值。 默认值取决于[类型](../../../ado/reference/ado-api/type-property-ado.md)属性。
  
## <a name="remarks"></a>备注

使用**值**属性来设置或返回数据自**字段**对象，若要设置或返回参数值替换**参数**对象，或者要设置或返回与属性设置**属性**对象。 是否**值**属性为读/写或只读取决于多种因素。 请参阅各自的对象主题以了解更多信息。

ADO 允许设置和返回长度的二进制数据与**值**属性。
  
> [!NOTE]
> 有关**参数**对象，ADO 读取**值**属性一次只能从提供程序。 如果某个命令包含**参数**其**值**属性为空，并且创建[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)命令，请确保先关闭**记录集**检索之前**值**属性。 否则为对于某些提供程序**值**属性可能为空，并且不会包含正确的值。
> 
> 对新**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，**值**属性必须设置在任何其他前**字段**可以指定属性。 首先，为特定值**值**属性必须具有已分配和[更新](../../../ado/reference/ado-api/update-method.md)上**字段**名集合。 然后，其他属性，如[类型](../../../ado/reference/ado-api/type-property-ado.md)或[属性](../../../ado/reference/ado-api/attributes-property-ado.md)可访问。
  
## <a name="applies-to"></a>适用范围
  
||||  
|-|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>请参阅

[值属性示例 (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)
[值属性示例 （VC + +）](../../../ado/reference/ado-api/value-property-example-vc.md) 
