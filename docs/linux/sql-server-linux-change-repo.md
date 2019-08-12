---
title: 配置适用于 SQL Server 2017 和 2019 的 Linux 存储库
description: 检查并配置适用于 Linux 中 SQL Server 2019 和 SQL Server 2017 的源存储库。 源存储库会影响在安装和升级期间应用的 SQL Server 版本。
author: VanMSFT
ms.author: vanto
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 33616b9a7767156e4cfd69d233f7dcfe5fc080f6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67967529"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>配置存储库以便安装和升级 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
本文介绍如何为 Linux 上的 SQL Server 2017 和 SQL Server 2019 的安装和升级配置正确的存储库。 在顶部，当前所选内容为“Red Hat (RHEL)”  。
::: zone-end

::: zone pivot="ld2-sles"
本文介绍如何为 Linux 上的 SQL Server 2017 和 SQL Server 2019 的安装和升级配置正确的存储库。 在顶部，当前所选内容为“SUSE (SLES)”  。
::: zone-end

::: zone pivot="ld2-ubuntu"
本文介绍如何为 Linux 上的 SQL Server 2017 和 SQL Server 2019 的安装和升级配置正确的存储库。 在顶部，当前所选内容为“Ubuntu”  。
::: zone-end

> [!TIP]
> SQL Server 2019 预览版现已推出！ 若要试用该预览版，请按照本文说明配置新的 mssql-server-preview 存储库  。 然后按照[安装指南](sql-server-linux-setup.md)中的说明进行安装。

## <a id="repositories"></a>存储库

在 Linux 上安装 SQL Server 时，须配置 Microsoft 存储库。 此存储库用于获取数据库引擎包、mssql-server 以及相关 SQL Server 包  。 现有三个主要存储库：

| 存储库 | “属性” | 描述 |
|---|---|---|
| **预览版 (2017)** | **mssql-server** | SQL Server 2017 CTP 和 RC 存储库（已停用）。 |
| **预览版 (2019)** | **mssql-server-preview** | SQL Server 2019 预览版和 RC 存储库。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累积更新 (CU) 存储库。 |
| **GDR** | **mssql-server-2017-gdr** | SQL Server 2017 GDR 存储库仅用于关键更新。 |

## <a id="cuversusgdr"></a> 累积更新与 GDR

务必注意，每个分发都有两种主要的存储库类型：

- **累积更新 (CU)** ：累积更新 (CU) 存储库包含基础 SQL Server 版本包，以及自该版本以来的所有 bug 修复程序或改进。 累积更新特定于发布的版本，例如 SQL Server 2017。 它们会定期发布。

- **GDR**：GDR 存储库包含基础 SQL Server 版本包，并且仅包含自该版本以来的关键修复程序和安全更新。 这些更新也会添加到下一个 CU 版本中。

每个 CU 和 GDR 版本都包含完整的 SQL Server 包以及该存储库此前的所有更新。 通过更改为 SQL Server 配置的存储库，可支持从 GDR 版本更新到 CU 版本。 也可以[降级](sql-server-linux-setup.md#rollback)到主要版本中的任何版本（例如：2017）。

> [!NOTE]
> 可以随时通过更改存储库从 GDR 版本更新到 CU 版本。 不支持从 CU 版本更新到 GDR 版本。

## <a name="configure-repositories"></a>配置存储库

::: zone pivot="ld2-rhel"
使用以下部分中的步骤来配置 Red Hat Enterprise Server (RHEL) 上的存储库。
::: zone-end

::: zone pivot="ld2-sles"
使用以下部分中的步骤来配置 SUSE Linux Enterprise Server (SLES) 上的存储库。
::: zone-end

::: zone pivot="ld2-ubuntu"
使用以下部分中的步骤来配置 Ubuntu 上的存储库。
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>检查先前配置的存储库

<!--RHEL-->
::: zone pivot="ld2-rhel"
首先，请验证是否已注册了 SQL Server 存储库。

1. 通过以下命令查看“/etc/yum.repos.d”目录中的文件  ：

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 查找配置 SQL Server 目录的文件，例如“mssql-server.repo”  。

3. 打印文件内容。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. “name”属性为配置的存储库  。 可以使用本文[存储库](#repositories)部分中的表确认该存储库。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
首先，请验证是否已注册了 SQL Server 存储库。

1. 使用“zypper info”获取之前配置的任何存储库的相关信息  。

   ```bash
   sudo zypper info mssql-server
   ```

2. “Repository”属性为配置的存储库  。 可以使用本文[存储库](#repositories)部分中的表确认该存储库。

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
首先，请验证是否已注册了 SQL Server 存储库。

1. 查看“/etc/apt/sources.list”文件的内容  。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 检查 mssql-server 的包 URL。 可以使用本文[存储库](#repositories)部分中的表确认该存储库。

::: zone-end

## <a name="remove-old-repository"></a>删除旧存储库

<!--RHEL-->
::: zone pivot="ld2-rhel"
如有必要，通过以下命令删除旧存储库。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假定上一部分中标识的文件名为“mssql-server”  。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
如有必要，删除旧的存储库。 基于之前配置的存储库类型，使用以下命令之一。

| 存储库 | 要删除的命令 |
|---|---|
| **预览版 (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **预览版 (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
如有必要，删除旧的存储库。 基于之前配置的存储库类型，使用以下命令之一。

| 存储库 | 要删除的命令 |
|---|---|
| **预览版 (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **预览版 (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>配置新的存储库

<!--RHEL-->
::: zone pivot="ld2-rhel"
配置要用于 SQL Server 安装和升级的新存储库。 使用以下命令之一配置所选存储库。

| 存储库 | 版本 | Command |
|---|---|---|
| **预览版 (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
配置要用于 SQL Server 安装和升级的新存储库。 使用以下命令之一配置所选存储库。

| 存储库 | 版本 | Command |
|---|---|---|
| **预览版 (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
配置要用于 SQL Server 安装和升级的新存储库。

1. 导入公共存储库 GPG 密钥。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用以下命令之一配置所选存储库。

   | 存储库 | 版本 | Command |
   |---|---|---|
   | **预览版 (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 运行“apt-get 更新”  。

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>后续步骤

配置了正确的存储库后，可继续通过新存储库[安装](sql-server-linux-setup.md#platforms)或[升级](sql-server-linux-setup.md#upgrade) SQL Server 以及任何相关包。

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> 此时，如果选择使用 [RHEL 快速入门](quickstart-install-connect-red-hat.md)，回想一下，现已配置目标存储库。 请勿在教程学习过程中重复该步骤。 尤其是在配置 GDR 存储库的情况下，因为快速入门会使用 CU 存储库。
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> 此时，如果选择使用 [SLES 快速入门](quickstart-install-connect-suse.md)，回想一下，现已配置目标存储库。 请勿在教程学习过程中重复该步骤。 尤其是在配置 GDR 存储库的情况下，因为快速入门会使用 CU 存储库。
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> 此时，如果选择使用 [Ubuntu 快速入门](quickstart-install-connect-ubuntu.md)，回想一下，现已配置目标存储库。 请勿在教程学习过程中重复该步骤。 尤其是在配置 GDR 存储库的情况下，因为快速入门会使用 CU 存储库。
::: zone-end

有关如何在 Linux 上安装 SQL Server 2017 的详细信息，请参阅 [Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)。
