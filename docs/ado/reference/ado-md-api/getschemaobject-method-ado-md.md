---
title: GetSchemaObject 方法（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: a8853e967a75a67aadccc7e48d684ab92819a71d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764208"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 方法 (ADO MD)
通过[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)检索 ADO MD 架构对象（[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)、[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)、[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)或[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)）。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>参数  
 *ObjType*  
 一个[SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md)值，指定要检索的架构对象类型（维度、层次结构、级别或成员）。  
  
 *UniqueName*  
 一个**字符串**，指定要检索的对象的**UniqueName**属性值。  
  
## <a name="remarks"></a>备注  
 **GetSchemaObject**使用其唯一名称（由**UniqueName**属性指定）检索对象。 父对象的名称无需知道，并且无需填充父集合即可检索架构对象。  
  
## <a name="applies-to"></a>应用于  
 [CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
