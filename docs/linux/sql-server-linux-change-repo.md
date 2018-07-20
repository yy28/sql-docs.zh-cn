---
title: Linux 上的 SQL Server 配置存储库 |Microsoft Docs
description: 检查并配置 SQL Server 2017 Linux 上的源代码存储库。 源存储库会影响应用在安装和升级过程的 SQL Server 的版本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 361f66fff8fecfd748b1bd573367509e93cc7b87
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086979"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>配置安装和升级 Linux 上的 SQL Server 存储库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置 SQL Server 2017 安装和升级的正确存储库。

> [!IMPORTANT]
> 如果您以前安装的 CTP 或 SQL Server 2017 的 RC 版本，你必须使用本文中的步骤注册正式版 (GA) 存储库和升级或重新安装。 SQL Server 2017 的预览版本不受支持，并将过期。

## <a id="repositories"></a>存储库

在 Linux 上安装 SQL Server，必须配置 Microsoft 存储库。 使用此存储库获取数据库引擎包， **mssql server**，和相关的 SQL Server 包。 目前有三个主要的存储库：

| 存储库 | “属性” | Description |
|---|---|---|
| **预览** | **mssql-server** | 预览存储库的 SQL Server ctp 版本和 RC 版本。 SQL Server 2017 不支持此存储库。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累积更新 (CU) 存储库。 |
| **GDR** | **mssql-server-2017-gdr** | SQL Server 2017 GDR 仅关键更新的存储库。 |

## <a id="cuversusgdr"></a> 与 GDR 累积更新

请务必注意，有两种主要类型的每个分布区的存储库：

- **累积更新 (CU)**： 自发行以来的累积更新 (CU) 存储库包含为基的 SQL Server 版本和任何 bug 修复或改进的包。 特定于一个发行版本，如 SQL Server 2017 累积更新。 正则频率发布它们。

- **GDR**: GDR 存储库包含自发行以来的基本 SQL Server 版本和仅关键的修复程序和安全更新的包。 这些更新也会添加到下一步的 CU 版本。

每个 CU 和 GDR 版本包含完整的 SQL Server 包和所有此前更新为该存储库。 通过更改 SQL Server 配置的存储库支持从 GDR 版本更新到 CU 版本。 此外可以[降级](sql-server-linux-setup.md#rollback)到主要版本中的任何版本 (例如： 2017年)。

> [!NOTE]
> 可以从 GDR 版本更新到 CU 发布在任何时候通过更改存储库。 正在更新从 CU GDR 发行的版本不支持。 

## <a id="configure"></a> 配置存储库

以下部分介绍如何验证并配置以下受支持的平台的存储库：

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> 配置 RHEL 存储库
使用以下步骤配置 Red Hat Enterprise Server (RHEL) 上的存储库。

### <a name="check-for-previously-configured-repositories-rhel"></a>对于以前配置的存储库 (RHEL) 检查
首先，验证是否已注册的 SQL Server 存储库。

1. 查看中的文件 **/etc/yum.repos.d**目录使用以下命令：

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 查找文件，用于配置 SQL Server 目录中，如**mssql server.repo**。

3. 输出文件的内容。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **名称**属性是配置存储库。 您可以使用的表中识别它[存储库](#repositories)本文的部分。

### <a name="remove-old-repository-rhel"></a>删除旧存储库 (RHEL)
如有必要，删除旧的存储库使用以下命令。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假定名为上一节中标识的文件**mssql server.repo**。

### <a name="configure-new-repository-rhel"></a>配置新的存储库 (RHEL)
配置新的存储库，用于 SQL Server 安装和升级。 使用以下命令之一配置所选存储库。

| 存储库 | Command |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> 配置 SLES 存储库
使用以下步骤在 SLES 上配置存储库。

### <a name="check-for-previously-configured-repositories-sles"></a>对于以前配置的存储库 (SLES) 检查
首先，验证是否已注册的 SQL Server 存储库。

1. 使用**zypper 信息**以获取有关任何以前配置的存储库的信息。

   ```bash
   sudo zypper info mssql-server
   ```

2. **存储库**属性是配置存储库。 您可以使用的表中识别它[存储库](#repositories)本文的部分。

### <a name="remove-old-repository-sles"></a>删除旧存储库 (SLES)
如有必要，删除旧的存储库。 使用以下命令基于以前配置的存储库的类型之一。

| 存储库 | 若要删除的命令 |
|---|---|
| **预览** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>配置新的存储库 (SLES)
配置新的存储库，用于 SQL Server 安装和升级。 使用以下命令之一配置所选存储库。

| 存储库 | Command |
|---|---|
| **CU** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> 配置 Ubuntu 存储库
使用以下步骤在 Ubuntu 上配置存储库。

### <a name="check-for-previously-configured-repositories-ubuntu"></a>对于以前配置的存储库 (Ubuntu) 检查
首先，验证是否已注册的 SQL Server 存储库。

1. 查看的内容 **/etc/apt/sources.list**文件。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 检查 mssql server 包 URL。 您可以使用的表中识别它[存储库](#repositories)本文的部分。

### <a name="remove-old-repository-ubuntu"></a>删除旧存储库 (Ubuntu)
如有必要，删除旧的存储库。 使用以下命令基于以前配置的存储库的类型之一。

| 存储库 | 若要删除的命令 |
|---|---|
| **预览** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>配置新的存储库 (Ubuntu)
配置新的存储库，用于 SQL Server 安装和升级。

1. 导入公共存储库 GPG 密钥。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用以下命令之一配置所选存储库。

   | 存储库 | Command |
   |---|---|
   | **CU** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 运行**apt get 更新**。

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>后续步骤

配置正确的存储库后，便可以前往[安装](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade)SQL Server 和任何相关包从新的存储库。

> [!IMPORTANT]
> 此时，如果选择使用其中一个安装项目，如[快速入门](sql-server-linux-setup.md#platforms)，请记住已配置的目标存储库。 在这些教程中不重复该步骤。 这是配置 GDR 存储库，尤其如此，因为快速入门使用 CU 存储库。

有关如何在 Linux 上安装 SQL Server 2017 的详细信息，请参阅[Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。
