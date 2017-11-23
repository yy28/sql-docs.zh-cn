---
title: "在 SMO 中配置 SQL Server |Microsoft 文档"
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
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 80eb1df239768a6af53722977d2047c4f65cb9a1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configuring-sql-server-in-smo"></a>在 SMO 中配置 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在 SMO 中，<xref:Microsoft.SqlServer.Management.Smo.Information>对象，<xref:Microsoft.SqlServer.Management.Smo.Settings>对象，<xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象，与<xref:Microsoft.SqlServer.Management.Smo.Configuration>对象包含的实例的设置和信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具有许多描述已安装的实例的行为的属性。 这些属性描述了启动选项、服务器默认值、文件和目录、系统和处理器信息、产品和版本、连接信息、内存选项、语言和排序规则选择以及身份验证模式。  
  
## <a name="sql-server-configuration"></a>SQL Server 配置  
 <xref:Microsoft.SqlServer.Management.Smo.Information>对象属性包含的实例的有关信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，如处理器和平台。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Settings>对象属性包含的实例的有关信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 除邮件配置文件和服务器帐户之外，还可以修改默认的数据库文件和目录。 这些属性在连接持续时间内一直保留。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象属性包含与算术、ANSI 标准和事务相关的当前连接行为的相关信息。  
  
 没有配置选项表示一组<xref:Microsoft.SqlServer.Management.Smo.Configuration>对象。 它包含表示可通过 **sp_configure** 存储过程进行修改的选项的一组属性。 选项如**Priority Boost**，**恢复间隔**和**网络数据包大小**控制的实例的性能[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 其中的许多选项可以进行动态更改，但在某些情况下，其值需要先配置，在重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例后才发生更改。  
  
 没有<xref:Microsoft.SqlServer.Management.Smo.Configuration>对象每个配置选项的属性。 使用 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 对象，可以修改全局配置设置。 许多属性都有最大值和最小值，这些值也存储为 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 属性。 这些属性需要<xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A>方法以将更改提交到的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 中的配置选项的所有<xref:Microsoft.SqlServer.Management.Smo.Configuration>对象必须由系统管理员更改。  
  
## <a name="examples"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[创建 Visual C &#35;Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>在 Visual Basic 中修改 SQL Server 配置选项  
 此代码示例说明如何在 Visual Basic .NET 中更新配置选项。 它还检索并显示指定配置选项的最大值和最小值的相关信息。 最后，程序会通知用户如果动态，进行更改，或之前的实例存储[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]重新启动。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display all the configuration options.
Dim p As ConfigProperty
For Each p In srv.Configuration.Properties
    Console.WriteLine(p.DisplayName)
Next
Console.WriteLine("There are " & srv.Configuration.Properties.Count.ToString & " configuration options.")
'Display the maximum and minimum values for ShowAdvancedOptions.
Dim min As Integer
Dim max As Integer
min = srv.Configuration.ShowAdvancedOptions.Minimum
max = srv.Configuration.ShowAdvancedOptions.Maximum
Console.WriteLine("Minimum and Maximum values are " & min & " and " & max & ".")
'Modify the value of ShowAdvancedOptions and run the Alter method.
srv.Configuration.ShowAdvancedOptions.ConfigValue = 0
srv.Configuration.Alter()
'Display when the change takes place according to the IsDynamic property.
If srv.Configuration.ShowAdvancedOptions.IsDynamic = True Then
    Console.WriteLine("Configuration option has been updated.")
Else
    Console.WriteLine("Configuration option will be updated when SQL Server is restarted.")
End If
``` 
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>在 Visual Basic 中修改 SQL Server 设置  
 下面的代码示例显示的实例的有关信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中<xref:Microsoft.SqlServer.Management.Smo.Information>和<xref:Microsoft.SqlServer.Management.Smo.Settings>，并修改中的设置<xref:Microsoft.SqlServer.Management.Smo.Settings>和<xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象属性。  
  
 在此示例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象都有一个 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 你可以运行<xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>这些方法单独。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display information about the instance of SQL Server in Information and Settings.
Console.WriteLine("OS Version = " & srv.Information.OSVersion)
Console.WriteLine("State = " & srv.Settings.State.ToString)
'Display information specific to the current user in UserOptions.
Console.WriteLine("Quoted Identifier support = " & srv.UserOptions.QuotedIdentifier)
'Modify server settings in Settings.

srv.Settings.LoginMode = ServerLoginMode.Integrated
'Modify settings specific to the current connection in UserOptions.
srv.UserOptions.AbortOnArithmeticErrors = True
'Run the Alter method to make the changes on the instance of SQL Server.
srv.Alter()
```
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>在 Visual C# 中修改 SQL Server 设置  
 下面的代码示例显示的实例的有关信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中<xref:Microsoft.SqlServer.Management.Smo.Information>和<xref:Microsoft.SqlServer.Management.Smo.Settings>，并修改中的设置<xref:Microsoft.SqlServer.Management.Smo.Settings>和<xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象属性。  
  
 在此示例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象都有一个 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 你可以运行<xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>这些方法单独。  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```csharp  
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>在 PowerShell 中修改 SQL Server 设置  
 下面的代码示例显示的实例的有关信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中<xref:Microsoft.SqlServer.Management.Smo.Information>和<xref:Microsoft.SqlServer.Management.Smo.Settings>，并修改中的设置<xref:Microsoft.SqlServer.Management.Smo.Settings>和<xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象属性。  
  
 在此示例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象都有一个 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 你可以运行<xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>这些方法单独。  
  
```powershell 
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>在 PowerShell 中修改 SQL Server 配置选项  
 此代码示例说明如何在 Visual Basic .NET 中更新配置选项。 它还检索并显示指定配置选项的最大值和最小值的相关信息。 最后，程序会通知用户如果动态，进行更改，或之前的实例存储[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]重新启动。  
  
```powershell 
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = get-item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {    
   "Configuration option has been updated."  
 }  
Else  
{  
    "Configuration option will be updated when SQL Server is restarted."  
}  
```  
  
  
