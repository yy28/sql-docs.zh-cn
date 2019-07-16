---
title: 提取、 转换和加载使用 SSIS 在 Linux 上的数据
description: 本文介绍 SQL Server Integration Services (SSIS) 的 Linux 计算机
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e6230ee4efebc4b1af873a61e9f2ebfc191df171
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943811"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>提取、 转换和加载使用 SSIS 在 Linux 上的数据

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上运行 SQL Server Integration Services (SSIS) 包。 SSIS 从多个源和格式中提取数据，从而解决了复杂的数据集成问题转换和清理数据，并将数据加载到多个目标。 

在 Linux 上运行的 SSIS 包可以连接到运行在 Windows 本地或云中、 在 Linux 上，或者在 Docker 中的 Microsoft SQL Server。 它们还可以连接到 Azure SQL 数据库、 Azure SQL 数据仓库、 ODBC 数据源、 平面文件和其他数据源包括 ADO.NET 源、 XML 文件和 OData 服务。

有关 SSIS 的功能的详细信息，请参阅[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。

## <a name="prerequisites"></a>先决条件

若要在 Linux 计算机上运行 SSIS 包，您首先需要安装 SQL Server Integration Services。 SSIS 不包括在安装 SQL Server 的 Linux 计算机。 有关安装说明，请参阅[安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)。

您还必须有一台 Windows 计算机创建和维护包。 SSIS 设计和管理工具是不是目前适用于 Linux 计算机的 Windows 应用程序。 

## <a name="run-an-ssis-package"></a>运行 SSIS 包

若要在 Linux 计算机上运行 SSIS 包，请执行以下操作：

1.  将 SSIS 包复制到 Linux 计算机。
2.  运行下面的命令：
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>运行加密 （受密码保护） 包
有三种方法来运行 SSIS 包加密密码：

1.  将环境变量的值设置`SSIS_PACKAGE_DECRYPT`，如以下示例所示：

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  指定`/de[crypt]`选项输入密码以交互方式，如下面的示例中所示：

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  指定`/de`选项在命令行上提供的密码，如下面的示例中所示。 不推荐使用此方法，因为它在命令历史记录中存储该命令使用的解密密码。

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>设计包

**连接到 ODBC 数据源**。 使用 Linux CTP 2.1 刷新及更高版本的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 此功能经过了 SQL Server 和 MySQL ODBC 驱动程序，但也应使用 ODBC 规范将观察任何 Unicode ODBC 驱动程序。 在设计时，你可以提供 DSN 或连接字符串连接到 ODBC 数据;此外可以使用 Windows 身份验证。 有关详细信息，请参阅[博客文章在 Linux 上宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

**路径**。 提供 Windows 样式在 SSIS 包的路径。 Linux 上的 SSIS 不支持 Linux 样式的路径，但在运行时将 Windows 样式的路径映射到 Linux 样式的路径。 然后，例如，在 Linux 上的 SSIS 的 Windows 样式路径映射`C:\test`到 Linux 样式路径`/test`。

## <a name="deploy-packages"></a>部署包
只能将包存储在 Linux 上的文件系统中此版本中。 SSIS 目录数据库和旧 SSIS 服务不可以在 Linux 上的包部署和存储。

## <a name="schedule-packages"></a>计划包
可以使用 Linux 系统，如计划工具`cron`来安排包。 不能在 Linux 上使用 SQL 代理计划包执行在此版本中。 有关详细信息，请参阅[计划 SSIS 包在 Linux 上的使用 cron](sql-server-linux-schedule-ssis-packages.md)。

## <a name="limitations-and-known-issues"></a>限制和已知问题

有关限制和已知的问题的 Linux 上的 SSIS 的详细信息，请参阅[限制和已知的问题为 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md)。

## <a name="more-info-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的详细信息

有关在 Linux 上的 SSIS 的详细信息，请参阅以下博客文章：

-   [Linux 上的 SSIS 是 SQL Server CTP2.1 中可用](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [在 Linux （SQL Server CTP 2.1 刷新） 上的 SSIS 支持 ODBC](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>有关 SSIS 的详细信息

Microsoft SQL Server Integration Services (SSIS) 是一个平台，用于生成高性能数据集成解决方案，包括提取、 转换和加载 (ETL) 包针对数据仓库。 有关 SSIS 的详细信息，请参阅 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services)。

SSIS 包括以下功能：
- 图形工具和向导用于生成和调试 Windows 上的包
- 各种任务执行工作流功能，如 FTP 操作、 执行 SQL 语句和发送电子邮件
- 各种数据源和目标的提取和加载数据
- 各种用于清理、 聚合、 合并和复制数据的转换
- 应用程序编程接口 (Api) 用于 SSIS 扩展使用自己的自定义脚本和组件

若要开始使用 SSIS，下载最新版本[SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md)。

若要了解有关 SSIS 的详细信息，请参阅以下文章：
- [了解有关 SQL Server Integration Services 的详细信息](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) 开发和管理工具](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 教程](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>有关在 Linux 上的 SSIS 的相关的内容
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis conf 配置 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [限制和 Linux 上的 SSIS 的已知的问题](sql-server-linux-ssis-known-issues.md)
-   [计划 SQL Server Integration Services 包在 Linux 上的使用 cron 执行](sql-server-linux-schedule-ssis-packages.md)
