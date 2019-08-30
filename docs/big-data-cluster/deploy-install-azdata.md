---
title: 使用 pip 安装 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安装用于通过 pip 进行安装和管理[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版) 的 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a72e2ab39a17adef6c330f1ae17dcdc8a5dd8ddf
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160736"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>`azdata`使用安装[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]`pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何使用`azdata` `pip`在 Windows 或 Linux 上安装候选发布的工具。

## <a id="prerequisites"></a> 先决条件

`azdata`是用 Python 编写的命令行实用程序, 使群集管理员能够通过 REST Api 启动和管理大数据群集。 所需的 Python 最低版本为 v3.5。 还`pip`必须使用来下载和安装`azdata`工具。 以下说明提供 Windows 和 Ubuntu 示例。 若要在其他平台上安装 Python，请参阅 [Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。
此外，还必须安装和更新最新版本的 Python *requests* 包：
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 如果要安装较新版本的大数据群集, 则必须在升级`azdata`和安装新版本*之前*备份数据并删除旧的群集。 有关详细信息，请参阅[升级到新版本](deployment-upgrade.md)。

## <a id="windows"></a>Windows `azdata`安装

1. 在 Windows 客户端上，从 [https://www.python.org/downloads/](https://www.python.org/downloads/) 下载所需的 Python 包。 对于 python 3.5.3 及更高版本，安装 Python 时还会安装 pip3。 

   > [!TIP] 
   > 安装 Python3 时，选择将 Python 添加到 **PATH**。 如果没有这样做，可在稍后找到 pip3 所在的位置并手动将其添加到 **PATH**。

1. 打开新的 Windows PowerShell 会话，以便它获取包含 Python 的最新路径。

1. 如果安装了任何以前版本的工具 (在 CTP 3.2 之前), 请首先卸载该工具, 然后安装最新版本的`azdata`。 以下命令删除**mssqlctl**的 CTP 3.1 版本。

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果你安装了任何以前版本`azdata`的, 请务必先卸载该版本, 然后再安装最新版本。

   对于 CTP 3.2, 请运行以下命令。

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. 安装`azdata`以下命令:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Linux `azdata`安装

在 Linux 上，必须安装 Python 3.5，然后升级 pip。 以下示例介绍了适用于 Ubuntu 的命令。 对于其他 Linux 平台，请参阅 [Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安装必需的 Python 包：

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip
   ```

1. 升级 pip3：

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果安装了任何以前版本的工具 (在 CTP 3.2 之前), 请首先卸载该工具, 然后安装最新版本的`azdata`。 以下命令删除**mssqlctl**的 CTP 3.1 版本。

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果你安装了任何以前版本`azdata`的, 请务必先卸载该版本, 然后再安装最新版本。

   对于 CTP 3.2, 请运行以下命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. 安装`azdata`以下命令:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > 交换机将安装`azdata`到 Python 用户安装目录中。 `--user` 这通常是 Linux 上的 `~/.local/bin`。 将此目录添加到路径或导航到用户安装目录并从此处运行 `./azdata`。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]是？](big-data-cluster-overview.md)。
