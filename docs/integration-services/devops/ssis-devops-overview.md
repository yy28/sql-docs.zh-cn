---
title: SQL Server Integration Services DevOps 概述 | Microsoft Docs
description: 了解如何使用 SSIS DevOps 工具生成 SSIS CICD。
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6a1f903d0be82d6f5057af68dce80bda1e48238a
ms.sourcegitcommit: 951740963d5fe9cea7f2bfe053c45ad5d846df04
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225918"
---
# <a name="sql-server-integration-services-ssis-devops-tools-preview"></a>SQL Server Integration Services (SSIS) DevOps 工具（预览）

可从 Azure DevOps 市场获取 [SSIS DevOps 工具](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)扩展  。

如果你没有 Azure DevOps 组织，首先请注册 [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops)，然后根据[这些步骤](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension)添加 SSIS DevOps 工具扩展   。

SSIS DevOps 工具包括 SSIS 生成任务和 SSIS 部署发布任务    。

- SSIS 生成任务支持在项目部署模型或包部署模型中生成 dtproj 文件  。

- SSIS 部署任务支持将单个或多个 ispac 文件部署到本地 SSIS 目录，并将 Azure-SSIS IR 或 SSISDeploymentManifest 文件及其关联文件部署到本地或 Azure 文件共享  。

## <a name="ssis-build-task"></a>SSIS 生成任务

![生成任务](media/ssis-build-task.png)

### <a name="properties"></a>属性

#### <a name="project-path"></a>项目路径

要生成的项目文件夹或文件的路径。 如果指定了文件夹路径，则 SSIS 生成任务将以递归方式搜索此文件夹下的所有 dtproj 文件并生成所有文件。

项目路径不能为空  ，设置为 .  以便从存储库的根文件夹中生成。

#### <a name="project-configuration"></a>项目配置

要用于生成的项目配置的名称。 如果未提供，则默认为每个 dtproj 文件中第一个的定义项目配置。

#### <a name="output-path"></a>输出路径

用于保存生成结果的单独文件夹的路径，这些结果可通过[发布生成项目任务](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops)发布为生成项目。

### <a name="limitations-and-known-issues"></a>限制和已知问题

- SSIS 生成任务依赖于 Visual Studio 和 SSIS 设计器，这对于生成代理是必需的。 因此，要在管道中运行 SSIS 生成任务，必须为 Microsoft 托管代理选择 vs2017-win2016，或在自托管代理上安装 Visual Studio 和 SSIS 设计器（VS2017 + SSDT2017 或 VS2019 + SSIS 项目扩展）  。

- 要使用任何现成组件（包括 SSIS Azure 功能包和其他第三方组件）生成 SSIS 项目，必须在运行管道代理的计算机上安装这些现成组件。  对于 Microsoft 托管代理，用户可以添加 [PowerShell 脚本任务](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops)或[命令行脚本任务](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops)，以便在执行 SSIS 生成任务之前下载和安装组件。 下面是用于安装 Azure 功能包的示例 PowerShell 脚本： 

```powershell
wget -Uri https://download.microsoft.com/download/E/E/0/EE0CB6A0-4105-466D-A7CA-5E39FA9AB128/SsisAzureFeaturePack_2017_x86.msi -OutFile AFP.msi

start -Wait -FilePath msiexec -Args "/i AFP.msi /quiet /l* log.txt"

cat log.txt
```

- SSIS 生成任务不支持 EncryptSensitiveWithPassword 和 EncryptAllWithPassword 保护级别   。 请确保基本代码中的所有 SSIS 项目都不使用这两个保护级别，否则，SSIS 生成任务在执行过程中将挂起和超时。

- ConnectByProxy  是最近在 SSDT 中添加的新属性。 Microsoft 托管的代理上安装的 SSDT 未更新，因此，请使用自托管代理作为解决办法。

## <a name="ssis-deploy-task"></a>SSIS 部署任务

![部署任务](media/ssis-deploy-task.png)

### <a name="properties"></a>属性

#### <a name="source-path"></a>源路径

要部署的源 ISPAC 或 SSISDeploymentManifest 文件的路径。 此路径可以是文件夹路径或文件路径。

#### <a name="destination-type"></a>目标类型

目标类型。 当前的 SSIS 部署任务支持两种类型：

