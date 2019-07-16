---
title: 属性对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b7911608970e9860d7eddcf3e83156ac99645c3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965399"
---
# <a name="property-object-adox"></a>属性对象 (ADOX)
表示 ADOX 对象的特征。  
  
## <a name="remarks"></a>备注  
 ADOX 对象具有两种类型的属性： 内置和动态。  
  
 内置属性是立即可供任何新的对象，使用 MyObject.Property 语法使用这些属性。 它们不会为中的对象的属性对象会出现[属性集合](../../../ado/reference/ado-api/properties-collection-ado.md)，因此，尽管可以更改它们的值，但不能修改它们的特征。  
  
 动态属性定义的基础数据提供程序，并显示相应的 ADOX 对象的属性集合。  只能通过集合，并使用 MyObject.Properties(0) 或 MyObject.Properties("Name") 语法，可以引用动态属性。  
  
 不能删除这两种属性。  
  
 动态属性对象具有其自己的四个内置属性：  
  
 [名称](../../../ado/reference/ado-api/name-property-ado.md)属性是一个字符串，标识的属性。  
  
 [类型](../../../ado/reference/ado-api/type-property-ado.md)属性是一个整数，指定属性数据类型。  
  
 [值](../../../ado/reference/ado-api/value-property-ado.md)属性是变体，其中包含属性设置。 值为属性对象的默认属性。  
  
 [特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性是一个长值，指示属性特定于提供程序的特征。  
  
 本部分包含以下主题。  
  
-   [ADOX 属性对象属性、方法和事件](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
