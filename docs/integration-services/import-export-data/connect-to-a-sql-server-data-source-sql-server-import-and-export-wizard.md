---
title: "连接到 SQL Server 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17910c8e30dee98f39e977896fb67774b54a798d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>连接到 SQL Server 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**Microsoft SQL Server**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。 没有可用于连接到 SQL Server 的多个数据提供程序。

> [!TIP]
> 如果要在具有多个服务器的网络上，它可能更轻松地输入服务器名称，而不是展开的服务器的下拉列表。 如果单击下拉列表，它可能需要大量时间来查询网络中的所有可用的服务器，并且结果可能不甚至包含所需的服务器。

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用用于 SQL Server 的 .NET Framework 数据提供程序连接到 SQL Server 
选择后**SQL Server 的.NET Framework 数据提供程序**上**选择数据源**或**选择目标**向导页面的页面显示分组的提供程序选项的列表。 其中许多为友好名称，不熟悉的设置。 幸运的是，若要连接到任何企业数据库，通常必须提供仅有几条信息。 你可以忽略其他设置的默认值。

> [!NOTE]
> SQL Server 是否您的源或目标，此数据提供程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

|所需的信息|.Net framework Data Provider for SQL Server 属性|
|---|---|
|服务器名称|**数据源**|
|身份验证 （登录名） 信息|**集成安全性**; 或者，**用户 ID**和**密码**<br/>如果你想要在服务器上发现的数据库下拉列表，你首先必须提供有效的登录信息。|
|数据库名称|**初始目录**|

![使用.NET 提供程序连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>选项，以指定 （.NET Framework 数据提供程序的 SQL Server）

> [!NOTE]
> SQL Server 是否您的源或目标，此数据提供程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

**数据源**  
 输入的名称或 IP 地址的源或目标服务器，或从下拉列表选择一个服务器。  
 
 若要指定非标准的 TCP 端口，输入逗号后的服务器名称或 IP 地址，然后输入端口号。
 
 **初始目录**  
 输入源或目标数据库名称，或从下拉列表中选择数据库。  
  
 **Integrated Security**  
 指定**True**连接使用 Windows 集成身份验证 （推荐），或**False**连接与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 如果指定 **False**，则必须输入用户 ID 和密码。 默认值为 **False**。  
  
 **用户 ID**  
 输入用户名，如果你使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。  
  
 **密码**  
 如果你使用的输入的密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>For SQL Server 使用 ODBC 驱动程序连接到 SQL Server 
ODBC 驱动程序未列出在下拉列表中的数据源。 若要连接使用 ODBC 驱动程序，首先要选择**适用于 ODBC 的.NET Framework 数据提供程序**作为数据源。 此提供程序充当 ODBC 驱动程序周围的包装器。

> [!TIP]
> **获取最新的驱动程序**。 下载[Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)。

这是在选择用于 ODBC 的.NET Framework 数据提供程序之后立即看到泛型屏幕。

![连接到与之前的 ODBC SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>选项，以指定 （SQL Server ODBC 驱动程序）

> [!NOTE]
> SQL Server 是否您的源或目标，ODBC 驱动程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

若要使用最新的 ODBC 驱动程序连接到 SQL Server，组建连接字符串中包含以下设置和它们的值。 完整的连接字符串的格式紧随的设置的列表。

> [!TIP]
> 获取组合看起来正好的连接字符串的帮助。 或者，提供的连接字符串，而是提供现有的 DSN （数据源名称），或创建一个新。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
ODBC 驱动程序的名称。 名称是不同的不同版本的驱动程序。

**Server**  
SQL Server 的名称。

**数据库**  
数据库的名称。  

**Trusted_Connection**; 或者， **Uid**和**Pwd**  
指定**Trusted_Connection = Yes**以与 Windows 集成身份验证; 连接，或者指定**Uid** (用户 id) 和**Pwd** （密码） 来与 SQL Server 身份验证连接。

### <a name="connection-string-format"></a>连接字符串格式
下面是使用 Windows 集成身份验证的连接字符串的格式。

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

下面是使用 SQL Server 身份验证而不是 Windows 集成身份验证的连接字符串的格式。

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>输入连接字符串
输入中的连接字符串**ConnectionString**字段，或输入中的 DSN 名称**Dsn**字段中，**选择数据源**或**选择目标**页。 输入连接字符串后，向导将分析字符串，并在列表中显示的各个属性及其值。

下面的示例使用此连接字符串。

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

下面是你输入的连接字符串后看到的屏幕。

![连接到使用 ODBC 后的 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>为 SQL Server 或 SQL Server Native Client 连接到 SQL Server 的 Microsoft OLE DB 访问接口

> [!IMPORTANT]
> SQL Server 2012 起中，Microsoft OLE DB Provider for SQL Server 和 SQL Server Native Client 中的 SQL Server 版本不支持。 改为使用 ODBC 驱动程序。 若要了解有关转换到 ODBC 驱动程序的详细信息，请参阅以下博客文章。
>   -   [Microsoft 通过 ODBC 对齐进行本机关系数据访问](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [为 SQL Server 中引入新的 Microsoft ODBC 驱动程序](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何连接到 SQL Server 未在此处列出的数据访问接口的信息，请参阅[SQL Server 连接字符串](https://www.connectionstrings.com/sql-server/)。 此第三方站点还包含有关数据提供程序和在此页上所述的连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


