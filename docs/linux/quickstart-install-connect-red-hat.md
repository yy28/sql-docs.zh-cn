---
title: Red Hat Enterprise Linux 上的 SQL Server 入门
titleSuffix: SQL Server
description: 本快速入门介绍如何在 Red Hat Enterprise Linux 上安装 SQL Server 2017 或 SQL Server 2019，然后使用 sqlcmd 创建和查询数据库。
author: VanMSFT
ms.author: vanto
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 38df65ffefbc0ed264d631214025059449d84b35
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910498"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入门：在 Red Hat 上安装 SQL Server 并创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入门中，将在 Red Hat Enterprise Linux (RHEL) 上安装 SQL Server 2017 或 SQL Server 2019。 然后使用 **sqlcmd** 进行连接，以创建第一个数据库并运行查询。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入门中，将在 Red Hat Enterprise Linux (RHEL) 7.3+ 上安装 SQL Server 2019 预览版。 然后使用 **sqlcmd** 进行连接，以创建第一个数据库并运行查询。

::: moniker-end

> [!TIP]
> 本教程需要用户输入和 Internet 连接。 如果对[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装过程感兴趣，请参阅 [Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必备条件

必须拥有 RHEL 7.3、7.4、7.5 或 7.6 计算机（具有**至少 2 GB** 内存）。

若要在自己的计算机上安装 Red Hat Enterprise Linux，请转至 [https://access.redhat.com/products/red-hat-enterprise-linux/evaluation](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 也可以在 Azure 中创建 RHEL 虚拟机。 请参阅[使用 Azure CLI 创建和管理 Linux VM](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，并在对 `az vm create` 的调用中使用 `--image RHEL`。

如果以前安装了 SQL Server 2017 的 CTP 或 RC 版本，则必须先删除旧存储库，然后再执行这些步骤。 有关详细信息，请参阅[为 SQL Server 2017 和 2019 配置 Linux 存储库](sql-server-linux-change-repo.md)。

有关其他系统要求，请参阅 [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安装 SQL Server

若要在 RHEL 上配置 SQL Server，请在终端中运行以下命令以安装 **mssql-server** 包：

1. 下载 Microsoft SQL Server 2017 Red Hat 存储库配置文件：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > 如果想试用 SQL Server 2019，则必须改为注册**预览版 (2019)** 存储库。 使用以下命令安装 SQL Server 2019：
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   > ```

2. 运行以下命令以安装 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

3. 包安装完成后，运行 **mssql-conf setup**，按照提示设置 SA 密码并选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 以下 SQL Server 2017 版本是免费许可的：Evaluation、Developer 和 Express。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

4. 完成配置后，验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允许远程连接，请在 RHEL 的防火墙上打开 SQL Server 端口。 默认的 SQL Server 端口为 TCP 1433。 如果为防火墙使用的是 **FirewallD**，则可以使用以下命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此时，SQL Server 正在 RHEL 计算机上运行，随时可以使用！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安装 SQL Server

若要在 RHEL 上配置 SQL Server，请在终端中运行以下命令以安装 **mssql-server** 包：

1. 下载 Microsoft SQL Server 2019 预览版 Red Hat 存储库配置文件：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   ```

2. 运行以下命令以安装 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

3. 包安装完成后，运行 **mssql-conf setup**，按照提示设置 SA 密码并选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

4. 完成配置后，验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允许远程连接，请在 RHEL 的防火墙上打开 SQL Server 端口。 默认的 SQL Server 端口为 TCP 1433。 如果为防火墙使用的是 **FirewallD**，则可以使用以下命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此时，SQL Server 2019 预览版正在 RHEL 计算机上运行，随时可以使用！

::: moniker-end

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，需使用可在 SQL Server 上运行 Transact-SQL 语句的工具进行连接。 以下步骤将安装 SQL Server 命令行工具：[sqlcmd](../tools/sqlcmd-utility.md) 和 [bcp](../tools/bcp-utility.md)。

1. 下载 Microsoft Red Hat 存储库配置文件。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 如果安装了早期版本的 **mssql-tools**，请删除所有旧的 unixODBC 包。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 运行以下命令，以使用 unixODBC 开发人员包安装 **mssql-tools**。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 为方便起见，向 **PATH** 环境变量添加 `/opt/mssql-tools/bin/`。 这样就可以在不指定完整路径的情况下运行工具。 运行以下命令，以修改登录会话和交互式/非登录会话的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
