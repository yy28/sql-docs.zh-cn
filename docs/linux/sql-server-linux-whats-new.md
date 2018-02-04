---
title: "在 Linux 上的 SQL Server 自 2017 年 1 的新增功能 |Microsoft 文档"
description: "本主题重点介绍什么是用于在 Linux 上的 SQL Server 2017 的新功能。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.workload: On Demand
ms.openlocfilehash: 768d939d0014ca1818f8195627f57e0110d149fb
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Linux 版 SQL Server 2017 的新增功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍在 Linux 上运行的 SQL Server 2017 的主要功能和可用服务。

> [!NOTE]
> 除了这些功能在本文中，累积更新定期发布后 GA 版。 这些累积更新提供许多改进和修复。 有关最新 CU 版本的信息，请参阅[http://aka.ms/sql2017cu](http://aka.ms/sql2017cu)。 包下载和已知的问题，请参阅[发行说明](sql-server-linux-release-notes.md)。

## <a name="sql-server-database-engine"></a>SQL Server 数据库引擎

- 启用核心 SQL Server 数据库引擎功能。
- 对本机 Linux 路径的支持。
- IPV6 支持。
- 对 NFS 上数据库文件的支持。
- 启用[透明的层安全性](sql-server-linux-encrypted-connections.md)(TLS) 加密。
- 启用[Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。
- [可用性组功能](sql-server-linux-availability-group-overview.md)以实现高可用性。
- [全文搜索](sql-server-linux-setup-full-text-search.md)支持。

## <a name="sql-server-agent"></a>SQL Server 代理

- 启用[SQL Server 代理](sql-server-linux-setup-sql-agent.md)支持以下任务：
  - [TRANSACT-SQL 的作业](sql-server-linux-run-sql-server-agent-job.md)
  - [数据库邮件](sql-server-linux-db-mail-sql-agent.md)
  - [日志传送](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- 能够在 Linux 上运行 SSIS 包。 有关详细信息，请参阅[配置与 ssis conf Linux 上 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="other-improvements"></a>其他改进

- 命令行配置工具[mssql conf](sql-server-linux-configure-mssql-conf.md)。
- 使用无人参与的安装支持[环境变量](sql-server-linux-configure-environment-variables.md)。
- 跨平台[Visual Studio Code mssql server 扩展](sql-server-linux-develop-use-vscode.md)。
- 跨平台脚本生成器[mssql 脚本编写器](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- 跨平台动态管理视图 (DMV) 监视器[DBFS 工具](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>后续步骤

若要在 Linux 上安装 SQL Server，请使用以下教程之一：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

有关 SQL Server 在 Linux 上其他信息，请参阅[概述](sql-server-linux-overview.md)。 包下载和不支持的功能和已知的问题的列表，请参阅[发行说明](sql-server-linux-release-notes.md)。

若要查看在 SQL Server 2017 中引入的其他改进，请参阅[What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
