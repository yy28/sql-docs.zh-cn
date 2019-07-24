---
title: 安装 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安装用于安装和管理 SQL Server 2019 大数据群集 (预览版) 的 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426437"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>安装 azdata 以管理 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何在 Windows 或 Linux 上安装 CTP 3.2 的**azdata**工具。

## <a id="prerequisites"></a> 先决条件

**azdata**是用 Python 编写的命令行实用程序, 群集管理员可以通过 REST api 启动和管理大数据群集。 所需的最小 Python 版本为3.5。 还`pip`必须使用来下载和安装**azdata**工具。 以下说明提供了 Windows 和 Ubuntu 的示例。 若要在其他平台上安装 Python, 请参阅[Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。
此外, 还必须安装和更新最新版本的*请求*Python 包:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 如果要安装较新版本的大数据群集, 则必须在升级**azdata**并安装新版本*之前*备份数据并删除旧群集。 有关详细信息, 请参阅[升级到新版本](deployment-upgrade.md)。

## <a id="windows"></a>Windows azdata 安装

1. 在 Windows 客户端上, 从中[https://www.python.org/downloads/](https://www.python.org/downloads/)下载所需的 Python 包。 对于 Python 3.5.3 和更高版本, 安装 Python 时也会安装 pip3。 

   > [!TIP] 
   > 安装 Python3 时, 请选择将 Python 添加到你的**路径**。 如果不这样做, 可以在以后找到 pip3 所在位置, 并手动将其添加到你的**路径**。

1. 打开新的 Windows PowerShell 会话, 以便它能够获取其中包含 Python 的最新路径。

1. 如果安装了任何以前版本的工具 (previosly 名为**mssqlctl**), 请先卸载它, 然后再安装最新版本的**azdata**。

   对于 CTP 3.1 或更低版本, 请运行以下命令。 将`ctp3.1`命令中的替换为要卸载的**mssqlctl**的版本。 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果你安装了任何以前版本的**azdata** , 请先卸载它, 然后再安装最新版本。

   对于 CTP 3.2 或更高版本, 请运行以下命令。 将`ctp3.2`命令中的替换为要卸载的**azdata**的版本。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 通过以下命令安装**azdata** :

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Linux azdata 安装

在 Linux 上, 必须安装 Python 3.5, 然后升级 pip。 下面的示例演示适用于 Ubuntu 的命令。 对于其他 Linux 平台, 请参阅[Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安装必要的 Python 包:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. 升级 pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果安装了任何以前版本的工具 (以前称为**mssqlctl**), 请先卸载它, 然后再安装最新版本的**azdata**。

   对于 CTP 3.1 或更低版本, 请运行以下命令。 将`ctp3.1`命令中的替换为要卸载的**mssqlctl**的版本。 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果你安装了任何以前版本的**azdata** , 请先卸载它, 然后再安装最新版本。

   对于 CTP 3.2 或更高版本, 请运行以下命令。 将`ctp3.2`命令中的替换为要卸载的**azdata**的版本。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 通过以下命令安装**azdata** :

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > 此`--user`开关将 azdata 安装到 Python 用户安装目录。 这通常`~/.local/bin`是在 Linux 上。 将此目录添加到你的路径, 或导航到用户安装目录并`./azdata`从该目录中运行。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
