---
title: "连接到 MySQL 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3df56fcda5b39c2895de83feac4f302686b1adf3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>连接到 MySQL 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**MySQL**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。 没有可用于连接到 MySQL 的几个数据提供程序。

> [!IMPORTANT]
> 详细的要求和连接到 MySQL 数据库的先决条件是 Microsoft 本文的范畴。 本文假定你已安装的 MySQL 客户端软件，并且，你可以已成功连接到的目标 MySQL 数据库。 有关详细信息，请查阅你的 MySQL 数据库管理员或 MySQL 文档。

## <a name="get-the-mysql-connectors"></a>获取 MySQL 连接器
下载提供程序和驱动程序从本主题中所述[MySQL 连接器](https://dev.mysql.com/downloads/connector/)页。

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>连接到 MySQL 使用.Net Framework 数据提供程序 MySQL
选择后**MySQL 的.NET Framework 数据提供程序**上**选择数据源**或**选择目标**页的向导页上显示的提供程序选项的一个分组的列表。 其中许多为友好名称，不熟悉的设置。 幸运的是，你只需提供几条信息。 你可以忽略其他设置的默认值。

> [!NOTE]
> MySQL 是您的源还是目标，此数据提供程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

|所需的信息|.Net framework 数据提供程序 MySQL 属性|
|---|---|
|服务器名称|**Server**|
|数据库名称|**数据库**|
|身份验证 （登录名） 信息|**用户 Id**和**密码**|

无需输入中的连接字符串**ConnectionString**字段的列表。 每个值输入 MySQL 服务器名称后 (**服务器**) 和登录信息，该向导将来自单独的属性和它们的值组合的连接字符串。 

![使用.NET 提供程序，1，共 2 连接到 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![使用.NET 提供程序，2 2 连接到 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>使用 MySQL ODBC 驱动程序连接到 MySQL
ODBC 驱动程序未列出在下拉列表中的数据源。 若要连接使用 ODBC 驱动程序，首先要选择**适用于 ODBC 的.NET Framework 数据提供程序**上的数据源作为**选择数据源**或**选择目标**页。 此提供程序充当 ODBC 驱动程序周围的包装器。

这是在选择用于 ODBC 的.NET Framework 数据提供程序之后立即看到泛型屏幕。

![连接到与之前的 ODBC SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>选项，以指定 （MySQL ODBC 驱动程序）

> [!NOTE]
> MySQL 是您的源还是目标，此数据提供程序和 ODBC 驱动程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

若要使用 MySQL ODBC 驱动程序连接到 MySQL，组建连接字符串中包含以下设置和它们的值。 完整的连接字符串的格式紧随的设置的列表。

> [!TIP]
> 获取组合看起来正好的连接字符串的帮助。 或者，提供的连接字符串，而是提供现有的 DSN （数据源名称），或创建一个新。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
ODBC 驱动程序的名称。

**Server**  
MySQL server 的名称。 

**数据库**  
MySQL 数据库的名称。

**UID**和**PWD**   
用户 id 和密码以连接。

### <a name="connection-string-format"></a>连接字符串格式
以下是典型的连接字符串的格式。

    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>

### <a name="enter-the-connection-string"></a>输入连接字符串
输入中的连接字符串**ConnectionString**字段，或输入中的 DSN 名称**Dsn**字段中，**选择数据源**或**选择目标**页。 输入连接字符串后，向导将分析字符串，并在列表中显示的各个属性及其值。

下面的示例使用此连接字符串。

    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********

下面是你输入的连接字符串后看到的屏幕。

![连接到使用 ODBC 的 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何使用未在此处列出的数据访问接口连接到 MySQL 的信息，请参阅[MySQL 连接字符串](https://www.connectionstrings.com/mysql/)。 此第三方站点还包含有关数据提供程序和在此页上所述的连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


