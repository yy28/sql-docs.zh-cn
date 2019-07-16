---
title: 安装 mssqlctl
titleSuffix: SQL Server big data clusters
description: 了解如何安装 mssqlctl 工具用于安装和管理 SQL Server 2019 大数据群集 （预览版）。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3be1987baed27aeb49b03942ca3c4f07c2b0ce0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958526"
---
# <a name="install-mssqlctl-to-manage-sql-server-big-data-clusters"></a>安装 mssqlctl 来管理 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何安装**mssqlctl**对于在 Windows 或 Linux 的 CTP 3.1 工具。

**mssqlctl**是启用群集管理员若要启动和管理大数据群集通过 REST Api 以 Python 编写的命令行实用程序。 所需的最小的 Python 版本是 3.5 版。 您还必须拥有`pip`用于下载并安装**mssqlctl**工具。 下面的说明为 Windows 和 Ubuntu 提供示例。 在其他平台上安装 Python，请参阅[Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

> [!IMPORTANT]
> 如果要安装较新版本的大数据群集，必须备份您的数据并删除旧的群集*之前*升级**mssqlctl**和安装新版本。 有关详细信息，请参阅[升级到新的发行版](deployment-upgrade.md)。

## <a id="windows"></a> Windows mssqlctl 安装

1. Windows 客户端上下载必需的 Python 包从[ https://www.python.org/downloads/ ](https://www.python.org/downloads/)。 Python3.5.3 和更高版本，pip3 也会安装时安装 Python。 

   > [!TIP] 
   > 在安装时 Python3，选择要将 Python 添加到您**路径**。 如果不这样做，可以更高版本查找 pip3 所在的位置并手动将其添加到您**路径**。

1. 打开新的 Windows PowerShell 会话，以便获取在其中与 Python 配合使用的最新路径。

1. 如果有任何以前版本的**mssqlctl**安装，请务必卸载**mssqlctl**首先在之前安装最新版本。

   如果您在卸载**mssqlctl**对应于 CTP 2.2 或更低版本运行：

   ```powershell
   pip3 uninstall mssqlctl
   ```

   CTP 2.3 或更高版本，运行以下命令。 替换`ctp3.0`在命令中使用的版本**mssqlctl**要卸载。 如果版本在 CTP 3.0 之前，请添加短划线之前的版本编号 (例如， `ctp-2.5`)。

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. 安装**mssqlctl**使用以下命令：

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

## <a id="linux"></a> Linux mssqlctl 安装

在 Linux 上，你必须安装 Python 3.5，然后再升级 pip。 下面的示例显示了适用于 Ubuntu 的命令。 有关其他 Linux 平台，请参阅[Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安装所需的 Python 包：

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. 升级 pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果有任何以前版本的**mssqlctl**安装，请务必卸载**mssqlctl**首先在之前安装最新版本。

   如果您在卸载**mssqlctl**对应于 CTP 2.2 或更低版本运行：

   ```powershell
   pip3 uninstall mssqlctl
   ```

   CTP 2.3 或更高版本，运行以下命令。 替换`ctp3.0`在命令中使用的版本**mssqlctl**要卸载。 如果版本在 CTP 3.0 之前，请添加短划线之前的版本编号 (例如， `ctp-2.5`)。

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. 安装**mssqlctl**使用以下命令：

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt --user
   ```

   > [!NOTE]
   > `--user`开关将 mssqlctl 安装到 Python 用户安装目录。 这通常是`~/.local/bin`Linux 上。 可以将此目录添加到你的路径或导航到用户的安装目录并运行`./mssqlctl`从那里。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
