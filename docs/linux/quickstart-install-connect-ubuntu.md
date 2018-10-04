---
title: 在 Ubuntu 上的 SQL Server 入门 |Microsoft Docs
description: 本快速入门介绍如何在 Ubuntu 上安装 SQL Server 2017 或 SQL Server 2019 然后创建和查询使用 sqlcmd 数据库。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 2632b10aaf69701f93e51c1c945523300307789a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656685"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>快速入门： 安装 SQL Server 并在 Ubuntu 上创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入门，SQL Server 2017 或 SQL Server 2019 CTP 2.0 上安装 Ubuntu 16.04。 然后使用连接**sqlcmd**创建第一个数据库和运行查询。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入门，在 Ubuntu 16.04 上安装 SQL Server 2019 CTP 2.0。 然后使用连接**sqlcmd**创建第一个数据库和运行查询。

::: moniker-end

> [!TIP]
> 本教程需要用户输入和 Internet 连接。 如果您对[无人参与](sql-server-linux-setup.md#unattended)或[脱机](sql-server-linux-setup.md#offline)安装感兴趣，请参阅 [Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

您必须具有的 Ubuntu 16.04 计算机**至少 2 GB**的内存。

若要在自己的计算机上安装 Ubuntu，请转到[ http://www.ubuntu.com/download/server ](http://www.ubuntu.com/download/server)。 此外可以在 Azure 中创建 Ubuntu 虚拟机。 请参阅[创建和管理 Linux Vm 使用 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

> [!NOTE]
> 在此期间，[适用于 Linux 的 Windows 子系统](https://msdn.microsoft.com/commandline/wsl/about)作为安装目标不支持 Windows 10。

其他系统要求，请参阅[Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安装 SQL Server

若要在 Ubuntu 上配置 SQL Server ，在终端中运行以下命令安装**mssql server**包。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 注册 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > 如果你想要试用 SQL Server 2019，则必须改为注册**预览版 (2019)** 存储库。 对于 SQL Server 2019 安装中使用以下命令：
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   > ```

3. 运行以下命令，安装 SQL Server：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 程序包安装完成后，请运行 **mssql-conf setup** 命令并按提示设置 SA 密码，然后选择版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 自由授权以下 SQL Server 2017 版本： Evaluation、 Developer 和 Express。

   > [!NOTE]
   > 请确保为 SA 帐户指定强密码（最少 8 个字符，包括大写和小写字母、十进制数字和/或非字母数字符号）。

5. 配置完成后，请验证服务是否正在运行：

   ```bash
   systemctl status mssql-server
   ```

6. 如果你打算远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433）。

在此情况下，SQL Server 在 Ubuntu 计算机上运行并已准备好使用 ！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安装 SQL Server

若要在 Ubuntu 上配置 SQL Server ，在终端中运行以下命令安装**mssql server**包。

1. 导入公共存储库 GPG 密钥：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 注册 SQL Server 2019 预览版的 Microsoft SQL Server Ubuntu 存储库：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   ```

3. 运行以下命令，安装 SQL Server：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
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

6. 如果你打算远程连接，你可能还需要打开防火墙上的 SQL Server TCP 端口 （默认值为 1433）。

在此情况下，SQL Server 2019 CTP 2.0 在 Ubuntu 计算机上运行并已准备好使用 ！

::: moniker-end

## <a id="tools"></a>安装 SQL Server 命令行工具

若要创建数据库，需要使用一个能够在 SQL Server 上运行 Transact-SQL 语句的工具进行连接。 以下步骤安装 SQL Server 命令行工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

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
