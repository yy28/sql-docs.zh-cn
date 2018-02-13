---
title: "要开始使用在 Ubuntu 上的 SQL Server 2017 |Microsoft 文档"
description: "本快速入门演示如何在 Ubuntu 上安装 SQL Server 2017 然后创建并查询使用 sqlcmd 数据库。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.workload: Active
ms.openlocfilehash: e0dc1d24963e1e00018d5b5ac1418d68a4a22577
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>安装 SQL Server，并在 Ubuntu 上创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入门教程，你首先将安装 SQL Server 2017 Ubuntu 16.04。 然后通过连接**sqlcmd**创建第一个数据库和运行查询。

> [!TIP]
> 本教程需要用户输入和 internet 连接。 如果你有兴趣[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装过程，请参阅[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

你必须具有的 Ubuntu 16.04 机**至少 2 GB**的内存。

若要在您自己的计算机上安装 Ubuntu，请转到[http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server)。 你还可以在 Azure 中创建 Ubuntu 虚拟机。 请参阅[创建和管理 Linux Vm 的 Azure cli](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

> [!NOTE]
> 在此期间，[适用于 Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)作为安装目标不支持 Windows 10。

其他系统要求，请参阅[在 Linux 上的 SQL Server 的系统需求](sql-server-linux-setup.md#system)。

## <a id="install"></a>安装 SQL Server

若要在 Ubuntu 上配置 SQL Server ，在终端中运行以下命令安装**mssql server**包。

> [!IMPORTANT]
> 如果你已经安装 CTP 或 RC 版本的 SQL Server 自 2017 年，必须注册一个 GA 存储库之前先删除旧的存储库。 有关详细信息，请参阅[从预览存储库的存储库更改到 GA 存储库](sql-server-linux-change-repo.md)。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > 这是累积更新 (CU) 存储库。 有关你的存储库选项和它们之间的差异的详细信息，请参阅[为在 Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

1. 运行以下命令，安装 SQL Server：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. 软件包安装完成后，运行**mssql conf 安装**命令并按照操作提示设置 SA 密码，并选择你的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 如果你在本教程中尝试 SQL Server 自 2017 年，自由地授予许可的以下版本： 评估、 开发人员和快速。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

1. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

1. 如果你打算远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433）。

此时，SQL Server 正在您 Ubuntu 的计算机上运行并且已准备好使用 ！

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，你需要使用一种工具，可以在 SQL Server 上运行 TRANSACT-SQL 语句进行连接。 以下是 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
   ```

1. 更新源列表，然后运行 unixODBC 开发人员包的安装命令：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-tools unixodbc-dev
   ```

1. 为方便起见，添加`/opt/mssql-tools/bin/`到你的**PATH**境变量。 这使您可以运行工具，而无需指定完整路径。 在登录会话和交互式/非登录会话中运行以下命令以修改**PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd**只是一个用于连接到 SQL Server 并运行查询和执行管理及开发任务的工具。 其他工具包括：
>
> * [SQL Server 操作 Studio （预览版）](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Visual Studio Code](sql-server-linux-develop-use-vscode.md)。
> * [mssql-cli (Preview)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
