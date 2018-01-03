---
title: "参数对象 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Parameter
helpviewer_keywords: Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf234fd6cee37c525533bc082f4ae6c41a7b23f6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="parameter-object"></a>Parameter 对象
表示参数或参数与关联[命令](../../../ado/reference/ado-api/command-object-ado.md)对象基于参数化的查询或存储的过程。  
  
## <a name="remarks"></a>Remarks  
 许多提供程序支持参数化的命令。 这些是在其中一次，定义所需的操作的命令，但变量 （或参数） 用于更改该命令的某些详细信息。 例如，一个 SQL SELECT 语句可以使用一个参数定义的 WHERE 子句，另一个用于定义的排序依据子句的列名称的匹配条件。  
  
 **参数**对象表示与参数化查询，关联的参数或输入/输出参数和返回值的存储过程。 具体取决于提供程序、 一些集合、 方法或属性的功能**参数**对象可能不可用。  
  
 使用集合、 方法和属性的**参数**对象，你可以执行以下操作：  
  
-   设置或返回的参数的名称[名称](../../../ado/reference/ado-api/name-property-ado.md)属性。  
  
-   设置或返回与参数的值[值](../../../ado/reference/ado-api/value-property-ado.md)属性。 **值**是默认属性**参数**对象。  
  
-   设置或返回与参数特征[属性](../../../ado/reference/ado-api/attributes-property-ado.md)，[方向](../../../ado/reference/ado-api/direction-property.md)，[精度](../../../ado/reference/ado-api/precision-property-ado.md)， [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)， [大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)，和[类型](../../../ado/reference/ado-api/type-property-ado.md)属性。  
  
-   将长二进制或字符数据传递给参数[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法。  
  
-   通过使用访问提供程序特定属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 如果你知道名称和属性的参数与关联的存储的过程或参数化的查询你想要调用，可使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法来创建**参数**对象相应的属性设置和使用[追加](../../../ado/reference/ado-api/append-method-ado.md)方法以将其添加到[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 这样就可以设置和返回参数值，而无需调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法**参数**集合从提供程序，检索参数信息可能占用大量资源的操作。  
  
 **参数**对象不是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [参数对象属性、 方法和事件](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
