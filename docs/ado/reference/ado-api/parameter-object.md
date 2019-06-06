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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 152186c0bb1c2fb75197a920e06e0b6bb96dadd0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703316"
---
# <a name="parameter-object"></a>Parameter 对象
表示参数或参数与相关联[命令](../../../ado/reference/ado-api/command-object-ado.md)对象基于参数化的查询或存储的过程。  
  
## <a name="remarks"></a>备注  
 很多提供程序支持参数化的命令。 这些是在其中一次，定义所需的操作的命令，但使用变量 （或参数） 来更改该命令的一些详细信息。 例如，一个 SQL SELECT 语句可以使用一个参数定义的匹配条件的 WHERE 子句，另一个用于定义排序依据子句的列名称。  
  
 **参数**对象表示与参数化查询关联的参数或输入/输出参数和返回值的存储过程。 具体取决于提供程序、 一些集合、 方法或属性的功能**参数**对象可能不可用。  
  
 使用集合、 方法和属性的**参数**对象，您可以执行以下操作：  
  
-   设置或返回与参数的名称[名称](../../../ado/reference/ado-api/name-property-ado.md)属性。  
  
-   设置或返回与参数的值[值](../../../ado/reference/ado-api/value-property-ado.md)属性。 **值**是默认属性**参数**对象。  
  
-   设置或返回与参数特征[特性](../../../ado/reference/ado-api/attributes-property-ado.md)，[方向](../../../ado/reference/ado-api/direction-property.md)，[精度](../../../ado/reference/ado-api/precision-property-ado.md)， [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)， [大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)，并[类型](../../../ado/reference/ado-api/type-property-ado.md)属性。  
  
-   将长二进制或字符数据传递给参数[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法。  
  
-   通过使用访问特定于提供程序的特性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 如果知道名称，并与关联的属性的参数的存储的过程或参数化的查询你想要调用，可以使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法来创建**参数**对象使用相应的属性设置和使用[追加](../../../ado/reference/ado-api/append-method-ado.md)方法将其添加到[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 这样就可以设置和返回参数值，而无需致电[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法**参数**集合来检索参数信息从提供程序，可能会占用大量资源的操作。  
  
 **参数**对象不是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [参数对象属性、 方法和事件](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
