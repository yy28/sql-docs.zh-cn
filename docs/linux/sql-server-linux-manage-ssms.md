---
title: 使用 SSMS 管理 SQL Server on Linux |Microsoft 文档
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: 5de8495d6fc633f769feb5dfbc534dd60050615f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Windows 上使用 SQL Server Management Studio 管理 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)并指导您完成几个常见任务。 SSMS 是一个 Windows 应用程序，因此请在 Windows 计算机可连接到 Linux 上的远程 SQL Server 实例时使用 SSMS。

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)是 Microsoft 提供的免费的开发和管理需求的 SQL 工具套件的一部分。 SSMS 是一个集成环境，用于访问、配置、管理和开发 SQL Server（在本地或云中、Linux、Windows 或 macOS Docker 以及在 Azure SQL 数据库和 Azure SQL 数据仓库上运行）的所有组件。 SSMS 将大量图形工具与丰富的脚本编辑器相结合，各种技术水平的开发人员和管理员都能访问 SQL Server。

SSMS 提供适用于 SQL Server 的大量开发和管理功能，包括执行以下任务的工具：

- 配置、 监视和管理一个或多个 SQL Server 实例
- 部署、 监视和升级数据层组件，如数据库和数据仓库
- 备份和还原数据库
- 生成并执行 T-SQL 查询和脚本，请参阅结果
- 生成数据库对象的 T-SQL 脚本
- 查看和编辑数据库中的数据
- 以可视方式设计 T-SQL 查询和数据库对象，如视图、 表和存储的过程

请参阅[使用 SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)有关详细信息。

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>安装最新版本的 SQL Server Management Studio (SSMS)

使用 SQL Server 时，应始终使用最新版本的 SQL Server Management Studio (SSMS)。 最新版本的 SSMS 不断更新和优化并且当前适用于 SQL Server 2017 on Linux。 若要下载并安装最新版本，请参阅[下载 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为保持使用最新版本，有可供下载的新版本时，最新版本的 SSMS 会发出提示。 

## <a name="before-you-begin"></a>開始之前
- 请参阅[使用 SSMS 连接到 Linux 上的 SQL Server 的 Windows 上](sql-server-linux-develop-use-ssms.md)有关如何连接和查询使用 SSMS
- 读取[已知问题](sql-server-linux-release-notes.md)在 Linux 上的 SQL server 自 2017 年 1

## <a name="create-and-manage-databases"></a>创建和管理数据库
在连接到时*master*数据库，您可以在服务器上创建数据库和修改或删除现有数据库。 以下步骤介绍如何通过 Management Studio 完成几项常见的数据库管理任务。 若要执行这些任务，请确保你连接到*master*你设置在 Linux 上的 SQL Server 2017 时创建的服务器级别主体登录名的数据库。

### <a name="create-a-new-database"></a>新建数据库

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 2017 中的服务器

2. 在对象资源管理器，右键单击*数据库*文件夹，，然后单击 * 新建数据库..."

3. 在*新数据库*对话框中，输入新数据库的名称，然后单击*确定*

已成功在服务器中创建新数据库。 如果你希望在创建新的数据库使用 T-SQL 的那么请参阅[CREATE DATABASE (SQL Server TRANSACT-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)。

### <a name="drop-a-database"></a>删除数据库

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 2017 中的服务器

2. 在对象资源管理器，展开*数据库*文件夹以查看服务器上的所有数据库的列表。

3. 在对象资源管理器，右键单击你想要删除的数据库，然后单击*删除*

4. 在*删除对象*对话框中，选中*关闭现有连接*，然后单击*确定*

已成功从服务器中删除数据库。 如果你希望删除使用 T-SQL 的数据库，那么请参阅[DROP DATABASE (SQL Server TRANSACT-SQL)](../t-sql/statements/drop-database-transact-sql.md)。

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>使用活动监视器查看有关 SQL Server 活动的信息

[活动监视器](../relational-databases/performance-monitor/activity-monitor.md)工具是内置到 SQL Server Management Studio (SSMS)，并显示有关 SQL Server 过程和了解这些进程如何影响当前的 SQL Server 实例的信息。

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 2017 中的服务器

2. 在对象资源管理器，右键单击*服务器*节点，，然后单击*活动监视器*

活动监视器显示可展开和可折叠的窗格，提供以下相关信息：
- 概述
- 进程
- 资源等待
- 数据文件 I/O
- 最近耗费大量资源的查询
- 耗费大量资源的活动查询

展开某个窗格时，活动监视器会查询实例获取相关信息。 折叠窗格时，该窗格的所有查询活动都将停止。 可以同时展开一个或多个窗格，查看实例上不同种类的活动。

## <a name="see-also"></a>另请参阅
- [使用 SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)
- [导出和导入具有 SSMS 的数据库](sql-server-linux-migrate-ssms.md)
- [教程：SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/bb934498.aspx)
- [教程：编写 Transact-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)
- [服务器性能和活动监视](../relational-databases/performance/server-performance-and-activity-monitoring.md)
