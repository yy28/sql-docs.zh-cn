---
title: 为 SQL Server 2017 和 2019年配置 Linux 存储库
description: 检查并配置适用于 SQL Server 2019 和 Linux 上的 SQL Server 2017 源代码存储库。 源存储库会影响应用在安装和升级过程的 SQL Server 的版本。
author: VanMSFT
ms.author: vanto
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 33616b9a7767156e4cfd69d233f7dcfe5fc080f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967529"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>配置安装和升级 Linux 上的 SQL Server 存储库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
本文介绍如何在 Linux 上配置 SQL Server 2017 和 SQL Server 2019 安装和升级的正确存储库。 在顶部，你当前所选内容是**Red Hat (RHEL)** 。
::: zone-end

::: zone pivot="ld2-sles"
本文介绍如何在 Linux 上配置 SQL Server 2017 和 SQL Server 2019 安装和升级的正确存储库。 在顶部，你当前所选内容是**SUSE (SLES)** 。
::: zone-end

::: zone pivot="ld2-ubuntu"
本文介绍如何在 Linux 上配置 SQL Server 2017 和 SQL Server 2019 安装和升级的正确存储库。 在顶部，你当前所选内容是**Ubuntu**。
::: zone-end

> [!TIP]
> SQL Server 2019 预览版现已推出 ！ 若要试用，使用本文配置的新**mssql server 预览版**存储库。 然后使用中的说明进行安装[安装指南](sql-server-linux-setup.md)。

## <a id="repositories"></a>存储库

在 Linux 上安装 SQL Server，必须配置 Microsoft 存储库。 使用此存储库获取数据库引擎包， **mssql server**，和相关的 SQL Server 包。 目前有三个主要的存储库：

| 存储库 | 名称 | 描述 |
|---|---|---|
| **预览版 (2017)** | **mssql-server** | SQL Server 2017 ctp 版本和 RC 的存储库 （停用）。 |
| **预览版 (2019)** | **mssql-server-preview** | SQL Server 2019 预览和 RC 存储库。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累积更新 (CU) 存储库。 |
| **GDR** | **mssql-server-2017-gdr** | SQL Server 2017 GDR 仅关键更新的存储库。 |

## <a id="cuversusgdr"></a> 与 GDR 累积更新

请务必注意，有两种主要类型的每个分布区的存储库：

- **累积更新 (CU)** :累积更新 (CU) 存储库包含自发行以来为基的 SQL Server 版本和任何 bug 修复或改进的包。 特定于一个发行版本，如 SQL Server 2017 累积更新。 正则频率发布它们。

- **GDR**:GDR 存储库包含自发行以来的基本 SQL Server 版本和仅关键的修复程序和安全更新的包。 这些更新也会添加到下一步的 CU 版本。

每个 CU 和 GDR 版本包含完整的 SQL Server 包和所有此前更新为该存储库。 通过更改 SQL Server 配置的存储库支持从 GDR 版本更新到 CU 版本。 此外可以[降级](sql-server-linux-setup.md#rollback)到主要版本中的任何版本 (例如：2017)。

> [!NOTE]
> 可以从 GDR 版本更新到 CU 发布在任何时候通过更改存储库。 正在更新从 CU GDR 发行的版本不支持。

## <a name="configure-repositories"></a>配置存储库

::: zone pivot="ld2-rhel"
使用以下各节中的步骤配置 Red Hat Enterprise Server (RHEL) 上的存储库。
::: zone-end

::: zone pivot="ld2-sles"
使用以下各节中的步骤配置 SUSE Linux Enterprise Server (SLES) 上的存储库。
::: zone-end

::: zone pivot="ld2-ubuntu"
使用以下各节中的步骤在 Ubuntu 上配置存储库。
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>检查以前配置的存储库

<!--RHEL-->
::: zone pivot="ld2-rhel"
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

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
首先，验证是否已注册的 SQL Server 存储库。

1. 使用**zypper 信息**以获取有关任何以前配置的存储库的信息。

   ```bash
   sudo zypper info mssql-server
   ```

2. **存储库**属性是配置存储库。 您可以使用的表中识别它[存储库](#repositories)本文的部分。

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
首先，验证是否已注册的 SQL Server 存储库。

1. 查看的内容 **/etc/apt/sources.list**文件。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 检查 mssql server 包 URL。 您可以使用的表中识别它[存储库](#repositories)本文的部分。

::: zone-end

## <a name="remove-old-repository"></a>删除旧的存储库

<!--RHEL-->
::: zone pivot="ld2-rhel"
如有必要，删除旧的存储库使用以下命令。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假定名为上一节中标识的文件**mssql server.repo**。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
如有必要，删除旧的存储库。 使用以下命令基于以前配置的存储库的类型之一。

| 存储库 | 若要删除的命令 |
|---|---|
| **预览版 (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **预览版 (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
如有必要，删除旧的存储库。 使用以下命令基于以前配置的存储库的类型之一。

| 存储库 | 若要删除的命令 |
|---|---|
| **预览版 (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **预览版 (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>配置新的存储库

<!--RHEL-->
::: zone pivot="ld2-rhel"
配置新的存储库，用于 SQL Server 安装和升级。 使用以下命令之一配置所选存储库。

| 存储库 | Version | Command |
|---|---|---|
| **预览版 (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
配置新的存储库，用于 SQL Server 安装和升级。 使用以下命令之一配置所选存储库。

| 存储库 | Version | Command |
|---|---|---|
| **预览版 (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
配置新的存储库，用于 SQL Server 安装和升级。

1. 导入公共存储库 GPG 密钥。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用以下命令之一配置所选存储库。

   | 存储库 | Version | Command |
   |---|---|---|
   | **预览版 (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 运行**apt get 更新**。

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>后续步骤

配置正确的存储库后，便可以前往[安装](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade)SQL Server 和任何相关包从新的存储库。

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> 此时，如果您选择使用[RHEL 快速入门](quickstart-install-connect-red-hat.md)，请记住已配置的目标存储库。 在这些教程中不重复该步骤。 这是配置 GDR 存储库，尤其如此，因为快速开始使用 CU 存储库。
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> 此时，如果您选择使用[SLES 快速入门](quickstart-install-connect-suse.md)，请记住已配置的目标存储库。 在这些教程中不重复该步骤。 这是配置 GDR 存储库，尤其如此，因为快速开始使用 CU 存储库。
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> 此时，如果您选择使用[Ubuntu 快速入门](quickstart-install-connect-ubuntu.md)，请记住已配置的目标存储库。 在这些教程中不重复该步骤。 这是配置 GDR 存储库，尤其如此，因为快速开始使用 CU 存储库。
::: zone-end

有关如何在 Linux 上安装 SQL Server 2017 的详细信息，请参阅[Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md)。
