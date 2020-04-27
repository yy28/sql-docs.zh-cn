---
title: Property 对象（ADO） |Microsoft Docs
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
ms.openlocfilehash: 43bfa816a9ca8a93cdc1188a98e54d3e0d9111b1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917555"
---
# <a name="property-object-ado"></a>属性对象 (ADO)
表示由提供程序定义的 ADO 对象的动态特性。  
  
## <a name="remarks"></a>备注  
 ADO 对象具有两种类型的属性：内置和动态。  
  
 内置属性是在 ADO 中实现并使用`MyObject.Property`语法立即可用于任何新对象的属性。 它们不会在对象的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合中显示为**属性**对象，因此虽然您可以更改其值，但不能修改它们的特征。  
  
 动态属性由基础数据提供程序定义，并出现在相应 ADO 对象的**properties**集合中。 例如，特定于提供程序的属性可能指示[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象是否支持事务或更新。 这些附加属性将显示为该**记录集**对象的**属性**集合中的**属性**对象。 只能通过集合使用`MyObject.Properties(0)`或`MyObject.Properties("Name")`语法来引用动态属性。  
  
 不能删除任何一种属性。  
  
 动态**属性**对象具有自己的四个内置属性：  
  
-   [Name](../../../ado/reference/ado-api/name-property-ado.md)属性是用于标识属性的字符串。  
  
-   [Type](../../../ado/reference/ado-api/type-property-ado.md)属性是指定属性数据类型的整数。  
  
-   [值](../../../ado/reference/ado-api/value-property-ado.md)属性是包含属性设置的变量。 **值**是**属性**对象的默认属性。  
  
-   "[属性](../../../ado/reference/ado-api/attributes-property-ado.md)" 属性是一个 long 值，指示特定于提供程序的属性的特征。  
  
 本部分包含以下主题。  
  
-   [属性对象属性、方法和事件](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Command 对象（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [Connection 对象（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field 对象](../../../ado/reference/ado-api/field-object.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
