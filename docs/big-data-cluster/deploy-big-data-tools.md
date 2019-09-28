---
title: 安装大数据工具
titleSuffix: SQL Server big data clusters
description: 了解如何安装与 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] （预览版）一起使用的工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cbb34d5cd209281a5c97d819c7741503d234ad2d
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342020"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安装 SQL Server 2019 大数据工具

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍应安装的客户端工具，以便创建、管理和使用 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] （预览版）。 以下部分提供了工具列表和安装说明链接。 在部署大数据群集之前，请先配置 Windows 或 Linux 上标记为必需的工具。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>大数据群集工具

下表列出了常见的大数据群集工具及其安装方式：

| Tool | Required | 描述 | 安装 |
|---|---|---|---|
| **python** | 是 | Python 是一种使用动态语义解释的面向对象的高级编程语言。 SQL Server 大数据群集的许多部分都使用 python。 | [安装 python](#python)|
| **azdata** | 是 | 用于安装和管理大数据群集的命令行工具。 | [安装](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | 是 | 用于监视基础 Kuberentes 群集的命令行工具（[详细信息](https://kubernetes.io/docs/tasks/tools/install-kubectl/)）。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-using-native-package-management) |
| **Azure Data Studio SQL Server 2019 候选发布版本（RC）** | 是 | 用于查询 SQL Server 的跨平台图形工具。 | [安装](#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) |
| **SQL Server 2019 扩展** | 是 | 用于 Azure Data Studio 的扩展，支持连接到大数据群集。 还提供数据虚拟化向导。 | [安装](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | 针对 AKS | 用于管理 Azure 服务的新式命令行接口。 与 AKS 大数据群集部署配合使用（[详细信息](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)）。 | [安装](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 可选 | 用于查询 SQL Server 的新式命令行接口（[详细信息](https://github.com/dbcli/mssql-cli/blob/master/README.rst)）。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 针对某些脚本 | 用于查询 SQL Server 的旧式命令行工具（[详细信息](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)）。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 针对某些脚本 | 使用 URL 传输数据的命令行工具。 | [Windows](https://curl.haxx.se/windows/)\| Linux: 安装卷包 |

<sup>1</sup>你必须使用 kubectl 版本1.13 或更高版本。 此外，kubectl 的版本应该加或减 Kubernetes 群集的一个次要版本。 若要在 kubectl 客户端上安装特定版本，请参阅[通过 curl 安装 kubectl 二进制文件](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)（在 Windows 10 上，使用 cmd.exe 而不是 Windows PowerShell 来运行 curl）。

> [!TIP]
> 若要在 Azure Kubernetes 服务 (AKS) 上将 kubectl 与先前部署的群集配合使用，必须使用以下 Azure CLI 命令设置群集上下文：
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> 必须使用 Azure CLI 版本 2.0.4 或更高版本。 如果需要，可运行 `az --version` 来查找版本。

<sup>3</sup> 如果在 Windows 10 上运行，则在命令提示符下运行时，**curl** 就已经在你的路径中。 对于其他 Windows 版本，请使用链接下载 **curl** 并将其放在你的路径中。

## <a name="which-tools-are-required"></a>需要哪些工具？

上表提供了适用于大数据群集的所有常见工具。 具体需要哪些工具取决于你的方案。 但总的来说，以下工具对于管理、连接和查询群集最为重要：

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 扩展**

其余工具仅在某些情况下需要。 **Azure CLI** 可用于管理与 AKS 部署相关联的 Azure 服务。 **mssql-cli** 是一个可选但有用的工具，可用于连接到群集中的 SQL Server 主实例并从命令行运行查询。 如果计划使用 GitHub 脚本安装示例数据，则需要 **sqlcmd** 和 **curl**。

### <a id="python"></a> 脱机安装 python

1. 在具有 Internet 访问权限的计算机上，下载以下包含 Python 的压缩文件之一：

   | 操作系统 | 下载 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 将压缩文件复制到目标计算机，并将其解压缩到所选文件夹中。

1. 从该文件夹运行 `installLocalPythonPackages.bat`，并将完整路径作为参数传到同一文件夹，该操作仅适用于 Windows。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc"></a>下载并安装 Azure Data Studio SQL Server 2019 候选发布版本（RC）

Azure Data Studio SQL Server 2019 RC 为 SQL Server 2019 RC 提供专门功能。

对于 Azure Data Studio 的生产版本，请按照[下载并安装 Azure Data Studio](../azure-data-studio/download.md)中的说明进行操作。

|平台|下载|发布日期| 版本 |
|:---|:---|:---|:---|
|Windows|[用户安装程序（推荐）](https://go.microsoft.com/fwlink/?linkid=2102435)<br>[系统安装程序](https://go.microsoft.com/fwlink/?linkid=2102523)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2102524)|2019年8月27日 |RC 1.11.0-内部人员|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2102436)|2019年8月27日 |RC 1.11.0-内部人员|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2102526)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)|2019年8月27日 |RC 1.11.0-内部人员|

有关最新版本的详细信息，请参阅[发行说明](../big-data-cluster/release-notes-big-data-cluster.md)。

### <a name="get-azure-data-studio-for-windows"></a>获取适用于 Windows 的 Azure Data Studio

此版本的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 包含标准 Windows 安装程序体验和 .zip 文件。

建议使用用户安装程序，因为它不需要管理员权限，可简化安装和升级。 用户安装程序不需要管理员权限，因为它位于用户本地的 AppData (LOCALAPPDATA) 文件夹下。 用户安装程序还提供更流畅的后台更新体验。 有关详细信息，请参阅 [Windows 用户设置](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)。

**用户安装程序**（推荐）

1. 下载并运行[适用于 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 用户安装程序](https://go.microsoft.com/fwlink/?linkid=2102435)。
2. 启动 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 应用。

**系统安装程序**

1. 下载并运行[适用于 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 系统安装程序](https://go.microsoft.com/fwlink/?linkid=2102523)。
2. 启动 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 应用。

**zip 文件**

1. 下载[适用于 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2102524)。
2. 浏览到下载文件并将其解压缩。
3. 运行 `\azuredatastudio-windows\azuredatastudio.exe`

### <a name="get-azure-data-studio-for-macos"></a>获取适用于 macOS 的 Azure Data Studio

1. 下载适用于 macOS 的 [[!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2102436)。
2. 若要展开 zip 的内容，请双击它。
3. 若要使 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 在启动板中可用，请将 Azure Data Studio.app 拖到“Applications”文件夹中。

### <a name="get-azure-data-studio-for-linux"></a>获取适用于 Linux 的 Azure Data Studio

1. 使用其中一个安装程序或 tar.gz 存档下载适用于 Linux 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2102526)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)
1. 若要解压缩文件并启动 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，请打开新的终端窗口并键入以下命令：

   **Debian 安装：**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm 安装：**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **tar.gz 安装：**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > 在 Debian、Redhat 和 Ubuntu 上，可能缺少依赖项。 使用以下命令安装这些依赖项，具体取决于你的 Linux 版本：
   

   **Debian：** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat：** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu：** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

### <a name="supported-operating-systems"></a>支持的操作系统

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、macOS 和 Linux 上运行，并在以下平台上受支持：

#### <a name="windows"></a>Windows

- Windows 10（64 位）
- Windows 8.1（64 位）
- Windows 8（64 位）
- Windows 7 (SP1)（64 位）- 需要 [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2（64 位）
- Windows Server 2012（64 位）
- Windows Server 2008 R2（64 位）

#### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>后续步骤

配置工具后，将 SQL Server 2019 大数据群集部署到云中或本地的 Kubernetes。 有关详细信息，请参阅以下部署文章：

- [快速入门：在 Azure Kubernetes 服务 (AKS) 上部署 SQL Server 大数据群集](quickstart-big-data-cluster-deploy.md)
- [如何在 Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上部署](deployment-guidance.md)

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
