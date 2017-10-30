---
title: "连接到 Oracle 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e589e7f7a0262d258342bf887ec84c57d57dc978
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>连接到 Oracle 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**Oracle**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。 有几个数据提供程序可用于连接到 Oracle。

> [!IMPORTANT]
> 详细的要求和连接到 Oracle 数据库的先决条件是 Microsoft 本文的范畴。 本文假定你已安装的 Oracle 客户端软件，并且，你可以已成功连接到目标 Oracle 数据库。 有关详细信息，请参阅 Oracle 数据库管理员或 Oracle 文档。

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>连接到 Oracle 使用.Net Framework Data Provider for Oracle
选择后**适用于 Oracle 的.NET Framework 数据提供程序**上**选择数据源**或**选择目标**页的向导页上显示的提供程序选项的一个分组的列表。 其中许多为友好名称，不熟悉的设置。 幸运的是，你只需提供信息的两个或三个部分。 你可以忽略其他设置的默认值。

> [!NOTE]
> Oracle 是否您的源或目标，此数据提供程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

|所需的信息|.Net framework Data Provider for Oracle 属性|
|---|---|
|服务器名称|**数据源**|
|身份验证 （登录名） 信息|**用户 ID**和**密码**; 或者，**集成安全性**|

无需输入中的连接字符串**ConnectionString**字段的列表。 每个值输入 Oracle 服务器名称后 (**数据源**) 和登录信息，该向导将来自单独的属性和它们的值组合的连接字符串。 

![使用.NET 提供程序连接到 Oracle](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>连接到 Oracle 使用 Microsoft ODBC driver for Oracle
ODBC 驱动程序未列出在下拉列表中的数据源。 若要连接使用 ODBC 驱动程序，首先要选择**适用于 ODBC 的.NET Framework 数据提供程序**上的数据源作为**选择数据源**或**选择目标**页。 此提供程序充当 ODBC 驱动程序周围的包装器。

这是在选择用于 ODBC 的.NET Framework 数据提供程序之后立即看到泛型屏幕。

![连接到 Oracle 与之前的 ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>选项，以指定 （适用于 Oracle 的 ODBC 驱动程序）

> [!NOTE]
> Oracle 是否您的源或目标，此数据提供程序和 ODBC 驱动程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

若要连接到 Oracle Oracle 的 ODBC 驱动程序，组建连接字符串中包含以下设置和它们的值。 完整的连接字符串的格式紧随的设置的列表。

> [!TIP]
> 获取组合看起来正好的连接字符串的帮助。 或者，提供的连接字符串，而是提供现有的 DSN （数据源名称），或创建一个新。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
ODBC 驱动程序，名称**适用于 Oracle 的 Microsoft ODBC**。

**Server**  
Oracle 服务器的名称。 

**Uid**和**Pwd**   
用户 id 和密码以连接。

### <a name="connection-string-format"></a>连接字符串格式
以下是典型的连接字符串的格式。

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>输入连接字符串
输入中的连接字符串**ConnectionString**字段，或输入中的 DSN 名称**Dsn**字段中，**选择数据源**或**选择目标**页。 输入连接字符串后，向导将分析字符串，并在列表中显示的各个属性及其值。

下面是你输入的连接字符串后看到的屏幕。

![连接到 Oracle ODBC 与](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>我 Oracle 服务器名是什么？
运行以下查询以获取 Oracle 服务器的名称之一。

`SELECT host_name FROM v$instance`

或

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何连接到 Oracle 未在此处列出的数据访问接口的信息，请参阅[Oracle 连接字符串](https://www.connectionstrings.com/oracle/)。 此第三方站点还包含有关数据提供程序和在此页上所述的连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


