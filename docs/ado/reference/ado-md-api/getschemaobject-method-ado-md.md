---
title: "GetSchemaObject 方法 (ADO MD) |Microsoft 文档"
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
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f7dca37be4fdebaab7bb16f82086b01a90a3665
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 方法 (ADO MD)
检索 ADO MD 架构对象 ([维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)，或[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)) 通过其[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>语法  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *ObjType*  
 A [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md)值，该值指定哪种类型的架构对象 （维度、 层次结构、 级别或成员） 来检索。  
  
 *UniqueName*  
 A**字符串**指定**UniqueName**要检索的对象的属性值。  
  
## <a name="remarks"></a>注释  
 **GetSchemaObject**检索其唯一的名称，使用指定的对象**UniqueName**属性。 父对象的名称不必已知的也不需父集合填充，以便检索的架构对象。  
  
## <a name="applies-to"></a>适用范围  
 [CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
