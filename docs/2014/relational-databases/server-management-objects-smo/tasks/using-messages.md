---
title: 使用消息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e67d8818fb20d339c4166f606d15e0f7dbceced
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800580"
---
# <a name="using-messages"></a>使用消息
  在 SMO 中，系统消息由属于 `Server` 对象的 <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> 对象表示。 因为无法修改系统消息，所以 `SystemMessage` 对象属性为只读属性。  
  
 用户定义的消息在 SMO 中由 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> 对象以编程方式表示。 可通过循环访问该集合来发现现有的用户定义的消息。 可以通过实例化新的 `UserDefinedMessage` 对象并设置其相应的属性来创建新的用户定义的消息。  
  
## <a name="examples"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[在 Visual Studio.NET 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)并[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>在 Visual Basic 中查找特殊系统消息  
 此代码示例说明如何通过 ID 号标识系统消息并显示该消息。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMessages1](SMO How to#SMO_VBMessages1)]  -->  
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>在 Visual C# 中查找特殊系统消息  
 此代码示例说明如何通过 ID 号标识系统消息并显示该消息。  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference an existing system message using the   
            //ItemByIdAndLanguage method.   
            SystemMessage msg = default(SystemMessage);  
            msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
        }  
```  
  
## <a name="finding-a-particular-system-message-in-powershell"></a>在 PowerShell 中查找特殊系统消息  
 此代码示例说明如何通过 ID 号标识系统消息并显示该消息。  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>在 Visual Basic 中添加新的用户定义的消息  
 此代码示例说明如何使用大于 50000 的 ID 创建用户定义的消息。  
  
```  
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>在 Visual C# 中添加新的用户定义的消息  
 此代码示例说明如何使用大于 50000 的 ID 创建用户定义的消息。  
  
```  
{  
  
            Server mysrv = new Server();  
  
            UserDefinedMessage udm = new UserDefinedMessage(mysrv, 50030, "us_english",16, "Test message");  
            udm.Create();  
             UserDefinedMessage  msg = mysrv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
  
        }  
```  
  
## <a name="adding-a-new-user-defined-message-in-powershell"></a>在 PowerShell 中添加新的用户定义的消息  
 此代码示例说明如何使用大于 50000 的 ID 创建用户定义的消息。  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message  
  
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -argumentlist `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
  
  
