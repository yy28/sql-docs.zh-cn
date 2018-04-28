---
title: 更新应用程序到 OLE DB 驱动程序适用于 SQL Server 从 MDAC |Microsoft 文档
description: 更新应用程序到 OLE DB 驱动程序适用于从 MDAC 的 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7754d3db286c69245c626f9af018749c38592b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>更新应用程序到 OLE DB 驱动程序适用于从 MDAC 的 SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  有大量的 OLE DB 驱动程序的 SQL Server 和 Microsoft 数据访问组件 (MDAC); 之间的差异从 Windows Vista 开始，数据访问组件现在称为 Windows 数据访问组件 （或 Windows DAC）。 虽然两者都提供对本机数据访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库，OLE DB 驱动程序的 SQL Server 专门设计了可公开的新功能[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，而在同时保持与早期版本的向后兼容性。   

 此外，虽然 MDAC 包含有关使用 OLE DB、 ODBC 和 ActiveX 数据对象 (ADO) 的组件，但 OLE DB 驱动程序的 SQL Server 仅实现 OLE DB （尽管 ADO 可以访问 SQL Server 的 OLE DB 驱动程序的功能）。  

 OLE DB 驱动程序的 SQL Server 和 MDAC 中其他以下几个方面不同：  

-   使用 ADO 来访问 SQL Server 的 OLE DB 驱动程序的用户可能会发现更少比访问 SQL OLE DB 提供程序它们的筛选功能。  

-   如果 ADO 应用程序使用 for SQL Server 的 OLE DB 驱动程序，并尝试更新计算的列，将报告错误。 对于 MDAC，此更新已接受，但被忽略。  

-   OLE DB 驱动程序的 SQL Server 是一个单一自包含的动态链接库 (DLL) 文件。 公开的接口已经保持为最低限度，这样既是为了减轻分发工作，也是为了降低安全风险。  

-   支持仅 OLE DB 接口。  

-   SQL Server 名称的 OLE DB 驱动程序是不同于与 MDAC 一起使用。  

-   当使用 SQL Server 的 OLE DB 驱动程序，提供的 MDAC 组件的用户访问功能才可用。 这包括但不限于以下功能：连接池、ADO 支持以及客户端游标支持。 当使用这些功能时，OLE DB 驱动程序的 SQL Server 提供仅数据库连接。 MDAC 可提供诸如跟踪、管理控件和性能计数器等功能。  

-   应用程序可以使用 OLE DB 核心服务与 OLE DB 驱动程序对于 SQL Server，但如果使用 OLE DB 游标引擎，它们应使用的数据类型兼容性选项以避免因为游标引擎并不知道新的可能会出现任何潜在问题[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]数据类型。  

-   OLE DB 驱动程序的 SQL Server 支持访问以前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。  

-   OLE DB 驱动程序的 SQL Server 不包含的 XML 集成。 OLE DB 驱动程序的 SQL Server 支持选择... XML 查询，但不支持任何其他 XML 功能。 但是，支持 OLE DB 驱动程序的 SQL Server **xml**中引入的数据类型[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  

-   OLE DB 驱动程序的 SQL Server 支持配置客户端网络库使用仅连接字符串属性。 如果需要更完整的网络库配置，您必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器。  

-   OLE DB 驱动程序的 SQL Server 不是 odbcbcp.dll 与兼容的。 必须重新生成应用程序将与 msoledbsql.lib 链接以便用于 SQL Server 的 OLE DB 驱动程序。    

-   MDAC 连接字符串允许一个布尔值 (**true**) 为**Trusted_Connection**关键字。 用于 SQL Server 连接字符串的 OLE DB 驱动程序必须使用**是**或**没有**。  

-   警告和错误已发生小的改动。 警告和错误由服务器现在返回保留相同的严重性时传递给 OLE DB 驱动程序的 SQL Server。 如果要依赖于捕获特定的警告和错误，则应当确保已经全面测试了应用程序。  

-   OLE DB 驱动程序的 SQL Server 具有更严格的错误检查比 MDAC，这意味着，某些应用程序不符合严格的 OLE DB 规范行为可能有所不同。 例如，SQLOLEDB 访问接口未强制执行规则的参数名称必须以开头 @ 的结果未参数，但是 SQL Server 的 OLE DB 驱动程序。  

-   OLE DB 驱动程序的 SQL Server 的行为有所不同，从 MDAC 关于失败的连接。 例如，MDAC 返回缓存的属性值以连接出现故障，而 OLE DB 驱动程序的 SQL Server 将向调用应用程序报告错误。  

-   OLE DB 驱动程序的 SQL Server 不生成 Visual Studio 分析器事件，但改为生成的 Windows 跟踪事件。  

-   OLE DB 驱动程序的 SQL Server 无法用于 perfmon。 Perfmon 是一种 Windows 工具，它仅可与使用 Windows 附带的 MDAC SQLODBC 驱动程序的 DSN 一起使用。  

-   当 OLE DB 驱动程序的 SQL Server 连接到[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]和更高版本，服务器错误 16947 作为 SQL_ERROR 返回。 定位更新无法更新行或定位删除无法删除行时，会出现此错误。 当 MDAC 连接到任何版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，服务器错误 16947 会作为警告 (SQL_SUCCESS_WITH_INFO) 返回。  

-   OLE DB 驱动程序的 SQL Server 实现**IDBDataSourceAdmin**接口，这是可选的 OLE DB 接口，未以前的实现，但只有**CreateDataSource**方法的可选接口实现。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   SQL Server 的 OLE DB 驱动程序中的表和 TABLE_INFO 返回同义词架构行集，与 TABLE_TYPE 设置为同义词。  

-   返回数据类型的值**varchar （max)**， **nvarchar (max)**， **varbinary （max)**， **xml**， **udt**，或其他大型对象类型不会返回到客户端版本早于[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果你想要使用这些类型作为返回值，则必须使用 SQL Server 的 OLE DB 驱动程序。  

-   MDAC 允许以下语句，以在开始时手动和隐式事务中执行，但 OLE DB 驱动程序的 SQL Server 没有。 这些语句必须以自动提交模式执行。  

    -   所有全文操作（索引和目录 DDL）  

    -   所有数据库操作（创建数据库、更改数据库以及删除数据库）  

    -   重新配置  

    -   Shutdown  

    -   Kill  

    -   Backup  

-   MDAC 应用程序连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的数据类型将显示为与 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 兼容的数据类型，如下表所示。  

    |SQL Server 2005 类型|SQL Server 2000 类型|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     此类型映射会影响为列元数据返回的值。 例如，**文本**列具有最大为 2147483647，但 OLE DB 驱动程序的 SQL Server 报告的最大大小**varchar （max)** 为 2147483647 或-1，具体取决于平台的列。  

