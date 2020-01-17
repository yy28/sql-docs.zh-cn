---
title: 连接到 SQL Server 数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 938a6d8ba779d1cef37b5fab767e609d00b4f022
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308007"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>连接到 SQL Server 数据源（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”  页或“选择目标”  业连接到 Microsoft SQL Server  。 有多种数据提供程序可用来连接 SQL Server。

> [!TIP]
> 如果位于具有多个服务器的网络中，相比展开服务器的下拉列表，可能输入服务器名称会更便捷一些。 如果单击下拉列表，查询所有可用服务器的网络可能需要很长时间，并且结果可能甚至不会包含需要的服务器。

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用用于 SQL Server 的 .NET Framework 数据提供程序连接到 SQL Server 
在向导的“选择数据源”  页或“选择目标”  页上选择“用于 SQL Server 的 .NET Framework 数据提供程序”  之后，页面显示用于提供程序的选项的分组列表。 其中许多是不友好名称和不熟悉的设置。 所幸，要连接到任何企业数据库，通常只需要提供几条信息。 可以忽略其他设置的默认值。

> [!NOTE]
> 无论 SQL Server 是源还是目标，此数据提供程序的连接选项是相同的。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的   。

|必填信息|用于 SQL Server 的 .Net Framework 数据提供程序属性|
|---|---|
|Authentication|“集成安全性”默认为“NotSpecified”，也可选择其他身份验证模式  。 不支持“交互式 Active Directory 身份验证”。 |
|服务器名称|**数据源**|
|身份验证（登录）信息|“集成安全性”或“用户 ID”和“密码”   <br/>如果想查看服务器上的数据库的下拉列表，首先必须提供有效的登录信息。|
|数据库名称|**初始目录**|

![使用 .NET 提供程序连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>要指定的选项（用于 SQL Server 的 .NET Framework 数据提供程序）

> [!NOTE]
> 无论 SQL Server 是源还是目标，此数据提供程序的连接选项是相同的。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的   。

**数据源**  
 输入源或目标服务器的名称或 IP 地址，或从下拉列表选择服务器。  
 
 若要指定非标准 TCP 端口，请在服务器名称或 IP 地址之后输入逗号，然后输入端口号。
 
 **初始目录**  
 输入源或目标提供程序的名称，或从下拉列表选择服务器。  
  
 **Integrated Security**  
 使用 Windows 集成身份验证进行连接（建议），请指定 True  ；若要用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接，请指定 False  。 如果指定 **False**，则必须输入用户 ID 和密码。 默认值为 **False**。  
  
 **用户 ID**  
 如果正在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请输入用户名。  
  
 **密码**  
 如果正在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请输入密码。  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>使用用于 SQL Server 的 ODBC 驱动程序连接到 SQL Server 
ODBC 驱动程序不在数据源的下拉列表中列出。 若要使用 ODBC 驱动程序连接，首先选择“用于 ODBC 的 .NET Framework 数据提供程序”作为数据源  。 此提供程序充当 ODBC 驱动程序的包装器。

> [!TIP]
> 获取最新的驱动程序  。 下载[用于 SQL Server 的 Microsoft ODBC Driver 13](https://www.microsoft.com/download/details.aspx?id=53339)。

下面是选择用于 ODBC 的 .NET Framework 数据提供程序后随即显示的常规屏幕。

![先使用 ODBC 连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>要指定的选项（用于 SQL Server 的 ODBC 驱动程序）

> [!NOTE]
> 无论 SQL Server 是源还是目标，ODBC 驱动程序的连接选项是相同的。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的   。

若要使用最新的 ODBC 驱动程序连接到 SQL Server，请组合出一条包含以下设置及其值的连接字符串。 完整连接字符串的格式紧跟在设置列表之后。

> [!TIP]
> 获取有关组合出正确连接字符串的帮助。 或提供现有 DSN（数据源名称）或新建一个，而不是提供连接字符串。 有关这些选项的详细信息，请参阅[连接到 ODBC 数据源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驱动程序**  
ODBC 驱动程序的名称。 驱动程序不同版本的名称不同。

**Server**  
SQL Server 的名称。

**Database**  
数据库的名称。  

Trusted_Connection；或 Uid 和 Pwd     
将 Trusted_Connection=Yes  指定为通过 Windows 集成身份验证进行连接；或将 Uid  （用户 ID）或 Pwd  （密码）指定为通过 SQL Server 身份验证进行连接。

### <a name="connection-string-format"></a>连接字符串格式
下面是使用 Windows 集成身份验证的连接字符串的格式。

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

下面是使用 SQL Server 身份验证（而不是使用 Windows 集成身份验证）的连接字符串的格式。

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>输入连接字符串
在“选择数据源”页或“选择目标”页上的“ConnectionString”字段中输入连接字符串，或在“Dsn”字段中输入 DSN 名称     。 输入连接字符串后，向导会分析该字符串，并在列表中显示各个属性及其值。

以下示例使用此连接字符串。

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

下面是输入连接字符串后出现的屏幕。

![之后使用 ODBC 连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>使用用于 SQL Server 或 SQL Server Native Client 的 Microsoft OLE DB 提供程序连接到 SQL Server

> [!IMPORTANT]
> SQL Server 2012 之后的 SQL Server 版本不支持用于 SQL Server 和 SQL Server Native Client 的 Microsoft OLE DB 提供程序。 请改用 ODBC 驱动程序。 若要了解有关转为使用 ODBC 驱动程序的详细信息，请参阅以下博客文章。
>   -   [Microsoft 正在与 ODBC 对齐以进行本机关系数据访问](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [引入新的 Microsoft ODBC Drivers for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>其他数据提供程序和详细信息
有关如何使用此处未列出的数据提供程序连接到 SQL Server 的信息，请参阅 [SQL Server 连接字符串](https://www.connectionstrings.com/sql-server/)。 此第三方网站还包含有关此页介绍的数据提供程序和连接参数的详细信息。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

