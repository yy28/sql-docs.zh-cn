---
title: 在 SMO 中配置 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13fc00425a12737000a6400c5b9368288de80aa3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797244"
---
# <a name="configuring-sql-server-in-smo"></a>在 SMO 中配置 SQL Server
  在 SMO 中， <xref:Microsoft.SqlServer.Management.Smo.Information>对象<xref:Microsoft.SqlServer.Management.Smo.Settings> 、对象、 <xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象<xref:Microsoft.SqlServer.Management.Smo.Configuration>和对象都包含实例的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置和信息。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具有许多描述已安装的实例的行为的属性。 这些属性描述了启动选项、服务器默认值、文件和目录、系统和处理器信息、产品和版本、连接信息、内存选项、语言和排序规则选择以及身份验证模式。  
  
## <a name="sql-server-configuration"></a>SQL Server 配置  
 <xref:Microsoft.SqlServer.Management.Smo.Information> 对象属性包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的相关信息，例如处理器和平台。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象属性包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的相关信息。 除邮件配置文件和服务器帐户之外，还可以修改默认的数据库文件和目录。 这些属性在连接持续时间内一直保留。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象属性包含与算术、ANSI 标准和事务相关的当前连接行为的相关信息。  
  
 还存在由 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 对象表示的一组配置选项。 它包含表示可通过 `sp_configure` 存储过程进行修改的选项的一组属性。 "**优先级提升**"、"**恢复间隔**" 和 "**网络数据包大小**" 等选项控制实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的性能。 其中的许多选项可以进行动态更改，但在某些情况下，其值需要先配置，在重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例后才发生更改。  
  
 每个配置选项都对应一个 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 对象属性。 使用 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 对象，可以修改全局配置设置。 许多属性都有最大值和最小值，这些值也存储为 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 属性。 这些属性要求<xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A>方法将更改提交到的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 对象中的所有配置选项都必须由系统管理员进行更改。  
  
## <a name="examples"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[在 Visual studio .net 中创建 VISUAL BASIC SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 visual Studio .Net 中创建 VISUAL C&#35; smo 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>在 Visual Basic 中修改 SQL Server 配置选项  
 此代码示例说明如何在 Visual Basic .NET 中更新配置选项。 它还检索并显示指定配置选项的最大值和最小值的相关信息。 最后，程序会通知用户是否已进行了动态更改，或者是否存储了更改直到重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例后再予以应用。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure2](SMO How to#SMO_VBConfigure2)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>在 Visual Basic 中修改 SQL Server 设置  
 此代码示例显示有关[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]和<xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Settings>中的实例的信息，并修改和<xref:Microsoft.SqlServer.Management.Smo.Settings> <xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象属性中的设置。  
  
 在此示例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象都有一个 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 您可以分别运行这两个对象的 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure1](SMO How to#SMO_VBConfigure1)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>在 Visual C# 中修改 SQL Server 设置  
 此代码示例显示有关[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]和<xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Settings>中的实例的信息，并修改和<xref:Microsoft.SqlServer.Management.Smo.Settings> <xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象属性中的设置。  
  
 在此示例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象都有一个 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 您可以分别运行这两个对象的 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。  
  
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
 此代码示例显示有关[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]和<xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Settings>中的实例的信息，并修改和<xref:Microsoft.SqlServer.Management.Smo.Settings> <xref:Microsoft.SqlServer.Management.Smo.UserOptions>对象属性中的设置。  
  
 在此示例中，<xref:Microsoft.SqlServer.Management.Smo.UserOptions> 对象和 <xref:Microsoft.SqlServer.Management.Smo.Settings> 对象都有一个 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。 您可以分别运行这两个对象的 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 方法。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
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
 此代码示例说明如何在 Visual Basic .NET 中更新配置选项。 它还检索并显示指定配置选项的最大值和最小值的相关信息。 最后，程序会通知用户是否已进行了动态更改，或者是否存储了更改直到重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例后再予以应用。  
  
```powershell
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = Get-Item default  
  
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
