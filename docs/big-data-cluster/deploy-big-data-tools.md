---
title: 安装大数据工具
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何安装与 SQL Server 2019 大数据群集 （预览版） 配合使用的工具。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ab8633ef6741ae1d1a3a973796eec1de0cc12c37
ms.sourcegitcommit: 12911093559b4e006189d7a7d32b8d0474961cd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2019
ms.locfileid: "54372632"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安装 SQL Server 2019 大数据工具

本指南介绍了客户端工具应在管理，用于创建、 安装和使用 SQL Server 2019 大数据群集 （预览版）。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>大数据群集工具

下表列出了常用的大数据群集工具以及如何安装它们：

| 工具 | Required | Description | 安装 |
|---|---|---|---|
| **mssqlctl** | 用户帐户控制 | 用于安装和管理大数据群集的命令行工具。 | [安装](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | 用户帐户控制 | 监视基础 Kuberentes 群集的命令行工具 ([的详细信息](https://kubernetes.io/docs/tasks/tools/install-kubectl/))。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio** | 用户帐户控制 | 用于查询 SQL Server 的跨平台图形化工具 ([的详细信息](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15))。 | [安装](../azure-data-studio/download.md) |
| **SQL Server 2019 扩展** | 用户帐户控制 | 适用于支持连接到大数据群集的 Azure Data Studio 的扩展。 此外提供了数据虚拟化向导。 | [安装](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | 适用于 AKS | 用于管理 Azure 服务的新式命令行界面。 与 AKS 的大数据群集部署一起使用 ([的详细信息](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest))。 | [安装](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 可选 | 新式命令行接口，用于查询 SQL Server ([的详细信息](https://github.com/dbcli/mssql-cli/blob/master/README.rst))。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 对于某些脚本 | 用于查询 SQL Server 的传统命令行工具 ([的详细信息](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15))。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 对于某些脚本 | 将使用的 Url 的数据传输的命令行工具。 | [Windows](https://curl.haxx.se/windows/) \| Linux： 安装 curl 包 |

<sup>1</sup>必须使用 kubectl 版本 1.10 或更高版本。 此外，kubectl 的版本应为加上或减去的 Kubernetes 群集的一个次要版本。 如果你想要 kubectl 客户端上安装特定版本，请参阅[安装 kubectl 二进制通过 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) （在 Windows 10 上使用 cmd.exe 而非 Windows PowerShell 运行 curl）。 

> [!TIP]
> 若要与之前部署的群集在 Azure Kubernetes 服务 (AKS) 使用 kubectl，必须设置的群集上下文与以下 Azure CLI 命令：
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> ，必须使用 Azure CLI 2.0.4 或更高版本。 运行`az --version`如果需要查找版本。

<sup>3</sup>如果在 Windows 10 上运行**curl**从命令提示符处运行时已在你的路径。 对于其他版本的 Windows，下载**curl**使用的链接，并将其放在你的路径中。

## <a name="which-tools-are-required"></a>需要哪些工具？

上表提供了所有与大数据群集配合使用的常见工具。 所需的工具取决于你的方案。 但一般情况下，以下工具是最重要的管理、 连接和查询群集：

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 扩展**

在某些情况下仅需要其余的工具。 **Azure CLI**可用于管理与 AKS 部署关联的 Azure 服务。 **mssql cli**是一种可选的但有用的工具，可用于连接到群集中的 SQL Server 主实例和从命令行运行查询。 并**sqlcmd**并**curl**是必需的如果你打算使用 GitHub 脚本安装示例数据。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
