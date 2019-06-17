---
title: 使用 SSMS 管理 Linux 上的 SQL Server |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.openlocfilehash: 38f0f3a03e6de4cec622ffe03f9dbdc47a7ccb73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713153"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>在 Windows 上使用 SQL Server Management Studio 来管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍了[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)并指导你完成几个常见任务。 SSMS 是一个 Windows 应用程序，因此请在 Windows 计算机可连接到 Linux 上的远程 SQL Server 实例时使用 SSMS。

> [!TIP]
> 如果您没有 Windows 计算机上运行 SSMS，请考虑新[Azure Data Studio](../azure-data-studio/index.md)。 它用于管理 SQL Server 提供一种图形工具，并在 Linux 和 Windows 上运行。

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)是 Microsoft 免费提供为开发和管理需求的 SQL 工具套件的一部分。 SSMS 是一个集成的环境，若要访问、 配置、 管理、 管理和开发 SQL Server 的所有组件。 它可以连接到任何平台上运行这两个在本地，在 Docker 容器中和云中的 SQL Server。 它还连接到 Azure SQL 数据库和 Azure SQL 数据仓库。 SSMS 将大量图形工具与丰富的脚本编辑器相结合，各种技术水平的开发人员和管理员都能访问 SQL Server。

SSMS 提供适用于 SQL Server 的大量开发和管理功能，包括执行以下任务的工具：

- 配置、 监视和管理单个或多个 SQL Server 实例
- 部署、 监视和升级数据层组件，如数据库和数据仓库
- 备份和还原数据库
- 生成和执行 T-SQL 查询和脚本，并查看结果
- 生成数据库对象的 T-SQL 脚本
- 查看和编辑数据库中的数据
- 以可视方式设计 T-SQL 查询和数据库对象，如视图、 表和存储的过程

请参阅[什么是 SSMS？](../ssms/sql-server-management-studio-ssms.md)有关 SSMS 的详细信息。

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>安装最新版本的 SQL Server Management Studio (SSMS)

使用 SQL Server 时，应始终使用最新版本的 SQL Server Management Studio (SSMS)。 最新版本的 SSMS 不断更新并进行优化，目前适用于 Linux 上的 SQL Server。 若要下载并安装最新版本，请参阅[下载 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为保持使用最新版本，有可供下载的新版本时，最新版本的 SSMS 会发出提示。

> [!NOTE]
> 使用 SSMS 管理 Linux 之前, 查看[已知问题](sql-server-linux-release-notes.md)Linux 上的 ssms。

## <a name="connect-to-sql-server-on-linux"></a>连接到 Linux 上的 SQL Server

使用以下基本步骤进行连接：

1. 通过键入启动 SSMS **Microsoft SQL Server Management Studio**在 Windows 搜索框中，并单击桌面应用。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. 在中**连接到服务器**窗口中，输入以下信息 (如果已在运行 SSMS，请单击**连接 > 数据库引擎**以打开**连接到服务器**窗口）：

   | 设置 | Description |
   |-----|-----|
   | **服务器类型** | 默认为数据库引擎；请勿更改此值。 |
   | **服务器名称** | 输入目标 Linux SQL Server 计算机的名称或它的 IP 地址。 |
   | **身份验证** | 对于 Linux 上的 SQL Server，使用**SQL Server 身份验证**。 |
   | **登录** | 输入数据库服务器上具有访问权限的用户的名称 (例如，默认值**SA**安装过程中创建的帐户)。 |
   | **密码** | 指定的用户输入的密码 (对于**SA**帐户，则此安装过程中创建)。 |

    ![SQL Server Management Studio:连接到 SQL 数据库服务器](./media/sql-server-linux-manage-ssms/connect.png)

1. 单击 **“连接”** 。

    > [!TIP]
    > 如果连接失败，请首先尝试根据错误消息诊断问题。 然后查看[连接故障排除建议](sql-server-linux-troubleshooting-guide.md#connection)。
 
1. 已成功连接到 SQL Server 以后,**对象资源管理器**，你现在可以访问你的数据库来执行管理任务或查询数据。

## <a name="run-transact-sql-queries"></a>运行 TRANSACT-SQL 查询

连接到服务器后，可以连接到数据库并运行 Transact SQL 查询。 Transact SQL 查询可用于几乎所有数据库的任务。

1. 在中**对象资源管理器**，导航到在服务器上的目标数据库。 例如，展开**系统数据库**以使用**master**数据库。

1. 右键单击数据库，然后选择**新查询**。

1. 在查询窗口中，编写 Transact SQL 查询，以便选择返回所有数据库的名称在服务器上。

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   如果您不熟悉编写查询，请参阅[编写 TRANSACT-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)。

1. 单击**Execute**按钮运行查询并查看结果。

   ![成功。 连接到 SQL 数据库服务器：SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

尽管可以执行几乎任何 Transact SQL 查询使用的管理任务，但 SSMS 是一种图形工具，可更轻松地管理 SQL Server。 以下部分提供使用图形用户界面的一些示例。

## <a name="create-and-manage-databases"></a>创建和管理数据库

在连接到*主*数据库，您可以在服务器上创建数据库以及修改或删除现有数据库。 以下步骤介绍如何通过 Management Studio 完成几项常见的数据库管理任务。 若要执行这些任务，请确保您连接到*主*您设置在 Linux 上的 SQL Server 时创建的服务器级别主体登录名的数据库。

### <a name="create-a-new-database"></a>新建数据库

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 中的服务器

2. 在对象资源管理器，右键单击*数据库*文件夹，，然后单击 * 新建数据库..."

3. 在中*新的数据库*对话框中，输入新数据库的名称，然后单击*确定*

已成功在服务器中创建新数据库。 如果倾向于创建新的数据库使用 T-SQL，则请参阅[CREATE DATABASE (SQL Server TRANSACT-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)。

### <a name="drop-a-database"></a>删除数据库

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 中的服务器

2. 在对象资源管理器，展开*数据库*文件夹，以查看在服务器上的所有数据库的列表。

3. 在对象资源管理器，右键单击你想要删除的数据库，然后单击*删除*

4. 在中*删除对象*对话框中，选中*关闭现有连接*，然后单击*确定*

已成功从服务器中删除数据库。 如果想使用 T-SQL 的数据库，请参阅[DROP DATABASE (SQL Server TRANSACT-SQL)](../t-sql/statements/drop-database-transact-sql.md)。

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>使用活动监视器查看有关 SQL Server 活动的信息

[活动监视器](../relational-databases/performance-monitor/activity-monitor.md)工具内置到 SQL Server Management Studio (SSMS)，并显示有关 SQL Server 进程以及这些进程如何影响 SQL Server 的当前实例的信息。

1. 启动 SSMS 并连接到 Linux 上的 SQL Server 中的服务器

1. 在对象资源管理器中右键单击*服务器*节点，并单击*活动监视器*

活动监视器显示可展开和折叠的窗格，提供以下信息：

- 概述
- 进程
- 资源等待
- 数据文件 I/O
- 最近耗费大量资源的查询
- 耗费大量资源的活动查询

展开某个窗格时，活动监视器会查询实例获取相关信息。 折叠窗格时，该窗格的所有查询活动都将停止。 可以同时展开一个或多个窗格，查看实例上不同种类的活动。

## <a name="see-also"></a>另请参阅
- [什么是 SSMS？](../ssms/sql-server-management-studio-ssms.md)
- [导出和导入的数据库使用 SSMS](sql-server-linux-migrate-ssms.md)
- [教程：SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [教程：编写 Transact-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)
- [服务器性能和活动监视](../relational-databases/performance/server-performance-and-activity-monitoring.md)