-   OLE DB 驱动程序的 SQL Server 连接字符串中允许多义性 （例如，可能会超过一次，指定某些关键字和冲突关键字可能允许基于位置或的优先级的解决方法） 的向后兼容性原因。 OLE DB 驱动程序的 SQL Server 的未来版本可能不允许在连接字符串中的多义性。 修改应用程序以使用 OLE DB 驱动程序的 SQL Server 以消除任何依赖于连接字符串多义性时，它是很好的做法。  

-   如果你使用的 OLE DB 调用来启动事务，则 OLE DB 驱动程序的 SQL Server 和 MDAC; 之间的行为差异事务将立即开始与 OLE DB 驱动程序对于 SQL Server，但事务将开始后的第一个数据库访问使用 MDAC。 这可能会影响的存储的过程和批处理行为，因为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]需要@TRANCOUNT批处理或存储的过程和批处理或存储的过程开始时完成执行后必须相同。  

-   对于 OLE DB 驱动程序的 SQL Server，ITransactionLocal::BeginTransaction 将会导致事务要立即启动。 如果使用 MDAC，则事务会延迟，直到应用程序已执行要求事务处于隐式事务模式的语句后才启动。 有关详细信息，请参阅 [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  


 针对 SQL Server 和 MDAC 支持这两个 OLE DB 驱动程序读取已提交的事务隔离对 SQL Server 支持快照事务隔离使用行版本控制，但仅 OLE DB 驱动程序。 （就编程而言，使用行版本控制的已提交读事务隔离等同于已提交读事务。）  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
