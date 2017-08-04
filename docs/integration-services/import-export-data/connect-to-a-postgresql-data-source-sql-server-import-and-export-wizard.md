---
title: "连接到 PostgreSQL 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c82ae7eedc3e18e7591cf7ab30a507920695247
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>连接到 PostgreSQL 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**PostgreSQL**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。 

> [!IMPORTANT]
> 详细的要求和连接到 PostgreSQL 数据库先决条件不在 Microsoft 本文的讨论范围。 本文假定你已安装 PostgreSQL 客户端软件，并且，你可以已成功连接到目标 PostgreSQL 数据库。 有关详细信息，请查阅 PostgreSQL 数据库管理员联系或 PostgreSQL 文档。

## <a name="get-the-postgresql-odbc-driver"></a>获取 PostgreSQL ODBC 驱动程序

### <a name="install-the-odbc-driver-with-stack-builder"></a>使用堆栈生成器安装 ODBC 驱动程序
运行堆栈生成器 PostgreSQL ODBC 驱动程序 (psqlODBC) 添加到你的 PostgreSQL 的安装。

![使用堆栈生成器安装 PostgreSQL ODBC](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>或者，下载最新的 ODBC 驱动程序
或者，直接从 FTP 站点的下载 PostgreSQL ODBC 驱动程序 (psqlODBC) 的最新版本 Windows installer [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/)。 从该.zip 文件中提取文件，并运行.msi 文件。

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>使用 PostgreSQL ODBC 驱动程序 (psqlODBC) 连接到 PostgreSQL
ODBC 驱动程序未列出在下拉列表中的数据源。 若要连接使用 ODBC 驱动程序，首先要选择**适用于 ODBC 的.NET Framework 数据提供程序**上的数据源作为**选择数据源**或**选择目标**页。 此提供程序充当 ODBC 驱动程序周围的包装器。

这是在选择用于 ODBC 的.NET Framework 数据提供程序之后立即看到泛型屏幕。

![连接到与之前的 ODBC PostgreSQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>选项，以指定 （PostgreSQL ODBC 驱动程序）

> [!NOTE]
> PostgreSQL 是您的源还是目标，此数据提供程序和 ODBC 驱动程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

若要使用 PostgreSQL ODBC 驱动程序连接到 PostgreSQL，组建连接字符串中包含以下设置和它们的值。 完整的连接字符串的格式紧随的设置的列表。

> [!TIP]
> 获取组合看起来正好的连接字符串的帮助。 或者，提供的连接字符串，而是提供现有的 DSN （数据源名称），或创建一个新。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
名称的 ODBC 驱动程序-请**PostgreSQL ODBC Driver(UNICODE)**或**PostgreSQL ODBC Driver(ANSI)**。

**Server**  
PostgreSQL 服务器的名称。 

**端口**  
要用于连接到 PostgreSQL 服务器的端口。

**数据库**  
PostgreSQL 数据库的名称。

**Uid**和**Pwd**   
**Uid** (用户 id) 和**Pwd** （密码） 进行连接。

### <a name="connection-string-format"></a>连接字符串格式
以下是典型的连接字符串的格式。 

    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>

### <a name="enter-the-connection-string"></a>输入连接字符串
输入中的连接字符串**ConnectionString**字段，或输入中的 DSN 名称**Dsn**字段中，**选择数据源**或**选择目标**页。 输入连接字符串后，向导将分析字符串，并在列表中显示的各个属性及其值。

下面的示例使用此连接字符串。

    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********

下面是你输入的连接字符串后看到的屏幕。

![连接到使用 ODBC 的 PostgreSQL](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何连接到 PostgreSQL 的数据提供程序未在此处列出的信息，请参阅[PostgreSQL 连接字符串](https://www.connectionstrings.com/postgresql/)。 此第三方站点还包含有关数据提供程序和在此页上所述的连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


