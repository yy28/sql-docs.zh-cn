---
title: FieldStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1ba7fe546f7ac8e1a036fc8fe7e5f523ebf09d4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719209"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定[状态](../../../ado/reference/ado-api/status-property-ado-field.md)的[Field 对象](../../../ado/reference/ado-api/field-object.md)。  
  
 **AdFieldPending\*** 值指示该操作导致状态为设置，并可配合其他状态的值。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|指示指定的字段已存在。|  
|**adFieldBadStatus**|12|指示从 ADO 发送无效的状态值，到 OLE DB 访问接口。 可能的原因包括 OLE DB 1.0 或 1.1 提供程序或不正确的组合[值](../../../ado/reference/ado-api/value-property-ado.md)并[状态](../../../ado/reference/ado-api/status-property-ado-field.md)。|  
|**adFieldCannotComplete**|20|指示指定的 URL 的服务器[源](../../../ado/reference/ado-api/source-property-ado-record.md)无法完成该操作。|  
|**adFieldCannotDeleteSource**|23|表示移动操作期间将树或子树已移动到新位置，但不是会删除源。|  
|**adFieldCantConvertValue**|2|指示该字段不能检索或存储而不丢失数据。|  
|**adFieldCantCreate**|7|指示由于提供程序超过了限制 （如字段允许的数量） 不可以添加字段。|  
|**adFieldDataOverflow**|6|指示提供程序返回的数据溢出字段的数据类型。|  
|**adFieldDefault**|13|指示该字段的默认值已设置数据时使用。|  
|**adFieldDoesNotExist**|16|指示指定的字段不存在。|  
|**adFieldIgnore**|15|指示在源中设置数据值时跳过此字段。 提供程序设置任何值。|  
|**adFieldIntegrityViolation**|10|指示不能修改该字段，因为它是计算或派生的实体。|  
|**adFieldInvalidURL**|17|指示数据源 URL 包含无效字符。|  
|**adFieldIsNull**|3|指示提供程序返回 VT_NULL 类型的变体值和字段不为空。|  
|**adFieldOK**|0|默认值。 指示已成功添加或删除该字段。|  
|**adFieldOutOfSpace**|22|指示提供程序无法获取足够的存储空间来完成移动或复制操作。|  
|**adFieldPendingChange**|0x40000|指示的字段都有已删除，然后重新添加，可能具有不同的数据类型，或以前的状态有的字段的值的**adFieldOK**已更改。 将修改该字段的最终格式[字段](../../../ado/reference/ado-api/fields-collection-ado.md)后的集合[更新](../../../ado/reference/ado-api/update-method.md)调用方法。|  
|**adFieldPendingDelete**|0x20000|指示**删除**操作导致要设置的状态。 该字段已标记为删除从**字段**后的集合**更新**调用方法。|  
|**adFieldPendingInsert**|0x10000|指示**追加**操作导致要设置的状态。 **字段**标记为要添加到**字段**之后，集合**更新**调用方法。|  
|**adFieldPendingUnknown**|0x80000|指示提供程序不能确定要设置哪些操作导致字段状态。|  
|**adFieldPendingUnknownDelete**|0x100000|指示提供程序不能确定哪个操作所导致的字段状态设置，并将从删除字段**字段**后的集合**更新**调用方法。|  
|**adFieldPermissionDenied**|9|指示不能修改字段，因为它被定义为只读的。|  
|**adFieldReadOnly**|24|指示数据源中的字段定义为只读的。|  
|**adFieldResourceExists**|19|指示提供程序无法执行操作，因为在目标 URL 已存在的对象并不能以覆盖该对象。|  
|**adFieldResourceLocked**|18|指示提供程序无法执行操作，因为数据源已被一个或多个其他应用程序或进程锁定。|  
|**adFieldResourceOutOfScope**|25|指示源或目标 URL 超出了当前记录的范围。|  
|**adFieldSchemaViolation**|11|指示值违反了该字段的数据源架构约束。|  
|**adFieldSignMismatch**|5|指示提供程序返回的数据值带有符号，但 ADO 字段值的数据类型是无符号。|  
|**adFieldTruncated**|4|指示从数据源读取时可变长度数据已被截断。|  
|**adFieldUnavailable**|8|指示提供程序无法从数据源读取数据时确定的值。 例如，只需创建行、 列的默认值不可用，和一个新的值未尚未指定一样。|  
|**adFieldVolumeNotFound**|21|指示提供程序找不到的 URL 所示的存储卷。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [Status 属性（ADO 字段）](../../../ado/reference/ado-api/status-property-ado-field.md)
