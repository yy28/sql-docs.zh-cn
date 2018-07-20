---
title: 在 Ubuntu 上的 SQL Server 2017 入门 |Microsoft Docs
description: 本快速入门介绍如何在 Ubuntu 上安装 SQL Server 2017 然后创建和查询使用 sqlcmd 数据库。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 30c05b25301004afbd1d9ed0b2a365b5a37f256d
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101819"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>快速入门： 安装 SQL Server 并在 Ubuntu 上创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入门，首先安装 SQL Server 2017 在 Ubuntu 16.04 上。 然后使用 **sqlcmd** 连接，以创建第一个数据库并运行查询。

> [!TIP]
> 本教程需要用户输入和 internet 连接。 如果您有兴趣[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装过程，请参阅[Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

您必须具有的 Ubuntu 16.04 计算机**至少 2 GB**的内存。

若要在自己的计算机上安装 Ubuntu，请转到[ http://www.ubuntu.com/download/server ](http://www.ubuntu.com/download/server)。 此外可以在 Azure 中创建 Ubuntu 虚拟机。 请参阅[创建和管理 Linux Vm 使用 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

> [!NOTE]
> 在此期间，[适用于 Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)作为安装目标不支持 Windows 10。

其他系统要求，请参阅[Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a id="install"></a>安装 SQL Server

若要在 Ubuntu 上配置 SQL Server ，在终端中运行以下命令安装**mssql server**包。

> [!IMPORTANT]
> 如果以前已安装的 CTP 或 SQL Server 2017 的 RC 版本，必须先注册 GA 存储库之一之前删除旧的存储库。 有关详细信息，请参阅[存储库从预览存储库更改为 GA 存储库](sql-server-linux-change-repo.md)。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > 这是累积更新 (CU) 存储库。 有关存储库的选项和它们之间的差异的详细信息，请参阅[Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

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
   > 如果在本教程中尝试 SQL Server 2017，自由地获得许可的以下版本： Evaluation、 Developer 和 Express。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

1. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

1. 如果你打算远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433）。

在此情况下，SQL Server 在 Ubuntu 计算机上运行并已准备好使用 ！

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库时，需要使用一种工具，可以在 SQL Server 上运行的 Transact SQL 语句进行连接。 以下是 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

使用以下步骤来安装**mssql 工具**Ubuntu 上。 

1. 导入公共存储库 GPG 密钥。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft Ubuntu 存储库。

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 更新源列表，并使用 unixODBC 开发人员包运行安装命令。

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 若要更新到最新版**mssql 工具**运行以下命令：
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **可选**： 添加`/opt/mssql-tools/bin/`到你**路径**bash shell 中的环境变量。

   若要使**sqlcmd/bcp**可从登录会话的 bash shell 访问修改你**路径**中 **~/.bash_profile**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要使**sqlcmd/bcp**能从交互式/非登录会话，bash shell 访问修改**路径**中 **~/.bashrc**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
