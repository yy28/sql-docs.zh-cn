---
title: 来自 MDAC 的更新
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1651eecd3238f737adfe82cfef0d574b5312b6c
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388277"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>将应用程序从 MDAC 更新到 SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 Microsoft 数据访问组件（MDAC；从 Windows Vista 开始，数据访问组件已改称为 Windows 数据访问组件或 Windows DAC）之间存在很多差异。 虽然都可提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的本机数据访问，但经过专门设计的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 可以公开 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的新功能，且同时保持了与早期版本的向后兼容性。  
  
 本主题中的信息有助于将您的 MDAC（或 Windows DAC）应用程序更新到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中附带的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 版本。 为了帮助您使此应用程序与在 中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]附带的本机客户端的版本保持最新，请参阅从 SQL Server [2005 本机客户端更新应用程序](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)。  
  
 此外，MDAC 包含使用 OLE DB、ODBC 和 ActiveX 数据对象 (ADO) 的组件，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 仅能实现 OLE DB 和 ODBC（尽管 ADO 可以访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的功能）。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 MDAC 在以下其他方面还存在区别：  
  
-   与访问 SQL OLE DB 访问接口相比，使用 ADO 访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 访问接口的用户可能会发现其筛选功能较少。  
  
-   如果 ADO 应用程序使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 并尝试更新计算列，则将会报告错误。 对于 MDAC，此更新已接受，但被忽略。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 是单个自包含的动态链接库 (DLL) 文件。 公开的接口已经保持为最低限度，这样既是为了减轻分发工作，也是为了降低安全风险。  
  
-   仅支持 OLE DB 和 ODBC 接口。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口和 ODBC 驱动程序名称与 MDAC 中使用的不同。  
  
-   使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时，将可以使用由 MDAC 组件提供的用户可访问功能。 这包括但不限于以下功能：连接池、ADO 支持以及客户端游标支持。 使用这些功能中的任意功能时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 仅提供数据库连接。 MDAC 可提供诸如跟踪、管理控件和性能计数器等功能。  
  
-   应用程序可以将 OLE DB 核心服务与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 一起使用，但如果使用 OLE DB 游标引擎，则应用程序应使用数据类型兼容选项以避免由于游标引擎不能识别新的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 数据类型而可能引起的任何潜在问题。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支持访问以前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不包含 XML 集成。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端支持 SELECT ...对于 XML 查询，但不支持任何其他 XML 功能。 但是，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端确实支持**xml**在 中[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]引入的 xml 数据类型。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支持仅使用连接字符串属性来配置客户端网络库。 如果需要更完整的网络库配置，您必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 与 odbcbcp.dll 不兼容。 必须重新生成同时使用 ODBC 和**bcp** API 的应用程序才能与 sqlncli11.lib[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]链接才能使用本机客户端。  
  
-   Microsoft OLE DB provider for ODBC (MSDASQL) 不支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 如果将 MDAC SQLODBC 驱动程序用于 MSDASQL 或将 MDAC SQLODBC 驱动程序用于 ADO，请在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中使用 OLE DB。  
  
