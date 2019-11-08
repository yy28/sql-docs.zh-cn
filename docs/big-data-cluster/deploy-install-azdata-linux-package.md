---
title: 在 Linux 上使用安装程序安装 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何使用安装程序 (Linux) 安装 azdata 工具，以安装和管理 SQL Server 大数据群集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8d4a34e89de7c136e1e80b43929531a2d10eba
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532065"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>安装 `azdata` 以管理 Linux 上的 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何在 Linux 上安装用于 SQL Server 2019 大数据群集的 `azdata`。 在这些包管理器可用之前，需要 `pip` 来安装 `azdata`。

包管理器适用于各种操作系统和发行版。

- 对于 Windows 和 Linux （Ubuntu 发行版），可以使用[包管理器](./deploy-install-azdata-installer.md)进行安装，以获得更简单的体验。
- 对于 Linux (Ubuntu)，[使用 `apt` 安装 `azdata`](#azdata-apt)

目前，没有可在其他操作系统或发行版上安装 `azdata` 的包管理器。 对于这些平台，请参阅[不使用包管理器安装 `azdata`](./deploy-install-azdata.md)。

## <a id="linux"></a>安装适用于 Linux 的 `azdata`

`azdata` 安装包适用于具有 `apt` 的 Ubuntu。

### <a id="azdata-apt"></a>使用 apt (Ubuntu) 安装 `azdata`

>[!NOTE]
>`azdata` 包不使用系统 Python，而是安装其自己的 Python 解释器。

1. 获取安装过程所需的包：

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 下载并安装签名密钥：

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. 添加 `azdata` 存储库信息：

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

4. 更新存储库信息并安装 `azdata`：

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 验证安装：

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

仅升级 `azdata`：

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

1. 通过 apt-get remove 卸载：

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. 删除 `azdata` 存储库信息：

    >[!NOTE]
    >如果计划在将来安装 `azdata`，则不需要执行此步骤

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 删除签名密钥：

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. 删除与 Azdata CLI 一起安装的所有不需要的依赖项：

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
