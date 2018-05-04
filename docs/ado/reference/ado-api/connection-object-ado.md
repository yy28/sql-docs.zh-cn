---
title: 连接对象 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba405d7993c5f9c327d5789cfa3bf3c9ccfba2b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connection-object-ado"></a>连接对象 (ADO)
表示与数据源的开放连接。  
  
## <a name="remarks"></a>注释  
 A**连接**对象表示与数据源的唯一会话。 在客户端/服务器数据库系统中，它可能等效于与服务器的实际网络连接。 具体取决于提供程序、 一些集合、 方法或属性的支持的功能**连接**对象可能不可用。  
  
 使用集合、 方法和属性的**连接**对象，你可以执行以下操作：  
  
-   配置连接，然后打开其与[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)， [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)，和[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性。 **ConnectionString**是默认属性**连接**对象。  
  
-   设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为客户端来调用[Microsoft 游标服务用于 OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)，后者支持批量更新。  
  
-   设置与连接的默认数据库[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)属性。  
  
-   在与连接打开的事务的隔离级别的组[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)属性。  
  
-   指定的 OLE DB 提供程序与[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性。  
  
-   建立，并在更高版本发生中断，具有的数据源的物理连接[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)和[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   具有连接上执行命令[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法和配置与执行[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)属性。  
  
    > [!NOTE]
    >  若要执行而无需使用命令对象的查询，查询将字符串传递给**执行**方法**连接**对象。 但是，[命令](../../../ado/reference/ado-api/command-object-ado.md)对象是必需的当你想要保留的命令文本并重新执行它，或使用查询参数。  
  
-   管理上打开的连接，如果使用的提供程序支持，包括嵌套的事务的事务[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)， [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)，和[不](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法与[属性](../../../ado/reference/ado-api/attributes-property-ado.md)属性。  
  
-   检查从数据源返回的错误[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
-   从与一起使用的 ADO 实现读取版本[版本](../../../ado/reference/ado-api/version-property-ado.md)属性。  
  
-   获取有关与数据库的架构信息[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法。  
  
 你可以创建**连接**独立于任何其他以前定义的对象的对象。  
  
 就像它们是本机方法上，你可以执行命名的命令或存储的过程**连接**对象，如在下一部分中所示。 当命名的命令具有与同名的存储过程时，在调用"的本机方法调用"**连接**对象始终执行命名的命令而不是存储过程。  
  
> [!NOTE]
>  不使用此功能 (就像它是上的本机方法调用的已命名的命令或存储的过程**连接**对象) 在 Microsoft®.NET Framework 应用程序，因为功能相冲突的基础实现与.NET Framework 与 com。 互操作  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>作为一个连接对象的本机方法执行命令  
 若要执行命令，提供以下命令名称使用**命令**对象[名称](../../../ado/reference/ado-api/name-property-ado.md)属性。 设置**ActiveConnection**属性**命令**连接到的对象。 然后发出的语句，则使用的命令名称，就像它是一种方法上**连接**对象后, 跟任何参数，和一个**记录集**对象如果返回任何行。 设置**记录集**属性，以自定义生成**记录集**。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>作为一个连接对象的本机方法执行存储的过程  
 若要执行存储的过程，就像它是一种方法在其中使用存储的过程名称语句发出**连接**对象后, 跟任何参数。 ADO 将进行"最佳猜测"的参数类型。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **连接**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [连接对象的属性、 方法和事件](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
