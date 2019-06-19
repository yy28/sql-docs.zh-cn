---
title: 属性对象 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: af077c1606148eacb4f93ba6cfb52c3bb5eeefce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702944"
---
# <a name="property-object-ado"></a>属性对象 (ADO)
表示由提供程序定义的 ADO 对象的动态特征。  
  
## <a name="remarks"></a>备注  
 ADO 对象具有两种类型的属性： 内置和动态。  
  
 内置属性是这些属性在 ADO 中实现，并立即可用于任何新对象，请使用`MyObject.Property`语法。 它们不显示为**属性**对象中的对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，因此尽管您可以更改它们的值，您无法修改它们的特征。  
  
 动态属性定义的基础数据提供程序，并且显示在**属性**为适当的 ADO 对象的集合。 例如，可能表示特定于提供程序的属性，如果[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象支持的事务或更新。 这些附加属性将显示为**属性**对象中的**记录集**对象的**属性**集合。 动态属性可以引用仅遍历该集合，使用`MyObject.Properties(0)`或`MyObject.Properties("Name")`语法。  
  
 不能删除这两种属性。  
  
 动态**属性**对象都有其自己的四个内置属性：  
  
-   [名称](../../../ado/reference/ado-api/name-property-ado.md)属性是一个字符串，标识的属性。  
  
-   [类型](../../../ado/reference/ado-api/type-property-ado.md)属性是一个整数，指定属性数据类型。  
  
-   [值](../../../ado/reference/ado-api/value-property-ado.md)属性是变体，其中包含属性设置。 **值**是默认属性**属性**对象。  
  
-   [特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性是一个长值，指示属性特定于提供程序的特征。  
  
 本部分包含以下主题。  
  
-   [属性对象属性、 方法和事件](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [字段对象](../../../ado/reference/ado-api/field-object.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
