---
title: SUSE Linux Enterprise Server 上的 SQL Server 入门
titleSuffix: SQL Server
description: 本快速入门介绍如何在 SUSE Linux Enterprise Server 上安装 SQL Server 2017 或 SQL Server 2019 然后创建和查询使用 sqlcmd 数据库。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: f5c0bb63ce7d188a2587d1a44d863a14308da273
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713578"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>快速入门：安装 SQL Server，在 SUSE Linux Enterprise Server 上创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在此快速入门中，您安装 SQL Server 2017 或 SQL Server 2019 预览版在 SUSE Linux Enterprise Server (SLES) v12 SP2 上。 然后使用连接**sqlcmd**创建第一个数据库和运行查询。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入门，在 SUSE Linux Enterprise Server (SLES) v12 SP2 上安装 SQL Server 2019 预览版。 然后使用连接**sqlcmd**创建第一个数据库和运行查询。

::: moniker-end

> [!TIP]
> 本教程需要用户输入和 Internet 连接。 如果您对[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装感兴趣，请参阅 [Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>先决条件

您必须具有的 SLES v12 SP2 计算机**至少 2 GB**的内存。 必须在文件系统**XFS**或**EXT4**。 其他文件系统，如**BTRFS**，均不受支持。

若要在自己的计算机上安装 SUSE Linux Enterprise Server，请转到[ https://www.suse.com/products/server ](https://www.suse.com/products/server)。 此外可以在 Azure 中创建 SLES 虚拟机。 请参阅[使用 Azure CLI 创建和管理 Linux VM](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，并在对 `az vm create` 的调用中使用 `--image SLES`。

如果以前已安装的 CTP 或 SQL Server 2017 的 RC 版本，必须执行以下步骤之前先删除旧存储库。 有关详细信息，请参阅[配置 Linux 存储库以用于 SQL Server 2017 和 2019年](sql-server-linux-change-repo.md)。

> [!NOTE]
> 在此期间，[适用于 Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)作为安装目标不支持 Windows 10。

其他系统要求，请参阅[Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安装 SQL Server

若要在 SLES 上配置 SQL Server，若要安装的终端中运行以下命令**mssql server**包：

1. 下载 Microsoft SQL Server 2017 SLES 存储库配置文件：

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > 如果你想要试用 SQL Server 2019，则必须改为注册**预览版 (2019)** 存储库。 对于 SQL Server 2019 安装中使用以下命令：
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   > ```

2. 刷新您的存储库。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. 运行以下命令，安装 SQL Server：

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 程序包安装完成后，请运行 **mssql-conf setup** 命令并按提示设置 SA 密码，然后选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 以下 SQL Server 2017 版本自由地授予使用许可：评估、 开发人员版和 Express。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

5. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

6. 如果你打算远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433）。 如果您正在使用 SuSE 防火墙，你需要编辑 **/etc/sysconfig/SuSEfirewall2**配置文件。 修改**FW_SERVICES_EXT_TCP**条目以包括 SQL Server 端口号。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

在此情况下，SQL Server SLES 计算机上运行并已准备好使用 ！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安装 SQL Server

若要在 SLES 上配置 SQL Server，若要安装的终端中运行以下命令**mssql server**包：

1. 下载 Microsoft SQL Server 2019 预览 SLES 存储库配置文件：

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   ```

2. 刷新您的存储库。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. 运行以下命令，安装 SQL Server：

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 程序包安装完成后，请运行 **mssql-conf setup** 命令并按提示设置 SA 密码，然后选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

5. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

6. 如果你打算远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433）。 如果您正在使用 SuSE 防火墙，你需要编辑 **/etc/sysconfig/SuSEfirewall2**配置文件。 修改**FW_SERVICES_EXT_TCP**条目以包括 SQL Server 端口号。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

在此情况下，SQL Server 2019 预览 SLES 计算机上运行并已准备好使用 ！

::: moniker-end


## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，需要使用一个能够在 SQL Server 上运行 Transact-SQL 语句的工具进行连接。 以下步骤安装 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 将 Microsoft SQL Server 存储库添加到 Zypper。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 安装**mssql 工具**使用 unixODBC 开发人员包。

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. 为方便起见，请将 `/opt/mssql-tools/bin/` 添加到 **PATH** 环境变量。 这样就可以在运行工具时不指定完整路径。 请运行以下命令，以便修改登录会话和交互/非登录会话的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
