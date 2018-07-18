---
title: 开始使用 Red Hat Enterprise Linux 上的 SQL Server 2017 |Microsoft Docs
description: 本快速入门介绍如何在 Red Hat Enterprise Linux 上安装 SQL Server 2017 然后创建和查询使用 sqlcmd 数据库。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: de149b0a75a550101e761baa109bc07dac062fcd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020414"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入门： 安装 SQL Server 和 Red Hat 上创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入门，首先安装 SQL Server 2017 上 Red Hat Enterprise Linux (RHEL) 7.3 +。 然后使用 **sqlcmd** 连接，以创建第一个数据库并运行查询。

> [!TIP]
> 本教程需要用户输入和 internet 连接。 如果您有兴趣[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装过程，请参阅[Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

您必须具有 RHEL 7.3 或 7.4 计算机**至少 2 GB**的内存。

若要在自己的计算机上安装 Red Hat Enterprise Linux，请转到[ http://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 此外可以在 Azure 中创建 RHEL 虚拟机。 请参阅[创建和使用 Azure CLI 管理 Linux Vm](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，并使用`--image RHEL`对的调用中`az vm create`。

其他系统要求，请参阅[Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a id="install"></a>安装 SQL Server

若要在 RHEL 上配置 SQL Server，若要安装的终端中运行以下命令**mssql server**包：

> [!IMPORTANT]
> 如果以前已安装的 CTP 或 SQL Server 2017 的 RC 版本，必须先注册 GA 存储库之一之前删除旧的存储库。 有关详细信息，请参阅[存储库从预览存储库更改为 GA 存储库](sql-server-linux-change-repo.md)。

1. 下载 Microsoft SQL Server Red Hat 存储库配置文件：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > 这是累积更新 (CU) 存储库。 有关存储库的选项和它们之间的差异的详细信息，请参阅[Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

1. 运行以下命令，安装 SQL Server：

   ```bash
   sudo yum install -y mssql-server
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
   
1. 若要允许远程连接，请在 RHEL 上打开防火墙上的 SQL Server 端口。 默认的 SQL Server 端口为 TCP 1433。 如果使用的**FirewallD**对于防火墙中，可以使用以下命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

在此情况下，SQL Server 在 RHEL 计算机上运行并已准备好使用 ！

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库时，需要使用一种工具，可以在 SQL Server 上运行的 Transact SQL 语句进行连接。 以下是 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 下载 Microsoft Red Hat 存储库配置文件。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 如果你有旧版**mssql 工具**安装，请删除任何较旧的 unixODBC 包。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 运行以下命令以安装**mssql 工具**使用 unixODBC 开发人员包。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 为方便起见，添加`/opt/mssql-tools/bin/`到你的**PATH**境变量。 这使您无需指定完整路径运行工具。 在登录会话和交互式/非登录会话中运行以下命令以修改**PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd**只是一个用于连接到 SQL Server 并运行查询和执行管理及开发任务的工具。 其他工具包括：
>
> * [SQL Server Operations Studio（预览版）](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-manage-ssms.md)
> * [Visual Studio Code](sql-server-linux-develop-use-vscode.md)。
> * [mssql-cli（预览版）](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
