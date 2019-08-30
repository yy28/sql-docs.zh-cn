---
title: 在 Linux 上安装 azdata 与安装程序
titleSuffix: SQL Server big data clusters
description: 了解如何安装 azdata 工具, 以便安装和管理[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版) 安装程序 (预览版)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11e4851294ac8ffd8efa66e2156dcd47bce3aa0
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160686"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>在`azdata` Linux 上[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]安装以进行管理

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何安装`azdata` Linux 上的 SQL Server 2019 大数据群集候选发布版本。 在这些包管理器可用之前, `azdata`需要`pip`安装。

包管理器适用于各种操作系统和分发。

- 适用于 Linux (Ubuntu) [, `azdata`随`apt`一起安装](#azdata-apt)

此时, 没有可在其他操作系统或分发上安装`azdata`的包管理器。 对于这些平台, 请[参阅`azdata`安装而不安装程序包管理器](./deploy-install-azdata.md)。

## <a id="linux"></a>为`azdata` Linux 安装

`azdata`安装包适用于 Ubuntu `apt`。

### <a id="azdata-apt"></a>安装`azdata` with apt (Ubuntu)

>[!NOTE]
>`azdata`该包不使用系统 python, 而是安装其自己的 python 解释器。

1. 获取安装过程所需的包:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 下载并安装签名密钥:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```

3. `azdata`添加存储库信息:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. 更新存储库信息并`azdata`安装:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 验证安装:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

仅`azdata`限升级:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>卸载

1. 卸载并删除 apt:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. `azdata`删除存储库信息:

    >[!NOTE]
    >如果计划在将来安装`azdata` , 则不需要执行此步骤

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 删除签名密钥:

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. 删除与 Azdata CLI 一起安装的所有不需要的依赖项:

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]是？](big-data-cluster-overview.md)。
