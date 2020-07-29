---
title: 使用 pip 安装 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安装 azdata 工具以使用 pip 安装和管理大数据群集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 034514c13a65171fca9eb1fc20b6c496329816a1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773630"
---
# <a name="install-azdata-with-pip"></a>使用 `pip` 安装 `azdata`

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文介绍如何使用 `pip` 在 Windows 或 Linux 上安装 `azdata` 工具。

对于 Windows 和 Linux （Ubuntu 发行版），可以使用[包管理器](./deploy-install-azdata-installer.md)进行安装，以获得更简单的体验。

## <a name="prerequisites"></a><a id="prerequisites"></a>先决条件

`azdata` 是使用 Python 编写的命令行实用工具，可让群集管理员通过 REST API 启动和管理大数据群集。 所需的 Python 最低版本为 v3.5。 需要 `pip` 来下载并安装 `azdata` 工具。 以下说明提供 Windows 和 Ubuntu 示例。 若要在其他平台上安装 Python，请参阅 [Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。
此外，需安装和更新最新版本的 `requests` Python 包：

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 如果要安装较新版本的大数据群集，需在升级 `azdata` 和安装新版本之前备份数据并删除旧群集。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

## <a name="windows-azdata-installation"></a><a id="windows"></a> Windows `azdata` 安装

1. 在 Windows 客户端上，从 [https://www.python.org/downloads/](https://www.python.org/downloads/) 下载所需的 Python 包。 对于 python 3.5.3 及更高版本，安装 Python 时还会安装 pip3。 

   > [!TIP] 
   > 安装 Python3 时，选择将 Python 添加到 `PATH`。 如果没有这样做，可在稍后找到 pip3 所在的位置并手动将其添加到 `PATH`。

1. 打开新的 Windows PowerShell 会话，以便它获取包含 Python 的最新路径。

1. 如果安装了以前的 `azdata` 版本，那么在安装最新版本之前，必须先卸载以前的版本。

   对于 CTP 3.2 或 RC1，请运行以下命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   或
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 使用以下命令安装 `azdata`：

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

1. 升级 pip3：

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果安装了以前的 `azdata` 版本，那么在安装最新版本之前，必须先卸载以前的版本。

   对于 CTP 3.2 或 RC1，请运行以下命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   或
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 使用以下命令安装 `azdata`：

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` 交换机将 `azdata` 安装到 Python 用户安装目录。 这通常是 Linux 上的 `~/.local/bin`。 将此目录添加到路径或导航到用户安装目录并从此处运行 `./azdata`。

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> 在 macOS 或 OS X 上安装 `azdata`

要在 macOS 或 OS X 上安装 `azdata`，请完成以下步骤。 对于每个步骤，请在终端中运行示例。

1. 在 macOS 客户端上，如果尚未安装 [Homebrew](https://brew.sh)，请进行安装：

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. 安装 Python 和 pip，最低版本为 3.0：

   ```
   brew install python3
   ```

1. 安装依赖项：

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. 如果安装了以前版本的 `azdata` 工具，那么在安装最新版本之前，必须先卸载以前的版本。 以下命令将删除 `azdata` 的版本。

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 使用以下命令安装 `azdata`：

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
