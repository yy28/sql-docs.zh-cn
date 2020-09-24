---
title: 在 Linux 上使用安装程序安装 azdata
titleSuffix: ''
description: 了解如何通过安装程序 (Linux) 安装 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2dc1c3d58ee5f7b6ea032a2e41f7c18431229881
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914967"
---
# <a name="install-azdata-with-apt"></a>使用 apt 安装 `azdata`

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/azdata.md)]

本文介绍如何在 Linux 上安装 `azdata`。 在这些包管理器可用之前，需要 `pip` 来安装 `azdata`。

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-azdata-for-linux"></a><a id="linux"></a>安装适用于 Linux 的 `azdata`

`azdata` 安装包适用于具有 `apt` 的 Ubuntu。

### <a name="install-azdata-with-apt-ubuntu"></a><a id="azdata-apt"></a>使用 apt (Ubuntu) 安装 `azdata`

>[!NOTE]
>`azdata` 包不使用系统 Python，而是安装其自己的 Python 解释器。

1. 获取安装过程所需的包：

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
    ```

2. 下载并安装签名密钥：

    ```bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
    ```

3. 添加 `azdata` 存储库信息。

   对于 Ubuntu 16.04 客户端运行：
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   对于 Ubuntu 18.04 客户端运行：
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
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

### <a name="update"></a>更新

仅升级 `azdata`：

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>卸载

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

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

将 azdata 用于[已启用 Azure Arc 的数据服务](/azure/azure-arc/data/)