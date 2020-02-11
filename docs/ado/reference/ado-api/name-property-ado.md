---
title: Name 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a919bb377eee2da1c3c1a65e85ddfb9807ed8d50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918037"
---
# <a name="name-property-ado"></a>Name 属性 (ADO)
指示对象的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**字符串**值，该值指示对象的名称。  
  
## <a name="remarks"></a>备注  
 使用 "**名称**" 属性可以为命令、**属性**、**字段**或**参数**对象指定名称或检索**命令**的名称。  
  
 对于**Command**对象，值为读/写，对**属性**对象为只读。  
  
 对于**字段**对象，**名称**通常是只读的。 但是，对于已追加到[记录](../../../ado/reference/ado-api/record-object-ado.md)的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**字段**对象，在指定了**字段**的[值](../../../ado/reference/ado-api/value-property-ado.md)属性并且数据访问接口已通过调用**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法成功添加了新**字段**之后，**名称**是只读的。  
  
 对于尚未追加到[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合中的**参数**对象， **Name**属性为读/写。 对于追加**参数**对象和所有其他对象， **Name**属性是只读的。 名称在集合中不必是唯一的。  
  
 可以按序号引用检索对象的**Name**属性，之后可以按名称直接引用对象。 例如，如果`rstMain.Properties(20).Name`生成`Updatability`，则可以随后将此属性称为。 `rstMain.Properties("Updatability")`  
  
## <a name="applies-to"></a>应用于  
  
|||  
|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[字段对象](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter 对象](../../../ado/reference/ado-api/parameter-object.md)|[属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [特性和名称属性示例（VB）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [特性和名称属性示例（VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
