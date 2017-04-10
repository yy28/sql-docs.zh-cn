---
title: "在数据库引擎 PowerShell 中管理身份验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 在数据库引擎 PowerShell 中管理身份验证
  默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 组件在连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例时使用 Windows 身份验证。 你可以通过定义 PowerShell 虚拟驱动器，或者通过为 **Invoke-Sqlcmd** 指定 **–Username** 和 **–Password** 参数，来使用 SQL Server 身份验证。  
  
1.  **开始之前：**  [权限](#Permissions)  
  
2.  **若要设置身份验证，请使用：**[虚拟驱动器](#SQLAuthVirtDrv)[Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="Permissions"></a> 权限  
 您可以在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中执行的所有操作都受到授予用于连接到该实例的身份验证凭据的权限的控制。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 和 cmdlet 将使用其运行所基于的 Windows 帐户来建立与 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的 Windows 身份验证连接。  
  
 若要建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接，您必须提供 SQL Server 身份验证登录 ID 和密码。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序时，必须将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录凭据与虚拟驱动器关联起来，然后使用更改目录命令 (**cd**) 连接到该驱动器。 在 Windows PowerShell 中，安全凭据只能与虚拟驱动器关联。  
  
##  <a name="SQLAuthVirtDrv"></a> 使用虚拟驱动器进行 SQL Server 身份验证  
 **创建与 SQL Server 身份验证登录相关联的虚拟驱动器**  
  
1.  创建一个函数，该函数：  
  
    1.  具有针对为虚拟驱动器提供的名称、登录 ID 以及要与虚拟驱动器相关联的提供程序路径的参数。  
  
    2.  使用 **read-host** 来提示用户输入密码。  
  
    3.  使用 **new-object** 来创建凭据对象。  
  
    4.  使用 **new-psdrive** 来创建具有提供的凭据的虚拟驱动器。  
  
2.  调用函数来创建具有提供的凭据的虚拟驱动器。  
  
### 示例（虚拟驱动器）  
 此示例创建名为 **sqldrive** 的函数，您可使用该函数来创建与指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名和实例相关联的虚拟驱动器。  
  
 **sqldrive** 函数提示您输入登录名的密码，并在您键入密码时屏蔽密码。 然后，每当你使用更改目录命令 (**cd**) 来通过使用虚拟驱动器名称连接到路径时，所有操作都将通过使用你在创建驱动器时提供的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录凭据来执行。  
  
```  
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = read-host -AsSecureString -Prompt "Password"  
    $cred = new-object System.Management.Automation.PSCredential -argumentlist $login,$pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> 使用 Invoke-Sqlcmd 的 SQL Server 身份验证  
 **将 Invoke-Sqlcmd 用于 SQL Server 身份验证**  
  
1.  使用 **–Username** 参数可以指定一个登录 ID，以及用于指定关联密码的 **–Password** 参数。  
  
### 示例 (Invoke-Sqlcmd)  
 此示例使用 read-host cmdlet 来提示用户输入密码，然后使用 SQL Server 身份验证进行连接。  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" –Username “MyLogin” –Password $pwd  
```  
  
## 另请参阅  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd cmdlet](../../powershell/invoke-sqlcmd-cmdlet.md)  
  
  