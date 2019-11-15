---
title: 升级到新版本
titleSuffix: SQL Server Big Data Clusters
description: 了解如何将 SQL Server 大数据群集升级到新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f44ef17a712d0d5a19707cf94e7d3e4196a2aba3
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706311"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何升级 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文指导如何将 SQL Server 大数据群集升级到新版本。 本文中的步骤专门适用于从预览版本升级到 SQL Server 2019 服务更新版本。

## <a name="backup-and-delete-the-old-cluster"></a>备份和删除旧群集

大数据群集目前没有就地升级，因此升级到新版本的唯一方法是手动删除并重新创建该群集。 每个版本都有唯一的 `azdata` 版本，该版本与以前的版本不兼容。 此外，如果旧群集必须下载新节点上的容器映像，则最新映像可能与群集上的旧映像不兼容。 请注意，仅当在容器设置的部署配置文件中使用 `latest` 映像标记时，才会拉取较新的映像。 默认情况下，每个版本都具有与 SQl Server 发行版本相对应的特定映像标记。 若要升级到最新版本，请使用以下步骤：

1. 在删除旧群集之前，备份 SQL Server 主实例和 HDFS 上的数据。 对于 SQL Server 主实例，可以使用 [SQL Server 备份和还原](data-ingestion-restore-database.md)。 对于 HDFS，[可以使用 `curl` 复制数据](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令删除旧群集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用与群集匹配的 `azdata` 版本。 请勿删除具有较新 `azdata` 版本的旧群集。

   > [!Note]
   > 发出 `azdata bdc delete` 命令将导致删除以大数据群集名称标识的命名空间中所创建的所有对象，而不会删除命名空间本身。 只要命名空间为空且未在其中创建其他应用程序，就可以在后续部署中重复使用该命名空间。

1. 卸载旧版本的 `azdata`

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 安装最新版本的 `azdata`。 通过以下命令安装最新版本的 `azdata`：

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 对于每个版本，`azdata` 的 `n-1` 的路径都有变化。 即使以前安装了 `azdata`，也必须在创建新群集前从最新路径重新安装。

## <a id="azdataversion"></a> 验证 azdata 版本

在部署新的大数据群集之前，请使用 `--version` 参数验证你是否使用最新版本的 `azdata`：

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安装新版本

删除以前的大数据群集并安装最新的 `azdata` 后，使用当前的部署说明部署新的大数据群集。 有关详细信息，请参阅[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deployment-guidance.md)。 然后，还原所有必需的数据库或文件。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。
