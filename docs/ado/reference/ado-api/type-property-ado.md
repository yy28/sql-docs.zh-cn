---
title: 类型属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a0557dff957b71c601acbfbe0776fe39d979856
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="type-property-ado"></a>类型属性 (ADO)
指示的操作的类型或数据类型[参数](../../../ado/reference/ado-api/parameter-object.md)，[字段](../../../ado/reference/ado-api/field-object.md)，或[属性](../../../ado/reference/ado-api/property-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。  
  
## <a name="remarks"></a>注释  
 有关**参数**对象，**类型**属性为读/写。 新**字段**已追加到的对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)，**类型**仅次于为读/写[值](../../../ado/reference/ado-api/value-property-ado.md)属性**字段**已指定的数据提供程序已经成功地添加新和**字段**通过调用[更新](../../../ado/reference/ado-api/update-method.md)方法**字段**集合。  
  
 对于所有其他对象，**类型**属性是只读的。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[字段对象](../../../ado/reference/ado-api/field-object.md)|[参数对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [类型属性示例 （字段） (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [类型属性示例 （属性） （VC + +）](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType 属性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 属性（ADO 流）](../../../ado/reference/ado-api/type-property-ado-stream.md)
