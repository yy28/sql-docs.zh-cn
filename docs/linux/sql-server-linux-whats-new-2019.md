---
title: Linux 上的 SQL Server 2019 的新增功能
description: 本文重点介绍 Linux 上的 SQL Server 2019 的新增功能。
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5183efa51afd89ad82d0cdcb6448996429b81d28
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "72890557"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>Linux 上的 SQL Server 2019 的新增功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍了可用于在 Linux 上运行的 SQL Server 2019 的主要功能和服务。 有关包下载和已知问题，请参阅[发行说明](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15)。

## <a name="updates"></a>更新

已在 Linux 上的 SQL Server 2019 中进行了更新：

| 新增功能或更新 | 详细信息 |
|:-----|:-----|
|复制支持 |[Linux 上的 SQL Server 复制](sql-server-linux-replication.md)
|支持 Microsoft 分布式事务处理协调器 (MSDTC) |[如何在 Linux 上配置 MSDTC](sql-server-linux-configure-msdtc.md) |
|OpenLDAP 支持第三方 AD 提供商 |[教程：对 Linux 上的 SQL Server 使用 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md) |
|Linux 上的机器学习 |[在 Linux 上配置机器学习](sql-server-linux-setup-machine-learning.md) |
|`tempdb` 改进： | 默认情况下，Linux 上的 SQL Server 新安装会根据逻辑内核数创建多个 `tempdb` 数据文件（最多 8 个数据文件）。 这不适用于就地次要版本或主版本升级。 每个 `tempdb` 文件的大小为 8MB，且自动增长大小为 64MB。 此行为类似于 Windows 上的默认 SQL Server 安装。 |
| Linux 上的 PolyBase | 在 Linux 上为非 Hadoop 连接器[安装 PolyBase](../relational-databases/polybase/polybase-linux-setup.md)。<br/><br/>[PolyBase 类型映射](../relational-databases/polybase/polybase-type-mapping.md)。 |
| 变更数据捕获 (CDC) 支持 | Linux 上的 SQL Server 2019 现在支持变更数据捕获 (CDC)。 |
| Microsoft 容器注册表 | [Microsoft 容器注册表](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/)现在将 Docker Hub 替换为新的官方 Microsoft 容器映像，其中包括 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。 |
| 非根容器 | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了通过在默认情况下以非根用户身份启动 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 进程来创建更安全容器的功能。 有关更多详细信息，请参阅[以非根用户的身份构建并运行 SQL Server 容器](sql-server-linux-configure-docker.md#buildnonrootcontainer)。 |

## <a name="next-steps"></a>后续步骤

要在 Linux 上安装 SQL Server，请使用以下教程之一：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [在 Docker 上运行](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

有关常见问题的解答，请参阅 [Linux 上的 SQL Server 常见问题解答](sql-server-linux-faq.md)。 要查看 SQL Server 2019 中引入的其他改进，请参阅 [SQL Server 2019 的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
