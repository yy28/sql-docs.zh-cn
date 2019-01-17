---
title: 安装 mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何安装 mssqlctl 工具用于安装和管理 SQL Server 2019 大数据群集 （预览版）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/15/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aec8f030a996e5dd86c44a5a655e98d4926988ed
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361407"
---
# <a name="install-mssqlctl-to-manage-sql-server-2019-big-data-clusters"></a>安装 mssqlctl 来管理 SQL Server 2019 大数据群集

本文介绍如何安装**mssqlctl** Windows 或 Linux 上的工具。

**mssqlctl**是启用群集管理员若要启动和管理大数据群集通过 REST Api 以 Python 编写的命令行实用程序。 所需的最小的 Python 版本是 3.5 版。 您还必须拥有`pip`用于下载并安装**mssqlctl**工具。 下面的说明为 Windows 和 Ubuntu 提供示例。 在其他平台上安装 Python，请参阅[Python 文档](https://wiki.python.org/moin/BeginnersGuide/Download)。

> [!IMPORTANT]
> 如果安装了以前版本的**mssqlctl**，则必须删除该群集*之前*升级**mssqlctl**和安装新版本。 有关详细信息，请参阅[升级到新的发行版](deployment-guidance.md#upgrade)。

## <a id="windows"></a> Windows mssqlctl 安装

1. Windows 客户端上下载必需的 Python 包从[ https://www.python.org/downloads/ ](https://www.python.org/downloads/)。 Python3.5.3 和更高版本，pip3 也会安装时安装 Python。 

   > [!TIP] 
   > 在安装时 Python3，选择要将 Python 添加到您**路径**。 如果不这样做，可以更高版本查找 pip3 所在的位置并手动将其添加到您**路径**。

1. 打开新的 Windows PowerShell 会话，以便获取在其中与 Python 配合使用的最新路径。

2. 安装**mssqlctl**使用以下命令：

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl
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
   
1. 安装**mssqlctl**使用以下命令：

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl --user
   ```
   
   > [!NOTE]
   > `--user`开关将 mssqlctl 安装到 Python 用户安装目录。 这通常是`~/.local/bin`Linux 上。 可以将此目录添加到你的路径或导航到用户的安装目录并运行`./mssqlctl`从那里。
   
## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