-   MDAC 连接字符串允许将布尔值 (true****) 用于 Trusted_Connection**** 关键字。 本机客户端连接字符串必须使用**是**或否 。 **no** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   警告和错误已发生小的改动。 现在，服务器返回的警告和错误在传递给 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时会保留相同的严重性。 如果要依赖于捕获特定的警告和错误，则应当确保已经全面测试了应用程序。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的错误检查比 MDAC 更为严格，也就是说，某些不严格遵从 ODBC and OLE DB 规范的应用程序的行为可能有所不同。 例如，SQLOLEDB 提供程序没有强制实施参数名称必须以 ''\@开头的结果参数的规则，但[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序强制执行。  
  
-   对于失败的连接，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 与 MDAC 的行为有所不同。 例如，对于失败的连接 MDAC 将返回缓存的属性值，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将向调用应用程序报告错误。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不会生成 Visual Studio Analyzer 事件，而是生成 Windows 跟踪事件。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不能与 perfmon 一起使用。 Perfmon 是一种 Windows 工具，它仅可与使用 Windows 附带的 MDAC SQLODBC 驱动程序的 DSN 一起使用。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本时，服务器错误 16947 会作为 SQL_ERROR 返回。 定位更新无法更新行或定位删除无法删除行时，会出现此错误。 当 MDAC 连接到任何版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，服务器错误 16947 会作为警告 (SQL_SUCCESS_WITH_INFO) 返回。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端实现**IDBDataSourceAdmin**接口，该接口是以前未实现的可选 OLE DB 接口，但仅实现此可选接口的**CreateDataSource**方法。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   在 TABLE_TYPE 设置为 SYNONYM 的情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口返回 TABLES 和 TABLE_INFO 架构行集中的同义词。  
  
-   数据类型[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]varchar（max）、nvarchar（max）、varbinary（max）、xml、udt**udt**或其他大型对象类型的返回值不能返回到早于 的客户端版本。 **varchar(max)** **nvarchar(max)** **varbinary(max)** **xml** 如果希望将这些类型用作返回值，则必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
-   MDAC 允许在手动事务和隐式事务启动时执行以下语句，但 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不允许。 这些语句必须以自动提交模式执行。  
  
    -   所有全文操作（索引和目录 DDL）  
  
    -   所有数据库操作（创建数据库、更改数据库以及删除数据库）  
  
    -   重新配置  
  
    -   关机  
  
    -   终止  
  
    -   备份  
  
-   MDAC 应用程序连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的数据类型将显示为与 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 兼容的数据类型，如下表所示。  
  
    |SQL Server 2005 类型|SQL Server 2000 类型|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**图像**|  
    |**Udt**|**varbinary**|  
    |**xml**|**ntext**|  
  
     此类型映射会影响为列元数据返回的值。 例如，**文本**列的最大大小为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]2，147，483，647，但本机客户端 ODBC 将**varchar（最大）** 列的最大大小报告为SQL_SS_LENGTH_UNLIMITED，本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端 OLE DB 报告**varchar（最大）** 列的最大大小为 2，147，483，647 或 -1，具体取决于平台。  
  
-   出于向后兼容的原因，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 允许连接字符串中存在多义性（例如，可能多次指定某些关键字，以及可能允许基于位置或优先级对发生冲突的关键字进行冲突解决）。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的未来版本可能不允许连接字符串中存在多义性。 在修改要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的应用程序时，最好消除对连接字符串多义性的任何依赖。  
  
-   如果使用 ODBC 或 OLE DB 调用来启动事务，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 MDAC 的行为会有所不同；使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时将立即启动事务，但使用 MDAC 时事务将在第一次数据库访问后开始启动。 这可能会影响存储过程和批处理的行为，因为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]要求在\@\@批处理或存储过程完成执行后，TRANCOUNT 与批处理或存储过程启动时相同。  
  
-   使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端时，I事务本地：开始事务将导致立即启动事务。 如果使用 MDAC，则事务会延迟，直到应用程序已执行要求事务处于隐式事务模式的语句后才启动。 有关详细信息，请参阅 [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  
  
-   在将本机客户端驱动程序与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]System.Data.Odbc 一起使用服务器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]计算机时可能会遇到错误，该服务器计算机公开[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]了新的特定数据类型或功能。 System.Data.Odbc 提供了通用 ODBC 实现，随后不公开供应商特定的功能或扩展。 （本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端驱动程序已更新为本机支持最新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能。要解决此问题，可以还原到 MDAC，也可以迁移到 System.Data.SqlClient。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 MDAC 都支持使用行版本控制的已提交读事务隔离，但只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支持快照事务隔离。 （就编程而言，使用行版本控制的已提交读事务隔离等同于已提交读事务。）  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server Native Client 生成应用程序](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
