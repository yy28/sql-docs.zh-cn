---
title: "使用捕获模式 |Microsoft 文档"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
caps.latest.revision: "39"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5632d4e1c8df64ae77f9da90fecbc81f9244c7fa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="using-capture-mode"></a>使用捕获模式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SMO 程序在捕获并记录等效[!INCLUDE[tsql](../../../includes/tsql-md.md)]签发程序代替了，或也由程序执行的语句的语句。 通过使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象，或者通过使用 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Server> 属性，启用捕获模式。  
  
## <a name="example"></a>示例  
若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[创建 Visual C &#35;Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  

  
## <a name="enabling-capture-mode-in-visual-basic"></a>在 Visual Basic 中启用捕获模式  
 此代码示例启用捕获模式，然后显示在捕获缓冲区中保存的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Set the execution mode to CaptureSql for the connection.
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql
'Make a modification to the server that is to be captured.
srv.UserOptions.AnsiNulls = True
srv.Alter()
'Iterate through the strings in the capture buffer and display the captured statements.
Dim s As String
For Each s In srv.ConnectionContext.CapturedSql.Text
    Console.WriteLine(s)
Next
'Execute the captured statements.
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text)
'Revert to immediate execution mode. 
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql
```
  
## <a name="enabling-capture-mode-in-visual-c"></a>在 Visual C# 中启用捕获模式  
 此代码示例启用捕获模式，然后显示在捕获缓冲区中保存的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
```csharp  
{   
// Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
// Set the execution mode to CaptureSql for the connection.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql;   
// Make a modification to the server that is to be captured.   
srv.UserOptions.AnsiNulls = true;   
srv.Alter();   
// Iterate through the strings in the capture buffer and display the captured statements.   
string s;   
foreach ( String p_s in srv.ConnectionContext.CapturedSql.Text ) {   
   Console.WriteLine(p_s);   
}   
// Execute the captured statements.   
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text);   
// Revert to immediate execution mode.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
  
