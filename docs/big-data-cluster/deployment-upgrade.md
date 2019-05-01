---
title: 升级到新版本
titleSuffix: SQL Server big data clusters
description: 了解如何升级到新版本的 SQL Server 2019 大数据群集 （预览版）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 604947f1616509f7267450fb3d3ba94f8ce21a97
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759154"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>如何升级 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文指导如何升级到新版本的 SQL Server 大数据群集。 在本文中的步骤专门适用于如何之间预览版本升级。

## <a name="backup-and-delete-the-old-cluster"></a>备份并删除旧群集

目前，大数据群集升级到新版本的唯一方法是手动删除并重新创建群集。 每个版本具有的唯一版本**mssqlctl**不是与以前的版本兼容。 此外，如果旧群集必须下载一个新的节点上的图像，最新的映像不可能与在群集上的较旧映像兼容。 若要升级到最新版本，请使用以下步骤：

1. 在删除之前在旧群集，备份数据，和 HDFS 上的 SQL Server 主实例。 对于 SQL Server 主实例，可以使用[SQL Server 备份和还原](data-ingestion-restore-database.md)。 Hdfs，你[可以使用的数据将复制**curl**](data-ingestion-curl.md)。

1. 删除与旧群集`mssqlctl delete cluster`命令。

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用的版本**mssqlctl**匹配你的群集。 不删除较旧群集使用的较新版本**mssqlctl**。

1. 如果有任何以前版本的**mssqlctl**安装，请务必卸载**mssqlctl**首先在之前安装最新版本。

   如果您在卸载**mssqlctl**对应于 CTP 2.2 或更低的运行：

   ```powershell
   pip3 uninstall mssqlctl
   ```

   CTP 2.3 或更高版本，运行以下命令。 替换`ctp-2.4`在命令中使用的版本**mssqlctl**要卸载：

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt
   ```

1. 安装最新版本**mssqlctl**。 下面的命令安装**mssqlctl** CTP 2.5:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > 对于每个版本的路径**mssqlctl**更改。 即使你安装了**mssqlctl**，则必须重新安装最新的路径中创建新群集之前。

## <a id="mssqlctlversion"></a> 验证 mssqlctl 版本

在部署新的大数据群集之前, 验证您使用的最新版本**mssqlctl**与`--version`参数：

```bash
mssqlctl --version
```

## <a name="install-the-new-release"></a>安装新的版本

删除以前的大数据群集并安装最新版本后**mssqlctl**，使用当前的部署说明部署新的大数据群集。 有关详细信息，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)。 然后，还原任何所需的数据库或文件。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 大数据群集](big-data-cluster-overview.md)。
