---
title: "要开始使用在 Ubuntu 上的 SQL Server 2017 |Microsoft 文档"
description: "此快速入门教程演示如何在 Ubuntu 上安装 SQL Server 2017 然后创建并查询使用 sqlcmd 数据库。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 052a2f0a7618c5e160d3c17a3a1efd7d7a4b3fd6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>安装 SQL Server，并在 Ubuntu 上创建数据库

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

在此快速入门教程中，你首先将安装 SQL Server 自 2017 年 1 RC2 Ubuntu 16.04。 然后通过连接**sqlcmd**创建第一个数据库和运行查询。

> [!TIP]
> 本教程需要用户输入和 internet 连接。 如果你有兴趣[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装过程，请参阅[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

你必须具有的 Ubuntu 机**至少 3.25 GB**的内存。

若要在您自己的计算机上安装 Ubuntu，请转到[http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server)。 你还可以在 Azure 中创建 Ubuntu 虚拟机。 请参阅[创建和管理 Linux Vm 的 Azure cli](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

其他系统要求，请参阅[在 Linux 上的 SQL Server 的系统需求](sql-server-linux-setup.md#system)。

## <a id="install"></a>安装 SQL Server

若要配置 SQL Server 在 Ubuntu 上，在安装终端中运行以下命令**mssql server**包。

1. 导入公共存储库 GPG 密钥：

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list)"
   ```

1. 运行以下命令，安装 SQL Server：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. 运行包安装完成后**mssql conf 安装**并按照提示设置 SA 密码并选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

   > [!TIP]
   > 在安装时 RC2，需要没有购买的许可证尝试的任何版本。 因为它是预发布版本，而不考虑你选择的版本将显示以下消息：
   >
   > `This is an evaluation version.  There are [175] days left in the evaluation period.`
   >
   > 此消息不会反映你选择的版本。 它与在预览期 for RC2。

1. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

1. 如果你计划远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433年）。

此时，SQL Server 正在您 Ubuntu 的计算机上运行并且已准备好使用 ！

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，你需要使用一种工具，可以在 SQL Server 上运行 TRANSACT-SQL 语句进行连接。 以下步骤安装 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 导入公共存储库 GPG 密钥：

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
   ```

1. 更新源列表，然后运行 unixODBC 开发人员包的安装命令：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-tools unixodbc-dev
   ```

1. 为方便起见，添加`/opt/mssql-tools/bin/`到你**路径**环境变量。 这使您可以运行工具，而无需指定完整路径。 运行以下命令以修改**路径**登录会话和交互式/非-登录会话：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd**是用于连接到 SQL Server 以运行查询并执行管理和开发任务只在一个工具。 其他工具包括[SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)和[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
