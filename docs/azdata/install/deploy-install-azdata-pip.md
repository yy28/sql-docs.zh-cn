---
title: 使用 pip 安装 Azure Data CLI (azdata)
titleSuffix: ''
description: 了解如何通过 pip 安装 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4aa52ebe56cbe4af3d2983a9ed800ebbc1538971
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257440"
---
# <a name="install-azure-data-cli-azdata-with-pip"></a>使用 `pip` 安装 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

本文介绍如何使用 `pip` 在 Windows、Linux 或 macOS/OS X 上安装 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] 工具。

> [!TIP]
> 为了获得更简单的体验，可使用适用于 Windows、Linux（Ubuntu、Debian、RHEL、CentOS、openSUSE 和 SLE 分发）和 macOS 的[包管理器](./deploy-install-azdata.md)安装 `azdata`。

## <a name="prerequisites"></a><a id="prerequisites"></a>先决条件

`azdata` 是使用 Python 编写的命令行实用工具，可让群集管理员通过 REST API 启动和管理数据资源。 所需的 Python 最低版本为 v3.5。 需要 `pip` 来下载并安装 `azdata` 工具。 以下说明提供了 Windows、Linux (Ubuntu) 和 macOS/OS X 的示例。若要在其他平台上安装 Python，请参阅 [Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。 此外，需安装和更新最新版本的 `requests` Python 包：

```bash
pip3 install -U requests
```

## <a name="windows-azdata-installation"></a><a id="windows"></a> Windows `azdata` 安装

1. 在 Windows 客户端上，从 [https://www.python.org/downloads/](https://www.python.org/downloads/) 下载所需的 Python 包。 对于 Python 3.5.3 及更高版本，安装 Python 时还会安装 pip3。

   > [!TIP]
   > 安装 Python3 时，选择将 Python 添加到 `PATH`。 如果没有这样做，可在稍后找到 pip3 所在的位置并手动将其添加到 `PATH`。

1. 打开新的 Windows PowerShell 会话，以便它获取包含 Python 的最新路径。

1. 从 SQL Server 2019 CU5 版本开始，azdata 具有来自服务器的独立语义版本。 如果你在此之前安装了任何以前的 `azdata` 版本，则在安装最新版本之前，务必先卸载这些以前的版本。

   例如，对于 2019-cu4，运行以下命令：

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu4/requirements.txt
   ```

  > [!NOTE]
  > 在前面的示例中，将 `2019-cu6` 替换为你安装的 `azdata` 版本和 CU。 

1. 安装 `azdata`。

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="linux-azdata-installation"></a><a id="linux"></a> Linux `azdata` 安装

在 Linux 上，必须安装 Python 3.5，然后升级 pip。 以下示例介绍了适用于 Ubuntu 的命令。 对于其他 Linux 平台，请参阅 [Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安装必需的 Python 包：

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. 升级 pip3。

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 从 SQL Server 2019 CU5 版本开始，azdata 具有来自服务器的独立语义版本。 如果你在此之前安装了任何以前的 `azdata` 版本，则在安装最新版本之前，务必先卸载这些以前的版本。

   例如，对于 `2019-cu6`，运行以下命令：

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu6/requirements.txt
   ```

  > [!NOTE]
  > 在前面的示例中，将 `2019-cu6` 替换为你安装的 `azdata` 版本和 CU。

1. 安装 `azdata`。

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` 交换机将 `azdata` 安装到 Python 用户安装目录。 这通常是 Linux 上的 `~/.local/bin`。 将此目录添加到路径或导航到用户安装目录并从此处运行 `./azdata`。

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> 在 macOS 或 OS X 上安装 `azdata`

要在 macOS 或 OS X 上安装 `azdata`，请完成以下步骤。 对于每个步骤，请在终端中运行示例。

1. 在 macOS 客户端上，如果尚未安装 [Homebrew](https://brew.sh)，请进行安装：

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. 安装 Python 和 pip，最低版本为 3.0：

   ```bash
   brew install python3
   ```

1. 安装依赖项：

   ```bash
   pip3 install -U requests
   brew install freetds
   ```

1. 从 SQL Server 2019 CU5 版本开始，azdata 具有来自服务器的独立语义版本。 如果你在此之前安装了任何以前的 `azdata` 版本，则在安装最新版本之前，务必先卸载这些以前的版本。 例如，以下命令删除 `azdata` 的 RC1 版本：

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 安装 Azure Data CLI。

   ```bash
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

将 azdata 用于[已启用 Azure Arc 的数据服务](/azure/azure-arc/data/)
