---
title: 连接到 PostgreSQL 数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7d3e27e4f4fdf813e30775c2cf44cfb4ca272b10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114662"
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>连接到 PostgreSQL 数据源（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主题向你介绍如何从 SQL Server 导入和导出向导的“选择数据源”页或“选择目标”页连接到 PostgreSQL 数据源    。 

> [!IMPORTANT]
> 连接到 PostgreSQL 数据库的详细需求和先决条件不在此 Microsoft 文章的范围之内。 本文假定已安装了 PostgreSQL 客户端软件，并且已成功连接到目标 PostgreSQL 数据库。 有关详细信息，请咨询 PostgreSQL 数据库管理员或参阅 PostgreSQL 文档。

## <a name="get-the-postgresql-odbc-driver"></a>获取 PostgreSQL ODBC 驱动程序

### <a name="install-the-odbc-driver-with-stack-builder"></a>使用堆栈生成器安装 ODBC 驱动程序
运行堆栈生成器，向 PostgreSQL 安装添加 PostgreSQL ODBC 驱动程序 (psqlODBC)。

![使用堆栈生成器安装 PostgreSQL ODBC](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>或者下载最新版 ODBC 驱动程序
或者从此 FTP 站点直接下载用于最新版 PostgreSQL ODBC 驱动程序 (psqlODBC) 的 Windows 安装程序：[https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/)。 从 .zip 文件中提取文件并运行 .msi 文件。

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>使用 PostgreSQL ODBC 驱动程序 (psqlODBC) 连接到 PostgreSQL
ODBC 驱动程序不在数据源的下拉列表中列出。 要使用 ODBC 驱动程序连接，请首先在“选择数据源”页或“选择目标”页上选择“用于ODBC 的 .NET Framework 数据提供程序”作为数据源    。 此提供程序充当 ODBC 驱动程序的包装器。

下面是选择用于 ODBC 的 .NET Framework 数据提供程序后随即显示的常规屏幕。

![先使用 ODBC 连接到 PostgreSQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>要指定的选项（PostgreSQL ODBC 驱动程序）

> [!NOTE]
> 无论 PostgreSQL 是源还是目标，此数据提供程序和 ODBC 驱动程序的连接选项是相同的。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的   。

若要使用 PostgreSQL ODBC 驱动程序连接到 PostgreSQL，请组合包含以下设置及其值的连接字符串。 完整连接字符串的格式紧跟在设置列表之后。

> [!TIP]
> 获取有关组合出正确连接字符串的帮助。 或提供现有 DSN（数据源名称）或新建一个，而不是提供连接字符串。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
ODBC 驱动程序的名称 - 可以为 PostgreSQL ODBC Driver(UNICODE) 或 PostgreSQL ODBC Driver(ANSI)   。

**Server**  
PostgreSQL 服务器的名称。 

**端口**  
用于连接到 PostgreSQL 服务器的端口。

**“数据库”**  
PostgreSQL 数据库的名称。

Uid 和 Pwd      
要连接的 UID（用户 ID）和密码   。

### <a name="connection-string-format"></a>连接字符串格式
以下是典型连接字符串的格式。 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>输入连接字符串
在“选择数据源”页或“选择目标”页上的“ConnectionString”字段中输入连接字符串，或在“Dsn”字段中输入 DSN 名称     。 输入连接字符串后，向导会分析该字符串，并在列表中显示各个属性及其值。

以下示例使用此连接字符串。

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

下面是输入连接字符串后出现的屏幕。

![使用 ODBC 连接到 PostgreSQL](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何使用此处未列出的数据提供程序连接到 PostgreSQL 的信息，请参阅 [PostgreSQL 连接字符串](https://www.connectionstrings.com/postgresql/)。 此第三方网站还包含有关此页介绍的数据提供程序和连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

