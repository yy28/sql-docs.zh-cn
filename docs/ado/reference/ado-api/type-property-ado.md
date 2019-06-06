---
title: 类型属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56e8e1eca3e57eba19f2dc17e3b1ec0eaa815594
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719024"
---
# <a name="type-property-ado"></a>Type 属性 (ADO)
指示的操作的类型或数据类型[参数](../../../ado/reference/ado-api/parameter-object.md)，[字段](../../../ado/reference/ado-api/field-object.md)，或[属性](../../../ado/reference/ado-api/property-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。  
  
## <a name="remarks"></a>备注  
 有关**参数**对象，**类型**属性为读/写。 对新**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)，**类型**后才为读/写[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定并且数据提供程序已成功添加新**域**通过调用[更新](../../../ado/reference/ado-api/update-method.md)的方法**字段**集合。  
  
 对于所有其他对象，**类型**属性是只读的。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [Type 属性示例 （字段） (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Type 属性示例 （属性） （VC + +）](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType 属性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 属性（ADO 流）](../../../ado/reference/ado-api/type-property-ado-stream.md)
