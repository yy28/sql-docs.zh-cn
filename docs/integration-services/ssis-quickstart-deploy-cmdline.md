---
title: "从命令提示符部署 SSIS 项目 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c3e7f7e3fa870c7aa5b30a5a4a324f0cef7f6ba
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>使用 ISDeploymentWizard.exe 从命令提示符部署 SSIS 项目
本快速入门教程演示如何通过运行 Integration Services 部署向导 (`ISDeploymentWizard.exe`) 从命令提示符部署 SSIS 项目。

有关 Integration Services 部署向导的详细信息，请参阅 [Integration Services 部署向导](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)。

## <a name="start-the-integration-services-deployment-wizard"></a>启动 Integration Services 部署向导
1. 打开命令提示符窗口。

2. 运行 `ISDeploymentWizard.exe`。 Integration Services 部署向导随即打开。

    如果包含 `ISDeploymentWizard.exe` 的文件夹不在 `path` 环境变量中，可能需要使用 `cd` 命令将目录更改为该文件夹的目录。 对于 SQL Server 2017，此文件夹通常位于 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

## <a name="deploy-a-project-with-the-wizard"></a>使用向导部署项目
1. 在向导的“简介”页上查看简介。 单击“下一步”打开“选择源”页。

2. 在“选择源”页上，选择要部署的现有 SSIS 项目。
    -   若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。
    -   若要部署位于 SSIS 目录中的项目，请选择“Integration Services 目录”，然后输入目录中该项目的服务器名称和路径。
    单击“下一步”  以查看“选择目标”  页。
  
3.  在“选择目标”页上，选择项目的目标。
    -   输入完全限定服务器名称。 如果目标服务器是 Azure SQL 数据库服务器，则名称采用以下格式：`<server_name>.database.windows.net`。
    -   然后单击“浏览”，在 SSISDB 中选择目标文件夹。
    单击“下一步”打开“查看”页。  
  
4.  在“查看”页上，查看所选的设置。
    -   可以通过单击 **“上一步”**或单击左窗格中的任意步骤来更改所做的选择。
    -   单击“部署”  以启动部署过程。
  
5.  部署过程完成之后，“结果”页随即打开。 该页显示每个操作是成功了还是失败了。
    -   如果操作失败，则单击“结果”列中的“失败”可显示错误说明。
    -   （可选）单击“保存报告...”以将结果保存到某一 XML 文件。
    -   单击“关闭”以退出向导。

## <a name="next-steps"></a>后续步骤
- 考虑部署包的其他方式。
    - [使用 SSMS 部署 SSIS 包](./ssis-quickstart-deploy-ssms.md)
    - [使用 Transact-SQL (SSMS) 部署 SSIS 包](./ssis-quickstart-deploy-tsql-ssms.md)
    - [使用 Transact-SQL (VS Code) 部署 SSIS 包](ssis-quickstart-deploy-tsql-vscode.md)
    - [使用 PowerShell 部署 SSIS 包](ssis-quickstart-deploy-powershell.md)
    - [使用 C# 部署 SSIS 包](./ssis-quickstart-deploy-dotnet.md) 
- 运行已部署的包。 若要运行包，可以从多个工具和语言中进行选择。 有关详细信息，请参阅下文：
    - [使用 SSMS 运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL (SSMS) 运行 SSIS 包](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [从命令提示符运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 
