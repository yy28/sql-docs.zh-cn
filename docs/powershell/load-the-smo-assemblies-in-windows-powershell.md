---
title: 在 Windows PowerShell 中加载 SMO 程序集 | Microsoft Docs
description: 了解如何在不使用 SQL Server PowerShell 提供程序的 Windows PowerShell 脚本中加载 SQL Server 管理对象 (SMO) 程序集。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 673e94da44cbdd46a8873468b4421a1a8ea4e037
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714225"
---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>在 Windows PowerShell 中加载 SMO 程序集
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

本文介绍如何在不使用 SQL Server PowerShell 提供程序的 Windows PowerShell 脚本中加载 SQL Server 管理对象 (SMO) 程序集。  
  
> [!NOTE]
> SQL Server PowerShell 模块有两种；SqlServer 和 SQLPS 。 虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块。 SqlServer 模块不仅包含 SQLPS 更新版本的 cmdlet，并且还包含新的 cmdlet 以支持最新的 SQL 功能 。  
> 虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 PowerShell 库安装 SqlServer 模块。
> 要安装 SqlServer 模块，请参阅[安装 SQL Server PowerShell](download-sql-server-ps-module.md)。


加载 SMO 程序集的首选机制是加载 SqlServer 模块。 该模块中包括的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序将自动加载 SMO 程序集，还会实现可扩展 PowerShell 脚本中的 SMO 对象的有用性的功能。
  
有两种情况可能需要您直接加载 SMO 程序集：  
  
-   脚本在从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理单元引用该提供程序或 cmdlet 的第一个命令之前引用了一个 SMO 对象。  
  
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
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
