---
title: "使用 PowerShell 部署 SSIS 项目 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d23639aa98492228fdec5d45799718f59b809425
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-an-ssis-project-with-powershell"></a>使用 PowerShell 部署 SSIS 项目
本快速入门教程演示了如何使用 PowerShell 脚本连接到数据库服务器，并将 SSIS 项目部署到 SSIS 目录。

## <a name="powershell-script"></a>PowerShell 脚本
为以下脚本顶部的变量提供适当的值，然后运行脚本以部署 SSIS 项目。

> [!NOTE]
> 下面的示例使用 Windows 身份验证。 要使用 SQL Server 身份验证，请将 `Integrated Security=SSPI;` 参数替换为 `User ID=<user name>;Password=<password>;`。

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Create the target folder
$folder = New-Object $SSISNamespace".CatalogFolder" ($catalog, $TargetFolderName,
    "Folder description")
$folder.Create()

Write-Host "Deploying " $ProjectName " project ..."

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

Write-Host "Done."
```

## <a name="next-steps"></a>后续步骤
- 考虑部署包的其他方式。
    - [使用 SSMS 部署 SSIS 包](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 包 (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL 部署 SSIS 包 (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [从命令提示符部署 SSIS 包](./ssis-quickstart-deploy-cmdline.md)
    - [使用 C# 部署 SSIS 包](./ssis-quickstart-deploy-dotnet.md) 
- 运行已部署的包。 若要运行包，可以从多个工具和语言中进行选择。 有关详细信息，请参阅下文：
    - [使用 SSMS 运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL 运行 SSIS 包 (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL 运行 SSIS 包 (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [从命令提示符运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 
