---
title: "提取、 转换和加载数据使用 SSIS 的 Linux 上 |Microsoft 文档"
description: 
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: aa4ac0cca739ea57a28beb399325d55b38502217
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>提取、 转换和加载使用 SSIS 的 Linux 上的数据

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主题介绍如何在 Linux 上运行 SQL Server Integration Services (SSIS) 包。 SSIS 从多个源和格式，提取数据，从而解决了复杂的数据集成问题转换和清理数据，并将数据加载到多个目标。 

在 Linux 上运行的 SSIS 包可以连接到 Windows 本地或云中，在 Linux 上，或在 Docker 中运行的 Microsoft SQL Server。 它们还可以连接到 Azure SQL 数据库、 Azure SQL 数据仓库、 ODBC 数据源、 平面文件和其他数据源，包括 ADO.NET 源、 XML 文件和 OData 服务。

关于 SSIS 的功能的详细信息，请参阅[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。

## <a name="prerequisites"></a>先决条件

若要在 Linux 计算机上运行 SSIS 包，你首先需要安装 SQL Server Integration Services。 SSIS 不包括在为 Linux 计算机安装 SQL Server。 有关安装说明，请参阅[安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)。

你还必须具有 Windows 计算机创建和维护包。 SSIS 设计和管理工具是不是当前适用于 Linux 计算机的 Windows 应用程序。 

## <a name="run-an-ssis-package"></a>运行 SSIS 包

若要在 Linux 计算机上运行 SSIS 包，请执行以下操作：

1.  将 SSIS 包复制到 Linux 计算机。
2.  运行以下命令：
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="other-common-ssis-tasks"></a>其他常见的 SSIS 任务

-   **设计包**。

    -   **连接到 ODBC 数据源**。 借助上 Linux CTP 2.1 刷新及更高版本的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 此功能已测试 SQL Server 和 MySQL ODBC 驱动程序，但还需要使用任何 Unicode ODBC 驱动程序观察到 ODBC 规范。 在设计时，你可以提供一个 DSN 或连接字符串以连接到 ODBC 数据中;你还可以使用 Windows 身份验证。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

    -   **路径**。 提供 Windows 样式在 SSIS 包的路径。 在 Linux 上的 SSIS 不支持 Linux 样式路径，但在运行时将 Windows 样式路径映射到 Linux 样式路径。 然后，例如，在 Linux 上的 SSIS 映射 Windows 样式路径`C:\test`到 Linux 样式路径`/test`。

-   **部署包**。 仅可以在此版本在 Linux 上文件系统中存储包。 SSIS 目录数据库和旧的 SSIS 服务不在 Linux 上可用于包部署和存储。

-   **计划包**。 你可以使用计划工具，如 Linux 系统`cron`计划包。 不能使用在 Linux 上的 SQL 代理用于计划在此版本的包执行。 有关详细信息，请参阅[计划 SSIS 包在 Linux 上的使用 cron](sql-server-linux-schedule-ssis-packages.md)。

## <a name="limitations-and-known-issues"></a>限制和已知的问题

### <a name="general-limitations-and-known-issues"></a>常规限制和已知的问题

在此版本的 Linux 上的 SSIS 不支持以下功能：
  - SSIS 目录数据库
  - SQL 代理计划的包执行
  - Windows 身份验证
  - 第三方组件
  - 变更数据捕获 (CDC)
  - SSIS 横向扩展
  - Azure Feature Pack for SSIS
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

其他限制和 Linux 上的 SSIS 的已知的问题，请参阅[发行说明](sql-server-linux-release-notes.md#ssis)。

### <a name="components"></a>支持和不支持组件

在 Linux 上支持以下内置 Integration Services 组件。 下表中所述，其中一些具有 Linux 平台上的限制。

在 Linux 上不支持未在此处列出的内置组件。

#### <a name="supported-control-flow-tasks"></a>支持控制流任务
- 大容量插入任务
- 数据流任务
- 数据事件探查任务
- 执行 SQL 任务
- 执行 T-SQL 语句任务
- 表达式任务
- FTP 任务
- Web 服务任务
- XML 任务

#### <a name="control-flow-tasks-supported-with-limitations"></a>支持限制的控制流任务

| 任务 | 限制 |
|------------|---|
| 执行进程任务 | 仅支持进程内模式。 |
| 文件系统任务 | *移动目录*和*设置文件属性*不支持操作。 |
| 脚本任务 | 仅支持标准的.NET Framework Api。 |
| 发送邮件任务 | 仅支持匿名用户模式。 |
| 传输数据库任务 | 不支持 UNC 路径。 |
| | |

#### <a name="supported-control-flow-containers"></a>支持控制流容器
- 序列容器
- For 循环容器
- Foreach 循环容器

#### <a name="supported-data-flow-sources-and-destinations"></a>支持的数据数据流源和目标
- 原始文件源和目标
- XML 源

#### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>数据流源和目标支持限制

| 组件 | 限制 |
|------------|---|
| ADO.NET 源和目标 | 仅支持 SQLClient 数据提供程序。 |
| 平面文件源和目标 | 仅支持 Windows 样式文件路径，默认路径映射规则应用于的。 例如`D:\home\ssis\travel.csv`变得`/home/ssis/travel.csv`。 |
| OData 源 | 仅支持基本身份验证。 |
| ODBC 源和目标 | 在 Linux 上支持 64 位 Unicode ODBC 驱动程序。 依赖于在 Linux 上的 UnixODBC 驱动程序管理器。 |
| OLE DB 源和目标 | 仅支持为 SQL Server 的 SQL Server Native Client 11.0 和 Microsoft OLE DB 访问接口。 |
| | |

#### <a name="supported-data-flow-transformations"></a>支持数据流转换
- Aggregate
- 审核
- 平衡的数据分发服务器
- 字符映射
- 有条件拆分
- 复制列
- 数据转换
- 派生列
- 导出列
- 模糊分组
- 模糊查找
- 导入列
- 查找
- 合并
- 合并联接
- 多播
- 透视
- 行计数
- 渐变维度
- Sort
- 字词查找
- Union All
- 逆透视

#### <a name="data-flow-transformations-supported-with-limitations"></a>数据流转换支持限制

| 组件 | 限制 |
|------------|---|
| OLE DB 命令转换 | 相同的限制的 OLE DB 源和目标。 |
| 脚本组件 | 仅支持标准的.NET Framework Api。 |
| | |

### <a name="supported-and-unsupported-log-providers"></a>支持和不支持的日志提供程序
所有内置的 SSIS 日志提供程序支持在 Linux 上除非 Windows 事件日志提供程序。

SQL Server 日志提供程序仅支持 SQL 身份验证;它不支持 Windows 身份验证。

SSIS 日志提供程序为文本文件、 XML 文件和 SQL Server 事件探查器将其输出写入你指定的文件中。 下列注意事项适用的文件路径：
-   如果不提供的路径，日志提供程序写入到主机的当前目录。 如果当前用户没有写入到主机的当前目录的权限，日志提供程序将引发错误。
-   不能使用环境变量中的文件路径。 如果你指定环境变量，你指定的文字文本将出现在文件路径中。 例如，如果你指定`%TMP%/log.txt`，日志提供程序将文本的文本追加`/%TMP%/log.txt`到当前的主机目录。

## <a name="more-info-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的详细信息

有关在 Linux 上的 SSIS 的详细信息，请参阅以下博客文章：

-   [在 Linux 上的 SSIS 位于 SQL Server 自 2017 年 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [在 Linux （SQL Server 自 2017 年 1 CTP 2.1 刷新） 上的 SSIS 支持 ODBC](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>有关 SSIS 的详细信息

Microsoft SQL Server Integration Services (SSIS) 是一个平台，用于生成高性能数据集成解决方案，包括提取、 转换和加载 (ETL) 数据仓库的包。 有关 SSIS 的详细信息，请参阅 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md)。

SSIS 包括以下功能：
- 图形工具和用于生成和调试在 Windows 上的包向导
- 各种任务的执行如 FTP 操作的工作流功能，执行 SQL 语句，并将发送电子邮件
- 各种数据源和目标来提取和加载数据
- 大量的数据的清除、 聚合、 合并和复制数据的转换
- 用于扩展 SSIS 与你自己的自定义脚本和组件的应用程序编程接口 (Api)

若要开始使用 SSIS，下载最新版本[SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md)。

## <a name="see-also"></a>另请参阅
- [了解有关 SQL Server Integration Services 的详细信息](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) 开发和管理工具](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 教程](../integration-services/integration-services-tutorials.md)

