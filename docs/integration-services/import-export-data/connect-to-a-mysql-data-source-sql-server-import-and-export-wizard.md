---
title: 连接到 MySQL 数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a359cdc0467d06cf0f67c1229981466f9b440101
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723924"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>连接到 MySQL 数据源（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”页或“选择目标”页连接到 MySQL 数据源。 有多个数据提供程序可用于连接到 MySQL。

> [!IMPORTANT]
> 连接到 MySQL 数据库的详细需求和先决条件不在此 Microsoft 文章的范围之内。 本文假定已安装了 MySQL 客户端软件，并且可以成功连接到目标 MySQL 数据库。 有关详细情况，请咨询 MySQL 数据库管理员或参阅 MySQL 文档。

## <a name="get-the-mysql-connectors"></a>获取 MySQL 连接器
从 [MySQL 连接器](https://dev.mysql.com/downloads/connector/)页面下载本主题中介绍的提供程序和驱动程序。

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>使用用于 MySQL 的 .NET Framework 数据提供程序连接到 MySQL
在向导的“选择数据源”页或“选择目标”页上选择“用于 MySQL 的 .NET Framework 数据提供程序”之后，页面显示用于提供程序的选项的分组列表。 其中包含许多不友好名称和不熟悉的设置。 幸运的是，只需提供几条信息。 可以忽略其他设置的默认值。

> [!NOTE]
> 无论 MySQL 是源还是目标，此数据提供程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

|必填信息|用于 MySQL 的 .NET Framework 数据提供程序属性|
|---|---|
|服务器名称|**Server**|
|数据库名称|**“数据库”**|
|身份验证（登录）信息|“用户 ID”和“密码”|

无须在列表的“ConnectionString”字段中输入连接字符串。 为 MySQL 服务器名称（“服务器”）输入单独值并输入登录信息后，向导会基于单独的属性及其值组合连接字符串。 

![使用 .NET 提供程序连接到 MySQL，1/2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![使用 .NET 提供程序连接到 MySQL，2/2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>使用 MySQL ODBC 驱动程序连接到 MySQL
ODBC 驱动程序未在数据源的下拉列表中列出。 要使用 ODBC 驱动程序连接，请首先在“选择数据源”页或“选择目标”页上选择“用于ODBC 的 .NET Framework 数据提供程序”作为数据源。 此提供程序充当 ODBC 驱动程序的包装器。

下面是选择用于 ODBC 的 .NET Framework 数据提供程序后随即显示的常规屏幕。

![先使用 ODBC 连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>要指定的选项（MySQL ODBC 驱动程序）

> [!NOTE]
> 无论 MySQL 是源还是目标，此数据提供程序和 ODBC 驱动程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

要使用 MySQL ODBC 驱动程序连接到 MySQL，请组合出一条包含以下设置及其值的连接字符串。 完整连接字符串的格式紧跟在设置列表之后。

> [!TIP]
> 获取有关组合出正确连接字符串的帮助。 或提供现有 DSN（数据源名称）或新建一个，而不是提供连接字符串。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
ODBC 驱动程序的名称。

**Server**  
MySQL 服务器的名称。 

**“数据库”**  
MySQL 数据库的名称。

**UID** 和 **PWD**   
要连接的用户 ID 和密码。

### <a name="connection-string-format"></a>连接字符串格式
以下是典型连接字符串的格式。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>输入连接字符串
在“选择数据源”页或“选择目标”页上的“ConnectionString”字段中输入连接字符串，或在“Dsn”字段中输入 DSN 名称。 输入连接字符串后，向导会分析该字符串，并在列表中显示各个属性及其值。

以下示例使用此连接字符串。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

下面是输入连接字符串后出现的屏幕。

![使用 ODBC 连接到 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何使用此处未列出的数据提供程序连接到 MySQL 的信息，请参阅 [MySQL connection strings](https://www.connectionstrings.com/mysql/)（MySQL 连接字符串）。 此第三方网站还包含有关此页介绍的数据提供程序和连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

