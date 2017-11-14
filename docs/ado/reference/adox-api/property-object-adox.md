---
title: "属性对象 (ADOX) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fa319e0fa981b3346232e3d3848bfdfe843d9f31
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="property-object-adox"></a>属性对象 (ADOX)
表示 ADOX 对象的特征。  
  
## <a name="remarks"></a>注释  
 ADOX 对象具有两种类型的属性： 内置和动态。  
  
 内置属性是立即可供任何新对象，使用 MyObject.Property 语法使用这些属性。 它们不会为属性对象的对象会显示[属性集合](../../../ado/reference/ado-api/properties-collection-ado.md)，因此，尽管您可以更改其值，但不能修改其特征。  
  
 动态属性定义的基础数据提供程序，并显示在相应的 ADOX 对象的属性集合。  动态属性可以引用只能通过使用 MyObject.Properties(0) 或 MyObject.Properties("Name") 语法的集合。  
  
 无法删除这两种属性。  
  
 动态属性对象具有自己的四个内置属性：  
  
 [名称](../../../ado/reference/ado-api/name-property-ado.md)属性是一个字符串，标识的属性。  
  
 [类型](../../../ado/reference/ado-api/type-property-ado.md)属性是一个整数，指定的属性数据类型。  
  
 [值](../../../ado/reference/ado-api/value-property-ado.md)属性是一个包含属性设置的变量。 值为属性对象的默认属性。  
  
 [属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性是一个长值，指示特征的特定于所提供的属性。  
  
 本部分包含以下主题。  
  
-   [ADOX 属性对象属性、 方法和事件](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)

