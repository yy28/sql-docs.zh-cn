---
title: 连接对象 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 701ced4f5e0ad511f4a1c5b39c9775e285d1f751
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695786"
---
# <a name="connection-object-ado"></a>连接对象 (ADO)
表示与数据源的开放连接。  
  
## <a name="remarks"></a>备注  
 一个**连接**对象表示与数据源的唯一会话。 在客户端/服务器数据库系统中，它可能与实际的网络连接到服务器。 具体取决于提供程序、 一些集合、 方法或属性的支持的功能**连接**对象可能不可用。  
  
 使用集合、 方法和属性的**连接**对象，您可以执行以下操作：  
  
-   配置连接，然后打开其与[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)， [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)，并[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性。 **ConnectionString**是默认属性**连接**对象。  
  
-   设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为客户端来调用[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)，它支持批量更新。  
  
-   设置与连接的默认数据库[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)属性。  
  
-   设置与连接打开的事务的隔离级别[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)属性。  
  
-   指定 OLE DB 提供程序与[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性。  
  
-   建立，并在更高版本发生中断，与具有的数据源的物理连接[开放](../../../ado/reference/ado-api/open-method-ado-connection.md)并[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   与连接上执行命令[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法，并配置与执行[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)属性。  
  
    > [!NOTE]
    >  若要执行查询而无需使用命令对象时，将传递到查询字符串**Execute**方法**连接**对象。 但是，[命令](../../../ado/reference/ado-api/command-object-ado.md)对象是必需的当你想要保留的命令文本并重新执行它，或使用查询参数。  
  
-   管理打开的连接，如果使用的提供程序支持，包括嵌套的事务上的事务[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)， [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)，并[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法和[特性](../../../ado/reference/ado-api/attributes-property-ado.md)属性。  
  
-   检查从数据源返回的错误[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
-   从 ADO 实现用于读取版本[版本](../../../ado/reference/ado-api/version-property-ado.md)属性。  
  
-   获取有关与数据库的架构信息[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法。  
  
 您可以创建**连接**独立于任何其他以前定义的对象的对象。  
  
 它们就在本机方法，可以执行命名的命令或存储的过程**连接**对象，如在下一节中所示。 当命名的命令具有与同名的存储过程时，在调用"本机方法调用"**连接**对象始终执行而不是存储过程的命名的命令。  
  
> [!NOTE]
>  不使用此功能 (像本机方法上调用命名的命令或存储的过程**连接**对象) 在 Microsoft®.NET Framework 应用程序中，因为底层实现的功能冲突与的方式在.NET Framework com 互操作  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>为连接对象的本机方法执行命令  
 若要执行的命令，为该命令名称使用**命令**对象[名称](../../../ado/reference/ado-api/name-property-ado.md)属性。 设置**ActiveConnection**的属性**命令**连接到的对象。 然后，发出它就在一种方法使用此命令名称的语句**连接**对象后, 跟任何参数，和一个**记录集**对象如果返回任何行。 设置**记录集**属性，以自定义生成**记录集**。 例如：  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>为连接对象的本机方法执行存储的过程  
 若要执行存储的过程时，发出它就在一种方法使用此存储的过程名称的语句**连接**对象后, 跟任何参数。 ADO，将进行"最佳猜测"的参数类型。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **连接**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [连接对象的属性、 方法和事件](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
