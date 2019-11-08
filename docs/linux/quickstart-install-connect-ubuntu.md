---
title: Ubuntu 上的 SQL Server 入门
titleSuffix: SQL Server
description: 本快速入门介绍如何在 Ubuntu 上安装 SQL Server 2017 或 SQL Server 2019，然后使用 sqlcmd 创建和查询数据库。
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 17f73e7529fb8e74e9ff83de8d7e0ebd61783909
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531352"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>快速入门：安装 SQL Server 并在 Ubuntu 上创建数据库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

本快速入门介绍如何在 Ubuntu 16.04 上安装 SQL Server 2017 或 SQL Server 2019。 然后使用 sqlcmd 进行连接，创建第一个数据库并运行查询  。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

本快速入门介绍如何在 Ubuntu 16.04 上安装 SQL Server 2019。 然后使用 sqlcmd 进行连接，创建第一个数据库并运行查询  。

::: moniker-end

> [!TIP]
> 本教程需要用户输入和 internet 连接。 如果对无人参与或脱机安装过程感兴趣，请参阅 [Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必备条件

需配备 Ubuntu 16.04 计算机，且至少具有 2 GB 内存  。

要在自己的计算机上安装 Ubuntu 16.04，请转到[http://releases.ubuntu.com/xenial/](http://releases.ubuntu.com/xenial/)。 还可以在 Azure 中创建 Ubuntu 虚拟机。 请参阅[使用 Azure CLI 创建和管理 Linux VM](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

> [!NOTE]
> 目前，不支持将适用于 Windows 10 的 [Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)作为安装目标。

有关其他系统要求，请参阅 [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

> [!NOTE]
> Ubuntu 18.04 尚未获得正式支持，但可以通过[修改](https://blogs.msdn.microsoft.com/sql_server_team/installing-sql-server-2017-for-linux-on-ubuntu-18-04-lts/)运行 SQL Server。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安装 SQL Server

要在 Ubuntu 上配置 SQL Server，请在终端中运行以下命令以安装 mssql-server 包  。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 注册 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > 如果想安装 SQL Server 2019，必须改为注册 SQL Server 2019 存储库。 使用以下命令安装 SQL Server 2019：
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   > ```

3. 运行以下命令以安装 SQL Server：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 包安装完成后，运行 **mssql-conf setup**，按照提示设置 SA 密码并选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 以下 SQL Server 2017 版本是免费提供许可的：Evaluation、Developer 和 Express 版。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

5. 完成配置后，验证服务是否正在运行：

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 如果计划远程连接，可能还需要在防火墙上打开 SQL Server TCP 端口（默认值为 1433）。

此时，SQL Server 已在 Ubuntu 计算机上运行，随时可以使用！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安装 SQL Server

要在 Ubuntu 上配置 SQL Server，请在终端中运行以下命令以安装 mssql-server 包  。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 为 SQL Server 2019 注册 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```

3. 运行以下命令以安装 SQL Server：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 包安装完成后，运行 **mssql-conf setup**，按照提示设置 SA 密码并选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

5. 完成配置后，验证服务是否正在运行：

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 如果计划远程连接，可能还需要在防火墙上打开 SQL Server TCP 端口（默认值为 1433）。

此时，SQL Server 2019 已在 Ubuntu 计算机上运行，随时可以使用！

::: moniker-end

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，则需要使用可在 SQL Server 上运行 Transact-SQL 语句的工具进行连接。 以下步骤安装 SQL Server 命令行工具：[sqlcmd](../tools/sqlcmd-utility.md) 和 [bcp](../tools/bcp-utility.md)。

通过下列步骤在 Ubuntu 上安装 mssql-tools  。 

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
   > 若要将 mssql-tools 更新至最新版本，请运行以下命令  ：
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **可选**：向 bash shell 中的 PATH 环境变量添加 `/opt/mssql-tools/bin/`  。

   要使 sqlcmd/bcp 能从登陆会话的 bash shell 进行访问，请使用下列命令修改 ~/.bash_profile 文件中的 PATH    ：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   要使 sqlcmd/bcp 能从交互式/非登录会话的 bash shell 进行访问，请使用下列命令修改 ~/.bashrc 文件中的 PATH    ：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
