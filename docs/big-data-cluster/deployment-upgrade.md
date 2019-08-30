---
title: 升级到新版本
titleSuffix: SQL Server big data clusters
description: 了解如何将 ( [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]预览版) 升级到新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e3fa24998e4c48dad568f926dca2bba4359fe691
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155335"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何升级[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文指导如何将 SQL Server 大数据群集升级到新版本。 本文中的步骤特别适用于如何在预览版本之间进行升级。

## <a name="backup-and-delete-the-old-cluster"></a>备份和删除旧群集

目前，将大数据群集升级到新版本的唯一方法是手动删除并重新创建群集。 每个版本的唯一版本`azdata`都与以前的版本不兼容。 此外，如果旧群集必须下载新节点上的映像，则最新映像可能与群集上的旧映像不兼容。 若要升级到最新版本，请使用以下步骤：

1. 在删除旧群集之前，备份 SQL Server 主实例和 HDFS 上的数据。 对于 SQL Server 主实例，可以使用 [SQL Server 备份和还原](data-ingestion-restore-database.md)。 对于 HDFS,[可以通过`curl`复制数据](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令删除旧群集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用与群集匹配`azdata`的版本。 不要使用较新版本的`azdata`删除较旧的群集。

1. 在 CTP 3.2 之前, `azdata`已调用`mssqlctl`。 如果你具有或`mssqlctl` `azdata`安装的任何以前版本, 请务必先卸载, 然后再安装最新版本的`azdata`。

   对于 CTP 2.3 或更高版本，请运行以下命令。 将`ctp3.1`命令中的替换为你要`mssqlctl`卸载的的版本。 如果是 CTP 3.1 之前的版本，请在版本号前面添加短划线（例如，`ctp-2.5`）。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 安装的`azdata`最新版本。 为候选发布版本`azdata`安装以下命令:

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 对于每个版本, 则为`azdata`要更改的路径。 即使之前安装了`azdata`或`mssqlctl`, 也必须先从最新路径重新安装, 然后才能创建新群集。

## <a id="azdataversion"></a> 验证 azdata 版本

在部署新的大数据群集之前, 请确认你使用的是最新`azdata`版本的`--version`参数:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安装新版本

删除以前的大数据群集并安装最新`azdata`的后, 请使用当前部署说明部署新的大数据群集。 有关详细信息, 请参阅[如何在[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Kubernetes 上部署](deployment-guidance.md)。 然后，还原所有必需的数据库或文件。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]是](big-data-cluster-overview.md)。
