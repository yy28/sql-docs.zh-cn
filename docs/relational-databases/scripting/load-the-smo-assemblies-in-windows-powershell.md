---
title: "在 Windows PowerShell 中加载 SMO 程序集 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 149ba0be18c46dbf2171f7a1fac0641ae81d3515
ms.lasthandoff: 04/11/2017

---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>在 Windows PowerShell 中加载 SMO 程序集
  本主题介绍如何在不使用 SQL Server PowerShell 提供程序的 Windows PowerShell 脚本中加载 SQL Server 管理对象 (SMO) 程序集。  
  
## <a name="before-you-begin"></a>开始之前  
 加载 SMO 程序集的首选机制是加载 **sqlps** 模块。 该模块中包括的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序将自动加载 SMO 程序集，还会实现可扩展 PowerShell 脚本中的 SMO 对象的有用性的功能。  有关详细信息，请参阅 [导入 SQLPS 模块](../../relational-databases/scripting/import-the-sqlps-module.md)。
  
 有两种情况可能需要您直接加载 SMO 程序集：  
  
-   脚本在从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理单元引用该提供程序或 cmdlet 的第一个命令之前引用了一个 SMO 对象。  
  
-   您需要从不使用该提供程序或 cmdlet 的另一种语言（例如 C# 或 Visual Basic）移植 SMO 代码。  
  
## <a name="example-loading-the-sql-server-management-objects"></a>示例：加载 SQL Server 管理对象  
 下面的代码加载 SMO 程序集：  
  
```  
#  
# Loads the SQL Server Management Objects (SMO)  
#  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg="HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
update-FormatData -prependpath SQLProvider.Format.ps1xml   
Pop-Location  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
