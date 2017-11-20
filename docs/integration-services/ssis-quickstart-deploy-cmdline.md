---
title: "部署从命令提示符的 SSIS 项目 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 0f1c7733f0ce6b132c209961a1fd12da80cbd282
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>部署从 ISDeploymentWizard.exe 在命令提示符的 SSIS 项目
此快速入门教程演示如何通过运行 Integration Services 部署向导，将部署从命令提示符的 SSIS 项目`ISDeploymentWizard.exe`。

有关 Integration Services 部署向导的详细信息，请参阅[Integration Services 部署向导](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)。

## <a name="start-the-integration-services-deployment-wizard"></a>启动 Integration Services 部署向导
1. 打开命令提示符窗口。

2. 运行 `ISDeploymentWizard.exe`。 Integration Services 部署向导将打开。

    如果该文件夹，包含`ISDeploymentWizard.exe`不在你`path`环境变量，你可能需要使用`cd`命令转到其目录。 对于 SQL Server 自 2017 年，此文件夹通常是`C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

## <a name="deploy-a-project-with-the-wizard"></a>部署向导项目
1. 上**简介**页的向导中，查看简介。 单击**下一步**以打开**选择源**页。

2. 上**选择源**页上，选择要部署的现有 SSIS 项目。
    -   若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。
    -   若要部署的 SSIS 目录中驻留的项目，选择**Integration Services 目录**，，然后输入服务器名称和路径的目录中的项目。
    单击“下一步”  以查看“选择目标”  页。
  
3.  上**选择目标**页上，选择项目的目标。
    -   输入完全限定的服务器名称。 如果目标服务器，Azure SQL 数据库服务器的名称所采用此格式： `<server_name>.database.windows.net`。
    -   然后单击**浏览**在 SSISDB 中选择目标文件夹。
    单击**下一步**以打开**评审**页。  
  
4.  上**查看**页上，查看所选的设置。
    -   可以通过单击 **“上一步”**或单击左窗格中的任意步骤来更改所做的选择。
    -   单击“部署”  以启动部署过程。
  
5.  在部署过程完成后**结果**页将打开。 该页显示每个操作是成功了还是失败了。
    -   如果操作失败，请单击**失败**中**结果**列以显示的错误说明。
    -   （可选） 单击**保存报表...**将结果保存到 XML 文件。
    -   单击**关闭**以退出向导。

## <a name="next-steps"></a>后续步骤
- 考虑使用其他方法来部署的包。
    - [部署 SSIS 包使用 SSMS](./ssis-quickstart-deploy-ssms.md)
    - [部署 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [部署 SSIS 包使用 TRANSACT-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [部署 SSIS 包使用 PowerShell](ssis-quickstart-deploy-powershell.md)
    - [部署使用 C# SSIS 包](./ssis-quickstart-deploy-dotnet.md) 
- 运行部署的包。 若要运行包，你可以从多个工具和语言选择。 有关详细信息，请参阅以下文章：
    - [使用 SSMS 中运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [运行 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [在命令提示符下运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 

