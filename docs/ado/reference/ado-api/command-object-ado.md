---
title: "命令对象 (ADO) |Microsoft 文档"
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
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 863c922dce68f5e3108136baf90ebc5a3d0b697a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="command-object-ado"></a>命令对象 (ADO)
定义要对数据源执行的特定命令。  
  
## <a name="remarks"></a>注释  
 使用**命令**对象，用于查询数据库并返回中的记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，来执行大容量操作，或操作数据库的结构。 一些具体的提供程序的功能取决于**命令**集合、 方法或属性会引用它们时，可能会生成错误。  
  
 使用集合、 方法和属性的**命令**对象，你可以执行以下操作：  
  
-   定义了一个命令 （例如，SQL 语句） 的可执行文本[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性。 或者，为命令或查询结构而非简单字符串 （例如，XML 模板查询） 定义该命令与[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性。  
  
-   （可选） 指示在中使用的命令方言**CommandText**或**CommandStream**与[方言](../../../ado/reference/ado-api/dialect-property.md)属性。  
  
-   定义参数化的查询或存储过程的参数[参数](../../../ado/reference/ado-api/parameter-object.md)对象和[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
-   指示是否应将参数名称传递给提供程序[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)属性。  
  
-   执行命令并返回**记录集**对象，如果代理与[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
-   指定的命令类型[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性，然后执行以优化性能。  
  
-   控制提供程序是否保存之前执行该命令的已准备的 （或已编译的） 版本[已准备](../../../ado/reference/ado-api/prepared-property-ado.md)属性。  
  
-   设置提供程序将等待要与执行的命令的秒数[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)属性。  
  
-   将关联的打开连接使用**命令**对象通过设置其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。  
  
-   设置[名称](../../../ado/reference/ado-api/name-property-ado.md)属性来标识**命令**作为关联的方法的对象[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
-   传递**命令**对象传递给[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性**记录集**获取数据。  
  
-   访问与提供程序特定属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  执行查询，而使用**命令**对象，查询将字符串传递给[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法**连接**对象或[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**对象。 但是，**命令**对象是必需的当你想要保留的命令文本并重新执行它，或使用查询参数。  
  
 若要创建**命令**独立于以前定义的对象**连接**对象，设置其**ActiveConnection**属性设置为有效的连接字符串。 ADO 仍会产生**连接**对象，但它不会给对象变量的分配该对象。 但是，如果您正在将关联多个**命令**对象相同的连接，你应显式创建并打开**连接**对象; 此分配**连接**给对象变量的对象。 请确保**连接**之前你将其分配给对象已成功打开**ActiveConnection**属性**命令**对象，因为分配关闭**连接**对象会导致错误。 如果你未设置**ActiveConnection**属性**命令**对象传递给此对象变量，ADO 创建一个新**连接**每个对象**命令**对象，即使使用相同的连接字符串。  
  
 若要执行**命令**，通过调用其[名称](../../../ado/reference/ado-api/name-property-ado.md)属性关联**连接**对象。 **命令**必须具有其**ActiveConnection**属性设置为**连接**对象。 如果**命令**具有参数，将其值作为参数传递给方法。  
  
 如果两个或多个**命令**对象执行相同的连接并**命令**对象是存储的过程与 output 参数，则会出错。 若要执行每个**命令**对象，请使用单独的连接或断开所有其他**命令**从连接的对象。  
  
 **参数**集合是的默认成员**命令**对象。 因此，下面的两个代码语句是等效的。  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **命令**对象不是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [命令对象属性、 方法和事件](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

