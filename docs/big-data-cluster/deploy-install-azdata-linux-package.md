---
title: 在 Linux 上安装 azdata 与安装程序
titleSuffix: SQL Server big data clusters
description: 了解如何安装 azdata 工具，以便安装和 @no__t 管理安装程序（预览版）的（预览版）。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2795178cb975ecb620528c4a5dc8715b70d447fd
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342015"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>安装 `azdata` 以管理 Linux 上的 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何安装 Linux 上的 SQL Server 2019 大数据群集候选发布的 `azdata`。 在这些包管理器可用之前，必须 @no__t 安装 @no__t 0。

包管理器适用于各种操作系统和分发。

- 对于 Linux （Ubuntu），请[安装 `apt` `azdata`](#azdata-apt)

目前，没有包管理器可在其他操作系统或分发上安装 `azdata`。 对于这些平台，请参阅[安装不带程序包管理器的 `azdata`](./deploy-install-azdata.md)。

## <a id="linux"></a>安装适用于 Linux 的 `azdata`

`azdata` 安装包可用于带 @no__t 的 Ubuntu。

### <a id="azdata-apt"></a>安装 `azdata` with apt （Ubuntu）

>[!NOTE]
>@No__t-0 包不使用系统 Python，而是安装其自己的 Python 解释器。

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
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
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

仅 @no__t 升级：

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

1. 卸载并删除 apt：

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. 删除 @no__t 的存储库信息：

    >[!NOTE]
    >如果计划在将来安装 @no__t 0，则不需要执行此步骤

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
