---
title: "FieldStatusEnum |Microsoft 文档"
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
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33ea3379808e818b1afd723ce9223858896ea709
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="fieldstatusenum"></a>FieldStatusEnum
指定[状态](../../../ado/reference/ado-api/status-property-ado-field.md)的[字段对象](../../../ado/reference/ado-api/field-object.md)。  
  
 **AdFieldPending\*** 值指示导致状态是一组，并可配合其他状态的值的操作。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|指示指定的字段已存在。|  
|**adFieldBadStatus**|12|指示从 ADO 发送无效的状态值，OLE DB 访问接口。 可能的原因包括 OLE DB 1.0 或 1.1 提供程序或组合不正确的[值](../../../ado/reference/ado-api/value-property-ado.md)和[状态](../../../ado/reference/ado-api/status-property-ado-field.md)。|  
|**adFieldCannotComplete**|20|指示指定的 URL 的服务器[源](../../../ado/reference/ado-api/source-property-ado-record.md)无法完成该操作。|  
|**adFieldCannotDeleteSource**|23|指示在移动操作，树或子树已移到新位置，但无法删除源。|  
|**adFieldCantConvertValue**|2|指示的字段不能检索或存储而不会丢失数据。|  
|**adFieldCantCreate**|7|指示由于提供程序超过了限制 （如字段允许的数量），可能不添加字段。|  
|**adFieldDataOverflow**|6|指示从提供程序返回的数据溢出字段的数据类型。|  
|**adFieldDefault**|13|指示设置数据时，使用该字段的默认值。|  
|**adFieldDoesNotExist**|16|指示指定的字段不存在。|  
|**adFieldIgnore**|15|指示在源中设置数据值时跳过此字段。 提供程序设置任何值。|  
|**adFieldIntegrityViolation**|10|指示不能修改字段，因为它是计算或派生的实体。|  
|**adFieldInvalidURL**|17|指示数据源 URL 包含无效字符。|  
|**adFieldIsNull**|3|指示提供程序返回了类型 VT_NULL 的变体值和字段不为空。|  
|**adFieldOK**|0|默认值。 指示已成功添加或删除字段。|  
|**adFieldOutOfSpace**|22|指示提供程序无法获取足够的存储空间来完成移动或复制操作。|  
|**adFieldPendingChange**|0x40000|指示字段具有已删除并随后重新添加，可能具有不同的数据类型，或以前状态的字段的值的**adFieldOK**已更改。 将修改的字段的最终形式[字段](../../../ado/reference/ado-api/fields-collection-ado.md)后的集合[更新](../../../ado/reference/ado-api/update-method.md)调用方法。|  
|**adFieldPendingDelete**|0x20000|指示**删除**操作导致要设置的状态。 字段已标记为删除**字段**后的集合**更新**调用方法。|  
|**adFieldPendingInsert**|0x10000|指示**追加**操作导致要设置的状态。 **字段**标记为要添加到**字段**后的集合**更新**调用方法。|  
|**adFieldPendingUnknown**|0x80000|指示提供程序无法确定要设置哪些操作导致字段状态。|  
|**adFieldPendingUnknownDelete**|0x100000|指示提供程序不能确定哪个操作导致要设置的字段状态和字段，将删除从**字段**后的集合**更新**调用方法。|  
|**adFieldPermissionDenied**|9|指示不能修改字段，因为它被定义为只读的。|  
|**adFieldReadOnly**|24|指示数据源中的字段定义为只读。|  
|**adFieldResourceExists**|19|指示提供程序无法执行该操作，因为在目标 URL 已存在的对象，并且不能以覆盖该对象。|  
|**adFieldResourceLocked**|18|指示提供程序无法执行该操作，因为数据源已被一个或多个其他应用程序或进程锁定。|  
|**adFieldResourceOutOfScope**|25|表示源或目标的 URL 的当前记录的作用域之外。|  
|**adFieldSchemaViolation**|11|指示值违反了该字段的数据源架构约束。|  
|**adFieldSignMismatch**|5|指示提供程序返回的数据值已签名，但 ADO 字段值的数据类型是无符号。|  
|**adFieldTruncated**|4|指示从数据源读取数据时，可变长度数据已被截断。|  
|**adFieldUnavailable**|8|指示提供程序无法从数据源读取数据时确定的值。 例如，刚刚创建的行、 列的默认值不可用，和一个新的值未尚未指定一样。|  
|**adFieldVolumeNotFound**|21|指示提供程序是找不到的 URL 所示的存储卷。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [状态属性 （ADO 字段）](../../../ado/reference/ado-api/status-property-ado-field.md)

