---
title: 开始使用 Red Hat Enterprise Linux 上的 SQL Server 2017 |Microsoft Docs
description: 本快速入门介绍如何在 Red Hat Enterprise Linux 上安装 SQL Server 2017，以及如何使用 sqlcmd 创建和查询数据库。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 4438184f6e14af1097ff05ea6e463f626025bb46
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103737"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入门：在 Red Hat 上安装 SQL Server 并创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入门中，请首先在 Red Hat Enterprise Linux (RHEL) 7.3+ 上安装 SQL Server 2017，然后使用 **sqlcmd** 进行连接，以便创建第一个数据库并运行查询。

> [!TIP]
> 本教程需要用户输入和 Internet 连接。如果您对[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装感兴趣，请参阅 [Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

必须使用 RHEL 7.3 或 7.4 计算机，且必须拥有**至少 2 GB** 的内存。

若要在自己的计算机上安装 Red Hat Enterprise Linux，请访问 [ http://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。也可在 Azure 中创建 RHEL 虚拟机。请参阅[使用 Azure CLI 创建和管理 Linux VM](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，并在对 `az vm create` 的调用中使用 `--image RHEL`。

其他系统要求，请参阅[Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

## <a id="install"></a>安装 SQL Server

若要在 RHEL 上配置 SQL Server，请在终端中运行以下命令，以便安装** mssql server **包：

> [!IMPORTANT]
> 如果之前安装了 CTP 或 RC 版 的 SQL Server 2017，则在注册某个 GA 存储库之前，必须先删除旧的存储库(mssql-server.repo)。有关详细信息，请参阅[将存储库从预览版存储库更改为 GA 版存储库](sql-server-linux-change-repo.md)。

1. 下载 Microsoft SQL Server Red Hat 存储库配置文件：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > 这是累积更新 (CU) 存储库。有关存储库选项及其差异的详细信息，请参阅[配置 Linux 上的 SQL Server 的存储库](sql-server-linux-change-repo.md)。

1. 运行以下命令，安装 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

1. 程序包安装完成后，请运行 **mssql-conf setup** 命令并按提示设置 SA 密码，然后选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > 若要在本教程中尝试 SQL Server 2017，可使用下述免费许可版本：Evaluation、Developer 和 Express。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

1. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```
   
1. 若要允许远程连接，请在 RHEL 上打开防火墙上的 SQL Server 端口。默认的 SQL Server 端口为 TCP 1433。如果对防火墙使用 **FirewallD**，可以使用以下命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

SQL Server 目前正在 RHEL 计算机上运行，可以使用了！

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，需要使用一个能够在 SQL Server 上运行 Transact-SQL 语句的工具进行连接。以下步骤安装 SQL Server 命令行工具：[sqlcmd](../tools/sqlcmd-utility.md) 和 [bcp](../tools/bcp-utility.md)。

1. 下载 Microsoft Red Hat 存储库配置文件。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 如果你有旧版**mssql 工具**安装，请删除任何较旧的 unixODBC 包。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 运行以下命令以安装 **mssql-tools** 和 unixODBC 开发人员包。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 为方便起见，请将 `/opt/mssql-tools/bin/` 添加到 **PATH** 环境变量。这样就可以在运行工具时不指定完整路径。请运行以下命令，以便修改登录会话和交互/非登录会话的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
