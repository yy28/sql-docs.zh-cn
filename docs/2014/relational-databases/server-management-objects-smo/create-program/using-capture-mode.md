---
title: 使用捕获模式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5195430b502873c79d3962270ffddd19121a5e62
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129197"
---
# <a name="using-capture-mode"></a>使用捕获模式
  SMO 程序可以捕获和记录该程序发出的等效 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，代替（或外加）该程序执行的语句。 通过使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象，或者通过使用 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Server> 属性，启用捕获模式。  
  
## <a name="example"></a>示例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="enabling-capture-mode-in-visual-basic"></a>在 Visual Basic 中启用捕获模式  
 此代码示例启用捕获模式，然后显示在捕获缓冲区中保存的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCapture1](SMO How to#SMO_VBCapture1)]  -->  
  
## <a name="enabling-capture-mode-in-visual-c"></a>在 Visual C# 中启用捕获模式  
 此代码示例启用捕获模式，然后显示在捕获缓冲区中保存的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
```  
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
  
  