- 文件系统  ：将 SSISDeploymentManifest 文件及其关联文件部署到指定的文件系统。 支持本地和 Azure 文件共享。
- SSISDB  ：将 ISPAC 文件部署到指定的 SSIS 目录，该目录可托管在本地 SQL Server 或 Azure-SSIS Integration Runtime 上。

#### <a name="destination-server"></a>目标服务器

目标 SQL 服务器的名称。 它可以是本地 SQL Server、Azure SQL 数据库或 Azure SQL 数据库托管实例的名称。 仅当目标类型为 SSISDB 时，此属性才可见。

#### <a name="destination-path"></a>目标路径

要部署源文件的目标文件夹的路径。 例如：

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

如果文件夹和子文件夹不存在，SSIS 部署任务会进行创建。

#### <a name="authentication-type"></a>身份验证类型

用于访问指定目标服务器的身份验证类型。 仅当目标类型为 SSISDB 时，此属性才可见。 SSIS 部署任务通常支持四种类型：

- Windows 身份验证
- SQL Server 身份验证
- Active Directory - 密码
- Active Directory - 集成

但特定身份验证类型是否受支持取决于目标服务器类型和代理类型。 下表列出了详细的支持矩阵。

| |Microsoft 托管代理|自托管代码|
|---------|---------|---------|
|本地 SQL Server 或 VM |空值|Windows 身份验证|
|Azure SQL|SQL Server 身份验证 <br> Active Directory - 密码|SQL Server 身份验证 <br> Active Directory - 密码 <br> Active Directory - 集成|

#### <a name="domain-name"></a>域名

用于访问指定文件系统的域名。 仅当目标类型为文件系统时，此属性才可见。
如果已向运行自托管代理的用户帐户授予指定目标路径的读写权限，则可以将其留空。

#### <a name="username"></a>用户名

用于访问指定文件系统或 SSISDB 的用户名。 当目标类型为文件系统或身份验证类型为“SQL Server 身份验证”或“Active Directory - 密码”时，此属性可见。
如果目标类型为文件系统，并且已向运行自托管代理的用户帐户授予指定目标路径的读写权限，则可以将其留空。

#### <a name="password"></a>密码

用于访问指定文件系统或 SSISDB 的密码。 当目标类型为文件系统或身份验证类型为“SQL Server 身份验证”或“Active Directory - 密码”时，此属性可见。
如果目标类型为文件系统，并且已向运行自托管代理的用户帐户授予指定目标路径的读写权限，则可以将其留空。

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>覆盖名称相同的现有项目或 SSISDeploymentManifest 文件

指定是否覆盖名称相同的现有项目或 SSISDeploymentManifest 文件。 如果选择“否”，SSIS 部署任务将跳过部署这些项目或文件。

#### <a name="continue-deployment-when-error-occurs"></a>发生错误时继续部署

指定是否在发生错误时继续部署剩余的项目或文件。 如果选择“否”，在发生错误时，SSIS 部署任务将立即停止。

### <a name="limitations-and-known-issues"></a>限制和已知问题

SSIS 部署任务当前不支持以下方案：

- 在 SSIS 目录中配置环境。
- 将 ispac 部署到只允许多重身份验证 (MFA) 的 Azure SQL Server 或 Azure SQL 托管实例。
- 将包部署到 MSDB 或 SSIS 包存储。

## <a name="release-notes"></a>发行说明

### <a name="version-013-preview"></a>版本 0.1.3 预览版

发行日期：2020 年 1 月 19 日

- 修复了一个问题，该问题会在 ispac 的原始文件名发生更改时阻止部署。

### <a name="version-012-preview"></a>版本 0.1.2 预览版

发行日期：2020 年 1 月 13 日

- 目标类型为 SSISDB 时，在 SSIS 部署任务日志中添加了更详细的异常信息。
- 修正了 SSIS 部署任务的属性目标路径帮助文本中的示例目标路径。

### <a name="version-011-preview"></a>版本 0.1.1 预览版

发行日期：2020 年 1 月 6 日

- 添加了对最低代理版本要求的限制。 目前，此产品的最低代理版本是 2.144.0。
- 修正了 SSIS 部署任务的一些不正确的显示文本。
- 完善了一些错误消息。

### <a name="version-010-preview"></a>版本 0.1.0 预览版

发行日期：2019 年 12 月 5 日

SSIS DevOps 工具的初始版本。 这是预览版。

## <a name="next-steps"></a>后续步骤

- 获取 [SSIS DevOps 扩展](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)
