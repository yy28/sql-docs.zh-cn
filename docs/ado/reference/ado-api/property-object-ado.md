---
title: "属性对象 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Property
helpviewer_keywords: Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0ffca466a4803e6dbf8817d4f7ad5c819cb0d46
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="property-object-ado"></a>属性对象 (ADO)
表示由提供程序定义的 ADO 对象的动态特性。  
  
## <a name="remarks"></a>注释  
 ADO 对象有两种类型的属性： 内置和动态。  
  
 内置属性是这些属性在 ADO 中实现，并立即可供任何新对象，请使用`MyObject.Property`语法。 它们不显示为**属性**中对象的对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，因此尽管您可以更改其值，但不能修改其特征。  
  
 动态属性定义的基础数据提供程序，并显示在**属性**为适当的 ADO 对象的集合。 例如，特定于所提供的属性可能指示如果[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象支持事务或更新。 这些附加属性将显示为**属性**中的对象**记录集**对象的**属性**集合。 动态属性可以引用该集合，只能通过使用`MyObject.Properties(0)`或`MyObject.Properties("Name")`语法。  
  
 无法删除这两种属性。  
  
 动态**属性**对象具有自己的四个内置属性：  
  
-   [名称](../../../ado/reference/ado-api/name-property-ado.md)属性是一个字符串，标识的属性。  
  
-   [类型](../../../ado/reference/ado-api/type-property-ado.md)属性是一个整数，指定的属性数据类型。  
  
-   [值](../../../ado/reference/ado-api/value-property-ado.md)属性是一个包含属性设置的变量。 **值**为默认属性**属性**对象。  
  
-   [属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性是一个长值，指示特征的特定于所提供的属性。  
  
 本部分包含以下主题。  
  
-   [属性对象属性、 方法和事件](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [字段对象](../../../ado/reference/ado-api/field-object.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
