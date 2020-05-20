---
title: 连接对象（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 49a270f143e57c1e093ac94732b67b6424c88607
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760293"
---
# <a name="connection-object-ado"></a>连接对象 (ADO)
表示到数据源的连接是打开的。  
  
## <a name="remarks"></a>备注  
 **Connection**对象表示与数据源的唯一会话。 在客户端/服务器数据库系统中，它可能等效于到服务器的实际网络连接。 根据提供程序支持的功能，**连接**对象的某些集合、方法或属性可能不可用。  
  
 使用**连接**对象的集合、方法和属性，可以执行以下操作：  
  
-   在通过[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)、 [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)和[Mode](../../../ado/reference/ado-api/mode-property-ado.md)属性打开连接之前配置连接。 **ConnectionString**是**连接**对象的默认属性。  
  
-   将[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为 client，以调用支持批处理更新的[OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)。  
  
-   设置与[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)属性的连接的默认数据库。  
  
-   为在连接上打开的事务设置[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)属性的隔离级别。  
  
-   使用[provider](../../../ado/reference/ado-api/provider-property-ado.md)属性指定 OLE DB 提供程序。  
  
-   建立与数据源的物理连接，并将其与[开放式](../../../ado/reference/ado-api/open-method-ado-connection.md)和[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法一起断开。  
  
-   使用[execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法对连接执行命令，并使用[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)属性配置执行操作。  
  
    > [!NOTE]
    >  若要在不使用命令对象的情况下执行查询，请将查询字符串传递到**连接**对象的**execute**方法。 但是，当你想要保留命令文本并重新执行它，或使用查询参数时，需要使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
-   通过[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)、 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)和[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法和[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)属性，管理打开的连接的事务（包括嵌套事务，如果提供程序支持它们）。  
  
-   检查从数据源返回的[错误集合中的错误](../../../ado/reference/ado-api/errors-collection-ado.md)。  
  
-   从用于[version](../../../ado/reference/ado-api/version-property-ado.md)属性的 ADO 实现读取版本。  
  
-   通过[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法获取有关数据库的架构信息。  
  
 您可以独立于任何其他以前定义的对象创建**连接**对象。  
  
 可以执行命名的命令或存储过程，就像它们是**连接**对象上的本机方法一样，如下一节所示。 当命名命令与存储过程具有相同的名称时，对**连接**对象调用 "本机方法调用" 将始终执行命名的命令而不是存储过程。  
  
> [!NOTE]
>  在 Microsoft® .NET Framework 应用程序中，不要使用此功能（在**连接**对象上以本机方法的方式）调用此功能，因为该功能的基础实现与 .NET FRAMEWORK 与 COM 互操作的方式发生冲突。  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>将命令作为连接对象的本机方法执行  
 若要执行命令，请使用**命令**对象[名称](../../../ado/reference/ado-api/name-property-ado.md)属性为命令指定名称。 将**命令**对象的**ActiveConnection**属性设置为连接。 然后发出一个语句，其中使用命令名称，就像它是**连接**对象的方法，后跟任何参数，如果返回任何行，则使用**记录集**对象。 设置**记录集**属性以自定义生成的**记录集**。 例如：  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>作为连接对象的本机方法执行存储过程  
 若要执行存储过程，请发出一个语句，其中使用存储过程名称，就像它是**连接**对象上的方法，然后是任何参数一样。 ADO 将对参数类型进行 "最佳推测"。 例如：  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 **连接**对象对于脚本是安全的。  
  
 本部分包含以下主题。  
  
-   [连接对象属性、方法和事件](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Command 对象（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors 集合（ADO）](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 对象（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
