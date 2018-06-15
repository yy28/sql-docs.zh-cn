---
title: 为在 Linux 上的 SQL Server 配置存储库 |Microsoft 文档
description: 检查并为在 Linux 上的 SQL Server 2017 配置源存储库。 源存储库会影响在安装和升级过程中应用的 SQL Server 的版本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 63cb2f56852a668bc48aa85cd31a72a2b583463b
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323368"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>配置存储库安装和升级在 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置 SQL Server 2017 安装和升级的正确存储库。

> [!IMPORTANT]
> 如果你以前安装的 CTP 或 RC 版本的 SQL Server 自 2017 年，你必须使用本文中的步骤注册正式版 (GA) 存储库和升级或重新安装。 SQL Server 自 2017 年的预览版本不支持，并将使其过期。

## <a id="repositories"></a>存储库

当在 Linux 上安装 SQL Server 时，你必须配置 Microsoft 存储库。 使用此存储库来获取数据库引擎程序包， **mssql server**，以及相关的 SQL Server 包。 目前，有三个主要的存储库：

| 存储库 | 名称 | Description |
|---|---|---|
| **预览** | **mssql-server** | CTP 和 RC 版本的 SQL Server 的预览存储库。 SQL Server 2017 不支持此存储库。 |
| **CU** | **mssql-server-2017** | 服务器 2017年累积 SQL 更新 (CU) 存储库。 |
| **GDR** | **mssql-server-2017-gdr** | 仅适用于关键更新的 SQL Server 自 2017 年 GDR 存储库。 |

## <a id="cuversusgdr"></a> 与 GDR 的累积更新

请务必请注意，有两种主要类型的每个分布的存储库：

- **累积更新 (CU)**: 累积更新 (CU) 存储库包含自该版本为基的 SQL Server 版本和任何 bug 修复或改进的包。 累积更新是特定于发行版中，如 SQL Server 自 2017 年。 正则的频率发布它们。

- **GDR**: GDR 储存库自该版本中包含的基本 SQL Server 版本和仅关键的修复程序和安全更新的包。 这些更新也会添加到下一步 CU 发行版。

每个 CU 和 GDR 版本包含完整的 SQL Server 程序包和所有以前的更新，该存储库。 从 GDR 版本更新到 CU 版本受更改 SQL Server 配置的存储库。 你还可以[降级](sql-server-linux-setup.md#rollback)到在主要版本中的任何版本 (ex： 自 2017 年)。

> [!NOTE]
> 你可以从 GDR 版本更新到 CU 释放任何时候通过更改存储库。 更新从 CU 的 GDR 发行版的版本不支持。 

## <a id="configure"></a> 配置存储库

下列各节描述如何验证和配置以下支持的平台的存储库：

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> 配置 RHEL 存储库
使用以下步骤配置 Red Hat Enterprise Server (RHEL) 上的存储库。

### <a name="check-for-previously-configured-repositories-rhel"></a>检查有以前配置的存储库 (RHEL)
首先，验证是否已注册的 SQL Server 存储库。

1. 查看中的文件 **/etc/yum.repos.d**目录使用以下命令：

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 查找配置 SQL Server 目录中，如文件**mssql server.repo**。

3. 输出文件的内容。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **名称**属性是配置的存储库。 您可以使用的表中识别它[存储库](#repositories)部分中的所述。

### <a name="remove-old-repository-rhel"></a>删除旧的存储库 (RHEL)
如有必要，删除旧的存储库使用以下命令。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假定名为上一节中标识的文件**mssql server.repo**。

### <a name="configure-new-repository-rhel"></a>配置新的存储库 (RHEL)
配置新的存储库，以用于 SQL Server 安装和升级。 请使用以下命令可配置的所选的存储库。

| 存储库 | Command |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> 配置 SLES 存储库
使用以下步骤在 SLES 上配置存储库。

### <a name="check-for-previously-configured-repositories-sles"></a>检查有以前配置的存储库 (SLES)
首先，验证是否已注册的 SQL Server 存储库。

1. 使用**zypper 信息**以获取有关任何以前配置的存储库的信息。

   ```bash
   sudo zypper info mssql-server
   ```

2. **存储库**属性是配置的存储库。 您可以使用的表中识别它[存储库](#repositories)部分中的所述。

### <a name="remove-old-repository-sles"></a>删除旧的存储库 (SLES)
如有必要，删除旧的存储库。 使用以下命令基于以前配置的存储库的类型之一。

| 存储库 | 若要删除的命令 |
|---|---|
| **预览** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>配置新的存储库 (SLES)
配置新的存储库，以用于 SQL Server 安装和升级。 请使用以下命令可配置的所选的存储库。

| 存储库 | Command |
|---|---|
| **CU** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> 配置 Ubuntu 存储库
使用以下步骤在 Ubuntu 上配置存储库。

### <a name="check-for-previously-configured-repositories-ubuntu"></a>检查有以前配置的存储库 (Ubuntu)
首先，验证是否已注册的 SQL Server 存储库。

1. 查看的内容 **/etc/apt/sources.list**文件。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 检查 mssql 服务器的程序包 URL。 您可以使用的表中识别它[存储库](#repositories)部分中的所述。

### <a name="remove-old-repository-ubuntu"></a>删除旧的存储库 (Ubuntu)
如有必要，删除旧的存储库。 使用以下命令基于以前配置的存储库的类型之一。

| 存储库 | 若要删除的命令 |
|---|---|
| **预览** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>配置新的存储库 (Ubuntu)
配置新的存储库，以用于 SQL Server 安装和升级。

1. 导入公共存储库 GPG 密钥。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 请使用以下命令可配置的所选的存储库。

   | 存储库 | Command |
   |---|---|
   | **CU** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 运行**apt get 更新**。

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>后续步骤

配置正确的存储库后，你可以继续[安装](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade)SQL Server 和任何相关包从新的存储库。

> [!IMPORTANT]
> 此时，如果你选择使用的某个安装项目中，如[快速入门](sql-server-linux-setup.md#platforms)，请记住，你已配置的目标存储库。 不在本教程中重复该步骤。 这是如果你配置 GDR 存储库，尤其如此，因为快速入门使用 CU 存储库。

有关如何在 Linux 上安装 SQL Server 自 2017 年的详细信息，请参阅[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)。
