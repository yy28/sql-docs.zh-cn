---
title: 使用数据库邮件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 232ea094ac81badfe7a6ec378371b55a0b08103b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62518738"
---
# <a name="using-database-mail"></a>使用数据库邮件
  在 SMO 中，数据库邮件子系统由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 属性引用的 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 对象表示。 使用 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 对象，可以配置数据库邮件子系统并管理配置文件和邮件帐户。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 对象属于 `Server` 对象，也就是说，邮件帐户的作用域处于服务器级别。  
  
## <a name="examples"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual Studio.NET 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
 有关程序使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库邮件，必须包括`Imports`语句以限定该邮件命名空间。 请在应用程序的其他 `Imports` 语句之后、任何声明之前插入该语句，例如：  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>使用 Visual Basic 创建数据库邮件帐户  
 此代码示例说明如何在 SMO 中创建电子邮件帐户。 数据库邮件由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 对象表示，并由 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Server> 属性引用。 SMO 可用于以编程方式配置数据库邮件，但它无法用于发送或处理收到的电子邮件。  
  
 VB.NET  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMail1](SMO How to#SMO_VBMail1)]  -->  
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>使用 Visual C# 创建数据库邮件帐户  
 此代码示例说明如何在 SMO 中创建电子邮件帐户。 数据库邮件由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 对象表示，并由 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Server> 属性引用。 SMO 可用于以编程方式配置数据库邮件，但它无法用于发送或处理收到的电子邮件。  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>使用 PowerShell 创建数据库邮件帐户  
 此代码示例说明如何在 SMO 中创建电子邮件帐户。 数据库邮件由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 对象表示，并由 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Server> 属性引用。 SMO 可用于以编程方式配置数据库邮件，但它无法用于发送或处理收到的电子邮件。  
  
 PowerShell  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
