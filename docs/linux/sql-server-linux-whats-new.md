---
title: 什么是 Linux 上的 SQL Server 2017 的新增功能 |Microsoft 文档
description: 本文重点介绍什么是 Linux 上的 SQL Server 2017 的新增功能。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: 266982731cc98121e6456d10fb93c7ccffaa4b22
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719343"
---
# <a name="whats-new-for-sql-server-on-linux"></a>什么是 Linux 上的 SQL Server 的新增功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍了在 Linux 上运行的 SQL Server 2017 的主要功能和可用的服务。

SQL Server 2019 预览版已发布。 本文不涉及 SQL Server 2019 预览版本。 若要了解有关 SQL Server 2019 预览，请参阅[什么是适用于 Linux 的 SQL Server 2019 preview 中的新增](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。

> [!NOTE]
> 除了本文中的这些功能外, 在 GA 发布之后, 还会定期发布累积更新。 这些累积更新提供许多改进和修复。 有关最新 CU 版本的信息，请参阅[ https://aka.ms/sql2017cu ](https://aka.ms/sql2017cu)。 有关包下载和已知的问题，请参阅[发行说明](sql-server-linux-release-notes.md)。

## <a name="sql-server-database-engine"></a>SQL Server 数据库引擎

- 启用核心 SQL Server 数据库引擎功能。
- 对本机 Linux 路径支持。
- IPV6 支持。
- 在 NFS 上数据库文件的支持。
- 已启用[传输层安全性](sql-server-linux-encrypted-connections.md)(TLS) 加密。
- 已启用[Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。
- [可用性组功能](sql-server-linux-availability-group-overview.md)以实现高可用性。
- [全文搜索](sql-server-linux-setup-full-text-search.md)支持。

## <a name="sql-server-agent"></a>SQL Server 代理

- 已启用[SQL Server 代理](sql-server-linux-setup-sql-agent.md)支持以下任务：
  - [Transact SQL 作业](sql-server-linux-run-sql-server-agent-job.md)
  - [数据库邮件](sql-server-linux-db-mail-sql-agent.md)
  - [日志传送](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- 若要在 Linux 上运行 SSIS 包的功能。 有关详细信息，请参阅[配置使用 ssis conf Linux 上 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="other-improvements"></a>其他改进

- 命令行配置工具[mssql conf](sql-server-linux-configure-mssql-conf.md)。
- 使用无人参与的安装支持[环境变量](sql-server-linux-configure-environment-variables.md)。
- 跨平台[Visual Studio Code 的 mssql server 扩展](sql-server-linux-develop-use-vscode.md)。
- 跨平台脚本生成器[mssql 脚本专家](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- 跨平台动态管理视图 (DMV) 监视[DBFS 工具](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>后续步骤

若要在 Linux 上安装 SQL Server，请使用以下教程之一：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

若要查看 SQL Server 2017 中引入了其他改进，请参阅[What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)。

> [!TIP]
> 有关常见问题的解答，请参阅[SQL Server Linux 常见问题](sql-server-linux-faq.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
