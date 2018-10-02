---
title: 连接到 Oracle 数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9bbb8092756cd12599c17d8dd7abeaba774689f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761895"
---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>连接到 Oracle 数据源（SQL Server 导入和导出向导）
本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”或“选择目标”页连接到 Oracle 数据源。 有多种数据提供程序可用来连接 Oracle。

> [!IMPORTANT]
> 此 Microsoft 文章不涵盖 Oracle 数据库连接相关详细要求和先决条件。 本文假定已安装 Oracle 客户端软件，并且可以成功连接目标 Oracle 数据库。 有关详细信息，请咨询 Oracle 数据库管理员或参阅 Oracle 文档。

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>使用用于 Oracle 的 .NET Framework 数据提供程序连接到 Oracle
在向导的“选择数据源”页或“选择目标”页上选择用于 Oracle 的 .NET Framework 数据提供程序之后，页面显示用于提供程序的选项的分组列表。 其中许多是不友好名称和不熟悉的设置。 幸运的是，只需提供两条或三条信息。 可以忽略其他设置的默认值。

> [!NOTE]
> 无论 Oracle 是源还是目标，此数据提供程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

|必填信息|用于 Oracle 的 .Net Framework 数据提供程序属性|
|---|---|
|服务器名称|**数据源**|
|身份验证（登录）信息|“用户 ID”和“密码”或“集成安全性”|

无须在列表的“ConnectionString”字段中输入连接字符串。 为 Oracle 服务器名称（“数据源”）输入单个值和登录信息后，向导会根据单个属性及其值组合出连接字符串。 

![使用 .NET 提供程序连接到 Oracle](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>使用用于 Oracle 的 Microsoft ODBC 驱动程序连接到 Oracle
ODBC 驱动程序不在数据源的下拉列表中列出。 要使用 ODBC 驱动程序连接，请首先在“选择数据源”页或“选择目标”页上选择“用于ODBC 的 .NET Framework 数据提供程序”作为数据源。 此提供程序充当 ODBC 驱动程序的包装器。

下面是选择用于 ODBC 的 .NET Framework 数据提供程序后随即显示的常规屏幕。

![先使用 ODBC 连接到 Oracle](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>要指定的选项（用于 Oracle 的 ODBC 驱动程序）

> [!NOTE]
> 无论 Oracle 是源还是目的地，此数据提供程序和 ODBC 驱动程序的连接选项是相同的。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

若要使用用于 Oracle 的 ODBC 驱动程序连接到 Oracle，请组合出一条包含以下设置及其值的连接字符串。 完整连接字符串的格式紧跟在设置列表之后。

> [!TIP]
> 获取有关组合出正确连接字符串的帮助。 或提供现有 DSN（数据源名称）或新建一个，而不是提供连接字符串。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

驱动程序  
用于 Oracle 的 Microsoft ODBC 驱动程序的名称。

**Server**  
Oracle 服务器的名称。 

Uid 和 Pwd   
要连接的用户 ID 和密码。

### <a name="connection-string-format"></a>连接字符串格式
以下是典型连接字符串的格式。

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>输入连接字符串
在“选择数据源”页或“选择目标”页上的“ConnectionString”字段中输入连接字符串，或在“Dsn”字段中输入 DSN 名称。 输入连接字符串后，向导会分析该字符串，并在列表中显示各个属性及其值。

下面是输入连接字符串后出现的屏幕。

![使用 ODBC 连接到 Oracle](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>我的 Oracle 服务器名称是什么？
运行以下查询之一以获取 Oracle 服务器名称。

`SELECT host_name FROM v$instance`

或多个

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何使用此处未列出的数据提供程序连接到 Oracle 的详细信息，请参阅 [Oracle 连接字符串](https://www.connectionstrings.com/oracle/)。 此第三方网站还包含有关此页介绍的数据提供程序和连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

