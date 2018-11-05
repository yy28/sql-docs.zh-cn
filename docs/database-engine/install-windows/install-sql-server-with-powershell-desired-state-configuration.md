---
title: 使用 PowerShell Desired State Configuration 安装 SQL Server | Microsoft Docs
description: 了解如何使用 PowerShell Desired State Configuration (DSC) 安装 SQL Server。
ms.custom: ''
ms.date: 10/26/2018
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 16d425d8eb66a950f432fa3ef9c68a8e68a78d22
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148473"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>使用 PowerShell Desired State Configuration 安装 SQL Server

你是否曾多次发生下述状况：单击 SQL Server 安装界面时，只是机械般地单击相同的旧按钮，输入相同的旧信息，而没有多加考虑？ 然后在安装完成时，突然想到“我忘了在 sysadmin 角色中指定 DBA 组”。 此时，必须花费宝贵的时间进入单用户模式，添加适当的用户或组，在多用户模式下进行 SQL 备份，然后进行测试。 更糟糕的是，现在你会对整个安装过程产生怀疑。 “我还忘记了什么？” 我不止一次遭遇这种情况。

输入 [PowerShell Desired State Configuration (DSC)](https://docs.microsoft.com/powershell/dsc/overview)。 使用 DSC，我可构建一个能在成百上千个服务器上重复使用的配置模板。 在所构建的配置模基础上，我可能需要调整一些设置参数，但这并不是什么大问题，因为所有标准设置仍可保持不变。 它的好处在于，即使我因照顾孩子一夜未眠而无法保持专注，也不会忘记输入重要参数。

在本文中，我将使用 SqlServerDsc DSC 资源探索 Windows Server 2016 上 SQL Server 2017 独立实例的初始设置。 由于我不会介绍 DSC 的工作原理，因此拥有一些 DSC 知识储备将会有所帮助。

本演练需要以下项：

- 运行 Windows Server 2016 的计算机
- SQL Server 2017 安装介质
- SqlServerDsc DSC 资源（撰写本文时，最新版本为版本 10.0.0.0）

## <a name="prerequisites"></a>必备条件

在大多数情况下，DSC 将用于处理先决条件要求。 但是，出于本演示的目的，我将手动处理先决条件。

## <a name="install-the-sqlserverdsc-dsc-resource"></a>安装 SqlServerDsc DSC 资源

可使用 [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1) cmdlet 从 [PowerShell 库](https://www.powershellgallery.com/)下载 [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) DSC 资源。 _注意：安装模块时，需确保“以管理员身份”运行 PowerShell。_

```PowerShell
Install-Module -Name SqlServerDsc
```

获取 SQL Server 2017 安装介质，将 SQL Server 2017 安装介质下载到服务器。 我已通过 Visual Studio 订阅下载 SQL Server 2017 Enterprise，并将 ISO 复制到“C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso”。

现在必须将 ISO 提取到目录。

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>创建配置

### <a name="configuration"></a>配置

创建配置函数，将调用该函数生成[托管对象格式 (MOF)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-) 文档。

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>模块

将模块导入当前会话。 这些模块指示配置文档如何构建 MOF 文档，并指示 DSC 引擎如何将 MOF 文档应用于服务器。

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>Resources

#### <a name="net-framework"></a>.NET Framework

SQL Server 依赖于 .NET Framework，因此需确保其先于 SQL Server 安装。 WindowsFeature 资源用于安装 Net-Framework-45-Core Windows 功能。

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

SqlSetup 资源用于告知 DSC 如何安装 SQL Server。 基本安装所需的参数包括：

- **InstanceName**：实例的名称。 使用 MSSQLSERVER 作为默认实例。
- **Features**：要安装的功能。 在此示例中，我将仅安装 SQLEngine 功能。
- **SourcePath**：SQL 安装介质的路径。 在此示例中，我将 SQL 安装介质存储在“C:\SQL2017”中。 可利用网络共享最大程度减少服务器上使用的空间。
- **SQLSysAdminAccounts**：要成为 sysadmin 角色成员的用户或组。 在此示例中，我将授予本地管理员组 sysadmin 访问权限。 _注意：不建议在高安全性环境中使用此配置。_

有关 SqlSetup 上可用参数的完整列表和说明，请参阅 [SqlServerDsc GitHub 存储库](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup)。

SqlSetup 资源很奇怪，因为它只安装 SQL，但不维护所应用的设置。 例如，如果在安装时指定了 SQLSysAdminAccounts，则管理员可在 sysadmin 角色中添加或删除登录名，而 SqlSetup 资源完全无视此操作。 如果希望 DSC 强制执行 sysadmin 角色的成员资格，则应使用 [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole) 资源。

#### <a name="complete-configuration"></a>完成配置

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>生成和部署

### <a name="compile-the-configuration"></a>编译配置

在配置脚本中添加圆点：

```PowerShell
. .\SQLInstallConfiguration.ps1
```

执行配置函数：

```PowerShell
SQLInstall
```

将在名为“SQLInstall”的工作目录中创建一个目录，该目录将包含一个名为“localhost.mof”的文件。 检查 MOF 的内容，已编译的 DSC 配置随即显示。

### <a name="deploy-the-configuration"></a>部署配置

若要启动 SQL Server 的 DSC 部署，请调用 Start-DscConfiguration cmdlet。 提供给该 cmdlet 的参数包括：

- **Path**：包含要部署的 MOF 文档的文件夹的路径。 （例如“C:\SQLInstall”）
- **Wait**：等待配置作业完成。
- **Force**：替代任何现有 DSC 配置。
- **Verbose**：显示详细输出。 首次推送配置时非常有用，可帮助排除故障。

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

应用配置后，详细输出将显示正在发生的情况，通过这种温馨的方式让你对将要发生的某些状况有所预知。 只要没有引发错误（红色文本），那么当屏幕上显示出“操作‘调用 CimMethod’完成。” 时，则已安装 SQL。

## <a name="validate-installation"></a>验证安装

### <a name="dsc"></a>DSC

可使用 [Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) cmdlet 来确定服务器的当前状态（在本例中为 SQL 安装）是否符合所需状态。 Test-DscConfiguration 的结果应为“True”。

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>服务

现在，服务列表应返回 SQL Server 服务

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>SQL Server

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>另请参阅

[Windows PowerShell Desired State Configuration 概述](https://docs.microsoft.com/powershell/dsc/overview)

[从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[使用配置文件安装 SQL Server](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
