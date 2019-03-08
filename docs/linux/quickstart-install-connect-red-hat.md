---
title: Red Hat Enterprise Linux 上的 SQL Server 入门
titleSuffix: SQL Server
description: 本快速入门介绍如何在 Red Hat Enterprise Linux 上安装 SQL Server 2017 或 SQL Server 2019 然后创建和查询使用 sqlcmd 数据库。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux, seodec18
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 03e3b5d578c8fee68098674e9b82501a290bafda
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579237"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入门：安装 SQL Server 和 Red Hat 上创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在此快速入门中，您安装 SQL Server 2017 或 SQL Server 2019 上 Red Hat Enterprise Linux (RHEL) 7.3 +。 然后使用连接**sqlcmd**创建第一个数据库和运行查询。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在此快速入门中，您安装 SQL Server 2019 preview 上 Red Hat Enterprise Linux (RHEL) 7.3 +。 然后使用连接**sqlcmd**创建第一个数据库和运行查询。

::: moniker-end

> [!TIP]
> 本教程需要用户输入和 Internet 连接。 如果您对[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装感兴趣，请参阅 [Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

必须使用 RHEL 7.3 或 7.4 计算机，且必须拥有**至少 2 GB** 的内存。

若要在自己的计算机上安装 Red Hat Enterprise Linux，请访问[ https://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 也可在 Azure 中创建 RHEL 虚拟机。 请参阅[使用 Azure CLI 创建和管理 Linux VM](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，并在对 `az vm create` 的调用中使用 `--image RHEL`。

如果以前已安装的 CTP 或 SQL Server 2017 的 RC 版本，必须执行以下步骤之前先删除旧存储库。 有关详细信息，请参阅[配置 Linux 存储库以用于 SQL Server 2017 和 2019年](sql-server-linux-change-repo.md)。

其他系统要求，请参阅[Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安装 SQL Server

若要在 RHEL 上配置 SQL Server，请在终端中运行以下命令，以便安装**mssql server**包：

1. 下载 Microsoft SQL Server 2017 Red Hat 存储库配置文件：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > 如果你想要试用 SQL Server 2019，则必须改为注册**预览版 (2019)** 存储库。 对于 SQL Server 2019 安装中使用以下命令：
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   > ```

2. 运行以下命令，安装 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

3. 程序包安装完成后，请运行 **mssql-conf setup** 命令并按提示设置 SA 密码，然后选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 以下 SQL Server 2017 版本自由地授予使用许可：评估、 开发人员版和 Express。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

4. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允许远程连接，请在 RHEL 上打开防火墙上的 SQL Server 端口。 默认的 SQL Server 端口为 TCP 1433。 如果对防火墙使用 **FirewallD**，可以使用以下命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

SQL Server 目前正在 RHEL 计算机上运行，可以使用了！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安装 SQL Server

若要在 RHEL 上配置 SQL Server，请在终端中运行以下命令，以便安装**mssql server**包：

1. 下载 Microsoft SQL Server 2019 预览 Red Hat 存储库配置文件：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   ```

2. 运行以下命令，安装 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

3. 程序包安装完成后，请运行 **mssql-conf setup** 命令并按提示设置 SA 密码，然后选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

4. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允许远程连接，请在 RHEL 上打开防火墙上的 SQL Server 端口。 默认的 SQL Server 端口为 TCP 1433。 如果对防火墙使用 **FirewallD**，可以使用以下命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

在此情况下，SQL Server 2019 预览 RHEL 计算机上运行并已准备好使用 ！

::: moniker-end

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，需要使用一个能够在 SQL Server 上运行 Transact-SQL 语句的工具进行连接。 以下步骤安装 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

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

1. 为方便起见，请将 `/opt/mssql-tools/bin/` 添加到 **PATH** 环境变量。 这样就可以在运行工具时不指定完整路径。 请运行以下命令，以便修改登录会话和交互/非登录会话的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
