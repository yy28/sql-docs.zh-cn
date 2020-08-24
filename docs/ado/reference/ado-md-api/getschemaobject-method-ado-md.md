---
description: GetSchemaObject 方法 (ADO MD)
title: GetSchemaObject 方法 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: rothja
ms.author: jroth
ms.openlocfilehash: b0a54b02cf748d8ff1144e50e3531295dbfe8c55
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778116"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 方法 (ADO MD)
通过[UniqueName](./uniquename-property-ado-md.md) ([维度](./dimension-object-ado-md.md)、[层次结构](./hierarchy-object-ado-md.md)、[级别](./level-object-ado-md.md)或[成员](./member-object-ado-md.md)) 检索 ADO MD 架构对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>parameters  
 *ObjType*  
 [SchemaObjectTypeEnum](./schemaobjecttypeenum.md)值，指定要检索的架构对象 (维度、层次结构、级别或成员) 的类型。  
  
 *UniqueName*  
 一个 **字符串** ，指定要检索的对象的 **UniqueName** 属性值。  
  
## <a name="remarks"></a>备注  
 **GetSchemaObject** 使用其唯一名称（由 **UniqueName** 属性指定）检索对象。 父对象的名称无需知道，并且无需填充父集合即可检索架构对象。  
  
## <a name="applies-to"></a>适用于  
 [CubeDef 对象 (ADO MD)](./cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 对象 (ADO MD)](./cubedef-object-ado-md.md)