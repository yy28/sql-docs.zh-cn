---
title: 安装大数据工具
titleSuffix: SQL Server big data clusters
description: 了解如何安装用于 SQL Server 2019 大数据群集（预览版）的工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 757209ff89fd40dcc737b65d3b19f2a7d4ef247b
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419457"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安装 SQL Server 2019 大数据工具

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍为创建、管理和使用 SQL Server 2019 大数据群集（预览版）而应安装的客户端工具。 以下部分提供了工具列表和安装说明链接。 在部署大数据群集之前，请先配置 Windows 或 Linux 上标记为必需的工具。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>大数据群集工具

下表列出了常见的大数据群集工具及其安装方式：

| 工具 | Required | 描述 | 安装 |
|---|---|---|---|
| **python** | 是 | Python 是一种使用动态语义解释的面向对象的高级编程语言。 SQL Server 大数据群集的许多部分都使用 python。 | [安装 python](#python)|
| **azdata** | 是 | 用于安装和管理大数据群集的命令行工具。 | [安装](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | 是 | 用于监视基础 Kuberentes 群集的命令行工具（[详细信息](https://kubernetes.io/docs/tasks/tools/install-kubectl/)）。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery)\|[Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio（预览体验成员）** | 是 | 用于查询 SQL Server 的跨平台图形工具（[详细信息](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)）。 | [安装](https://aka.ms/azdata-insiders) |
| **SQL Server 2019 扩展** | 是 | 用于 Azure Data Studio 的扩展，支持连接到大数据群集。 还提供数据虚拟化向导。 | [安装](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | 针对 AKS | 用于管理 Azure 服务的新式命令行接口。 与 AKS 大数据群集部署配合使用（[详细信息](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)）。 | [安装](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 可选 | 用于查询 SQL Server 的新式命令行接口（[详细信息](https://github.com/dbcli/mssql-cli/blob/master/README.rst)）。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md)\|[Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 针对某些脚本 | 用于查询 SQL Server 的旧式命令行工具（[详细信息](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)）。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433)\|[Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl**<sup>3</sup> | 针对某些脚本 | 使用 URL 传输数据的命令行工具。 | [Windows](https://curl.haxx.se/windows/)\| Linux：安装 curl 包 |

<sup>1</sup> 必须使用 kubectl 版本 1.10 或更高版本。 此外，kubectl 的版本应该加或减 Kubernetes 群集的一个次要版本。 若要在 kubectl 客户端上安装特定版本，请参阅[通过 curl 安装 kubectl 二进制文件](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)（在 Windows 10 上，使用 cmd.exe 而不是 Windows PowerShell 来运行 curl）。 

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

1. （仅适用于 Windows）从该文件夹运行 `installLocalPythonPackages.bat`，并将完整路径作为参数传递到同一文件夹。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="next-steps"></a>后续步骤

配置工具后，将 SQL Server 2019 大数据群集部署到云中或本地的 Kubernetes。 有关详细信息，请参阅以下部署文章：

- [快速入门：在 Azure Kubernetes 服务 (AKS) 上部署 SQL Server 大数据群集](quickstart-big-data-cluster-deploy.md)
- [如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)

有关大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
