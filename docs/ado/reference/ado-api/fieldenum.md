---
description: FieldEnum
title: FieldEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: rothja
ms.author: jroth
ms.openlocfilehash: b562d480cfbebefdee82703e0c953854de07d064
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443739"
---
# <a name="fieldenum"></a>FieldEnum
指定 [记录](../../../ado/reference/ado-api/record-object-ado.md) 对象的 [fields](../../../ado/reference/ado-api/fields-collection-ado.md) 集合中引用的特殊字段。  
  
## <a name="remarks"></a>备注  
 这些常量提供了访问与 **记录**关联的特殊字段的 "快捷方式"。 从 "**字段**" 集合中检索[字段](../../../ado/reference/ado-api/field-object.md)对象，然后获取其内容和**字段**对象的[Value](../../../ado/reference/ado-api/value-property-ado.md)属性。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|引用包含与**记录**关联的默认[流](../../../ado/reference/ado-api/stream-object-ado.md)对象的字段。|  
|**adRecordURL**|-2|引用包含当前 **记录**的绝对 URL 字符串的字段。|
