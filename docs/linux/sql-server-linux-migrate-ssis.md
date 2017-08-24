---
title: "提取、 转换和加载数据使用 SSIS 的 Linux 上 |Microsoft 文档"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7317cad5aa1e77653431c128ce1549bc4349e18
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>提取、 转换和加载使用 SSIS 的 Linux 上的数据

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

本主题介绍如何在 Linux 上运行 SQL Server Integration Services (SSIS) 包。 SSIS 通过从多个源和格式，加载数据转换和清理数据，和更新多个目标，解决了复杂的数据集成问题。 

在 Linux 上运行的 SSIS 包可以连接到 Windows 本地或云中，在 Linux 上，或在 Docker 中运行的 Microsoft SQL Server。 它们还可以连接到 Azure SQL 数据库、 Azure SQL 数据仓库和 ODBC 数据源。

SSIS 可以用于在 Linux 上运行包，当你还有 Windows 计算机创建和维护包。 SSIS 设计和管理工具是 Windows 应用程序。 

## <a name="prerequisites"></a>必要條件

若要在 Linux 计算机上运行 SSIS 包，你首先需要安装 SQL Server Integration Services。 有关安装说明，请参阅[安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)。

## <a name="run-an-ssis-package"></a>运行 SSIS 包

若要在 Linux 计算机上运行 SSIS 包，请执行以下操作：

1.  将 SSIS 包复制到 Linux 计算机。
2.  运行以下命令：
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="more-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的详细信息

**ODBC 连接**。 借助上 Linux CTP 2.1 刷新及更高版本的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 此功能已测试 SQL Server 和 MySQL ODBC 驱动程序，但还需要使用任何 Unicode ODBC 驱动程序观察到 ODBC 规范。 在设计时，你可以提供一个 DSN 或连接字符串以连接到 ODBC 数据中;你还可以使用 Windows 身份验证。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

**路径**。 在 Linux 上的 SSIS 不支持 Linux 样式路径，但在运行时将 Windows 样式路径映射到 Linux 样式路径。 提供 Windows 样式在 SSIS 包的路径。 然后，例如，在 Linux 上的 SSIS 映射 Windows 样式路径`C:\test`到 Linux 样式路径`/test`。

**部署包**。 仅可以在此版本在 Linux 上文件系统中存储包。 SSIS 目录数据库和旧的 SSIS 服务不在 Linux 上可用于包部署和存储。

**计划包**。 不能使用在 Linux 上的 SQL 代理用于计划在此版本的包执行。

**其他限制和已知的问题**。 在 Linux 上运行 SSIS 包时，在此版本中不支持以下功能：
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

有关在 Linux 上的 SSIS 的详细信息，请参阅以下博客文章：

-   [在 Linux 上的 SSIS 位于 SQL Server 自 2017 年 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [在 Linux （SQL Server 自 2017 年 1 CTP 2.1 刷新） 上的 SSIS 支持 ODBC](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-about-ssis"></a>有关 SSIS 的详细信息

Microsoft SQL Server Integration Services (SSIS) 是一个平台，用于生成高性能数据集成解决方案，包括提取、 转换和加载 (ETL) 数据仓库的包。 有关 SSIS 的详细信息，请参阅 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md)。

SSIS 包括以下功能：
- 图形工具和用于生成和调试在 Windows 上的包向导
- 各种任务的执行如 FTP 操作的工作流功能，执行 SQL 语句，并将发送电子邮件
- 各种数据源和目标来提取和加载数据
- 大量的数据的清除、 聚合、 合并和复制数据的转换
- 用于扩展 SSIS 与你自己的自定义脚本和组件的应用程序编程接口 (Api)

若要开始使用 SSIS，下载最新版本[SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)。 然后按照本教程[SSIS 如何创建 ETL 包](https://msdn.microsoft.com/en-us/library/ms169917.aspx)。

## <a name="see-also"></a>另请参阅
- [了解有关 SQL Server Integration Services 的详细信息](https://msdn.microsoft.com/en-us/library/ms141026.aspx)
- [SQL Server Integration Services (SSIS) 开发和管理工具](https://msdn.microsoft.com/en-us/library/ms140028.aspx)
- [SQL Server Integration Services 教程](https://msdn.microsoft.com/en-us/library/jj720568.aspx)

