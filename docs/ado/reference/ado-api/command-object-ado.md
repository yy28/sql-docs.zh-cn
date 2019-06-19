---
title: 命令对象 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 089a261eaea2701354af6082827c12491810b74c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699002"
---
# <a name="command-object-ado"></a>命令对象 (ADO)
定义要对数据源执行的特定命令。  
  
## <a name="remarks"></a>备注  
 使用**命令**对象来查询数据库，并返回中的记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，以执行大容量操作，或处理数据库的结构。 一些具体的提供程序的功能取决于**命令**集合、 方法或属性被引用时，可能会生成错误。  
  
 使用集合、 方法和属性的**命令**对象，您可以执行以下操作：  
  
-   定义可执行命令 （例如，SQL 语句） 的文本[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性。 或者，对于命令或查询结构简单以外的字符串 （例如，XML 模板查询） 定义与命令[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性。  
  
-   （可选） 指示使用的命令方言**CommandText**或**CommandStream**与[方言](../../../ado/reference/ado-api/dialect-property.md)属性。  
  
-   定义参数化的查询或存储过程参数以及[参数](../../../ado/reference/ado-api/parameter-object.md)对象和[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
-   指示是否应将参数名称传递给提供程序[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)属性。  
  
-   执行命令并返回**记录集**对象，如果具有相应[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
-   指定的命令的类型[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性，然后执行以优化性能。  
  
-   提供程序是否保存之前使用执行该命令的准备就绪 （或已编译） 版本控制[已准备](../../../ado/reference/ado-api/prepared-property-ado.md)属性。  
  
-   设置提供程序将等待命令执行使用的秒数[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)属性。  
  
-   将与打开的连接相关联**命令**对象通过设置其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。  
  
-   设置[名称](../../../ado/reference/ado-api/name-property-ado.md)属性来标识**命令**作为关联的方法的对象[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
-   传递**命令**对象传递给[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性**记录集**获取数据。  
  
-   访问使用特定于提供程序的特性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  若要执行的查询，而无需使用**命令**对象，请将传递到查询字符串[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法**连接**对象或设置为[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)的方法**记录集**对象。 但是，**命令**对象是必需的当你想要保留的命令文本并重新执行它，或使用查询参数。  
  
 若要创建**命令**独立于以前定义的对象**连接**对象，设置其**ActiveConnection**属性设置为有效的连接字符串。 仍会 ADO**连接**对象，但它不会分配该对象到对象变量。 但是，如果将多个相关联**命令**对象具有相同的连接，应显式创建并打开**连接**对象; 此分配**连接**给对象变量的对象。 请确保**连接**对象已成功打开，您将其分配给之前**ActiveConnection**属性**命令**对象，因为分配关闭**连接**对象会导致错误。 如果未设置**ActiveConnection**的属性**命令**对象传递给此对象变量，创建一个新的 ADO**连接**每个对象**命令**对象，即使使用相同的连接字符串。  
  
 若要执行**命令**，通过调用其[名称](../../../ado/reference/ado-api/name-property-ado.md)关联的属性**连接**对象。 **命令**必须具有其**ActiveConnection**属性设置为**连接**对象。 如果**命令**有参数，将其值作为参数传递给该方法。  
  
 如果两个或多个**命令**对象执行相同的连接，并在**命令**对象是具有输出参数的存储的过程发生错误。 执行每个**命令**对象，使用不同的连接或断开所有其他**命令**从连接的对象。  
  
 **参数**集合是的默认成员**命令**对象。 因此，以下两个代码语句是等效的。  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **命令**对象不是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [命令对象属性、 方法和事件](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
