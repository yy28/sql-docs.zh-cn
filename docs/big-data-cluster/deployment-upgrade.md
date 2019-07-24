---
title: 升级到新版本
titleSuffix: SQL Server big data clusters
description: 了解如何将 SQL Server 2019 大数据群集 (预览版) 升级到新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7bdb1eb59fd36d065df9dba0f6d6879c1a294914
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419393"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>如何升级 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供了有关如何将 SQL Server 大数据群集升级到新版本的指导。 本文中的步骤专门适用于在预览版本之间进行升级的方式。

## <a name="backup-and-delete-the-old-cluster"></a>备份并删除旧群集

目前, 将大数据群集升级到新版本的唯一方法是手动删除并重新创建群集。 每个版本都具有与以前版本不兼容的**azdata**的唯一版本。 此外, 如果较早的群集必须在新节点上下载映像, 则最新的映像可能与群集上的较旧映像不兼容。 若要升级到最新版本, 请使用以下步骤:

1. 删除旧群集之前, 请备份 SQL Server 主实例和 HDFS 上的数据。 对于 SQL Server 主实例, 可以使用[SQL Server 备份和还原](data-ingestion-restore-database.md)。 对于 HDFS,[可以通过**卷**复制数据](data-ingestion-curl.md)。

1. 用`azdata delete cluster`命令删除旧群集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用与群集匹配的**azdata**版本。 请勿删除**azdata**较新版本中的旧群集。

1. 在 CTP 3.2 之前, **azdata**称为**mssqlctl**。 如果安装了任何以前版本的**mssqlctl**或**azdata** , 则必须先卸载, 然后再安装最新版本的**azdata**。

   对于 CTP 2.3 或更高版本, 请运行以下命令。 将`ctp3.1`命令中的替换为要卸载的**mssqlctl**的版本。 如果版本早于 CTP 3.1, 请在版本号前添加一个短划线 (例如`ctp-2.5`)。

   ```powershell
   pip3 uninstall -r https://mcr.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 安装最新版本的**azdata**。 以下命令安装 CTP 3.2 的**azdata** :

   **Windows**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 对于每个版本, **azdata**的路径将更改。 即使之前安装了**azdata**或**mssqlctl**, 也必须在创建新群集之前从最新路径重新安装。

## <a id="azdataversion"></a>验证 azdata 版本

在部署新的大数据群集之前, 请确认你使用的是最新版本的 azdata `--version`和参数:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安装新版本

删除以前的大数据群集并安装最新的**azdata**后, 请使用当前部署说明部署新的大数据群集。 有关详细信息, 请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md)。 然后, 还原任何所需的数据库或文件。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么是 SQL Server 大数据群集](big-data-cluster-overview.md)。
