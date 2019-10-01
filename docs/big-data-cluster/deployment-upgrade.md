---
title: 升级到新版本
titleSuffix: SQL Server big data clusters
description: 了解如何将 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] （预览版）升级到新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb1bf33c9ccb342e6afc4d22d67463791c0d67b6
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688275"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何升级 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文指导如何将 SQL Server 大数据群集升级到新版本。 本文中的步骤特别适用于如何在预览版本之间进行升级。

## <a name="backup-and-delete-the-old-cluster"></a>备份和删除旧群集

目前，将大数据群集升级到新版本的唯一方法是手动删除并重新创建群集。 每个版本都有 `azdata` 的唯一版本，与以前的版本不兼容。 此外，如果旧群集必须下载新节点上的映像，则最新映像可能与群集上的旧映像不兼容。 若要升级到最新版本，请使用以下步骤：

1. 在删除旧群集之前，备份 SQL Server 主实例和 HDFS 上的数据。 对于 SQL Server 主实例，可以使用 [SQL Server 备份和还原](data-ingestion-restore-database.md)。 对于 HDFS，[可将数据复制到 `curl`](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令删除旧群集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用与你的群集匹配的 @no__t 的版本。 请勿删除更新版本为 @no__t 的旧群集。

   > [!Note]
   > 发出 `azdata bdc delete` 命令将导致使用要删除的大数据群集名称标识的命名空间中创建的所有对象，而不是命名空间本身。 只要命名空间为空且未在中创建其他应用程序，就可以在后续部署中重复使用命名空间。

1. 在 CTP 3.2 之前，`azdata` 称为 `mssqlctl`。 如果你安装了任何以前版本的 `mssqlctl` 或 `azdata`，则必须先卸载，然后再安装最新版本的 `azdata`。

   对于 CTP 2.3 或更高版本，请运行以下命令。 将命令中的 @no__t 替换为要卸载的 @no__t 版本。 如果是 CTP 3.1 之前的版本，请在版本号前面添加短划线（例如，`ctp-2.5`）。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 安装最新版本的 `azdata`。 以下命令将安装候选发布的 `azdata`：

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 对于每个版本，`azdata` 的路径更改。 即使之前安装 `azdata` 或 `mssqlctl`，你也必须在创建新群集之前从最新路径重新安装。

## <a id="azdataversion"></a> 验证 azdata 版本

在部署新的大数据群集之前，请确认你使用的是最新版本的 `azdata` 与 `--version` 参数：

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安装新版本

删除以前的大数据群集并安装最新 `azdata` 后，请使用当前部署说明部署新的大数据群集。 有关详细信息，请参阅[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)。 然后，还原所有必需的数据库或文件。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 @no__t](big-data-cluster-overview.md)。
