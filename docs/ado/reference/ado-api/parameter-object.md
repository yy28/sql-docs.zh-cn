---
title: 参数对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: rothja
ms.author: jroth
ms.openlocfilehash: 22af5fadda96adbe67c1c03aaa5cde3527df1113
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759993"
---
# <a name="parameter-object"></a>Parameter 对象
表示基于参数化查询或存储过程与[命令](../../../ado/reference/ado-api/command-object-ado.md)对象关联的参数或参数。  
  
## <a name="remarks"></a>备注  
 许多提供程序都支持参数化命令。 这是一次定义所需操作的命令，但使用变量（或参数）来更改命令的某些详细信息。 例如，SQL SELECT 语句可以使用参数来定义 WHERE 子句的匹配条件，并使用另一个参数定义 SORT BY 子句的列名称。  
  
 **参数**对象表示与参数化查询关联的参数，或 in/out 参数和存储过程的返回值。 **参数**对象的某些集合、方法或属性可能不可用，具体取决于提供程序的功能。  
  
 使用**参数**对象的集合、方法和属性，可以执行以下操作：  
  
-   设置或返回具有[name](../../../ado/reference/ado-api/name-property-ado.md)属性的参数的名称。  
  
-   设置或返回[值](../../../ado/reference/ado-api/value-property-ado.md)属性为的参数的值。 **值**是**参数**对象的默认属性。  
  
-   设置或返回[属性](../../../ado/reference/ado-api/attributes-property-ado.md)、[方向](../../../ado/reference/ado-api/direction-property.md)、[精度](../../../ado/reference/ado-api/precision-property-ado.md)、 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)、[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)和[类型](../../../ado/reference/ado-api/type-property-ado.md)属性的参数特征。  
  
-   使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法将长二进制或字符数据传递给参数。  
  
-   使用[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合访问特定于提供程序的特性。  
  
 如果知道与要调用的存储过程或参数化查询相关联的参数的名称和属性，则可以使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法创建具有相应属性设置的**参数**对象，并使用[Append](../../../ado/reference/ado-api/append-method-ado.md)方法将它们添加到[parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 这使您可以设置和返回参数值，而无需对**Parameters**集合调用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法即可从提供程序中检索参数信息，这可能会占用大量资源。  
  
 **参数**对象对于脚本编写是不安全的。  
  
 本部分包含以下主题。  
  
-   [参数对象属性、方法和事件](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Command 对象（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 方法（ADO）](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters 集合（ADO）](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
