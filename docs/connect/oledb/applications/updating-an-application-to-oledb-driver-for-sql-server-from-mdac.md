---
title: 将应用程序从 MDAC 更新到适用于 SQL Server 的 OLE DB 驱动程序 | Microsoft Docs
description: 将应用程序从 MDAC 更新到适用于 SQL Server 的 OLE DB 驱动程序
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 6b2c3ba7bc7ea16a4079cb247b4e7159b40eeb1a
ms.sourcegitcommit: 5152caf8f4346f8b565742bc1df4e454551d63eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37042667"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>将应用程序从 MDAC 更新到适用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序和 Microsoft 数据访问组件 (MDAC) 之间存在很多不同；从 Windows Vista 开始，数据访问组件改名为 Windows 数据访问组件（或 Windows DAC）。 虽然两者都可提供对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的本机数据访问权限，但适用于 SQL Server 的 OLE DB 驱动程序经过专门地设计以公开 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能，且同时保持了与早期版本的后向兼容性。   

 此外，MDAC 包含使用 OLE DB、 ODBC 和 ActiveX 数据对象 (ADO) 的组件，OLE DB 驱动程序适用于 SQL Server 仅实现 OLE DB （尽管 ADO 可以访问针对 SQL Server 的 OLE DB 驱动程序的功能）。  

 OLE DB 驱动程序适用于 SQL Server 和 MDAC 在以下其他方面不同：  

-   使用 ADO 访问针对 SQL Server 的 OLE DB 驱动程序的用户可能会发现比它们在访问 SQL OLE DB 提供程序时筛选功能较少。  

-   如果 ADO 应用程序使用 SQL Server 的 OLE DB 驱动程序，并尝试更新计算的列，将报告错误。 使用 MDAC，会接受但忽略此更新。  

-   OLE DB 驱动程序适用于 SQL Server 是单个自包含的动态链接库 (DLL) 文件。 公开的接口已经保持为最低限度，这样既是为了减轻分发工作，也是为了降低安全风险。  

-   支持仅 OLE DB 接口。  

-   对于 SQL Server 名称，OLE DB 驱动程序是不同于与 MDAC 中使用的名称。  

-   使用 SQL Server 的 OLE DB 驱动程序时，由 MDAC 组件提供的用户可访问功能都可用。 这包括但不限于以下功能：连接池、ADO 支持以及客户端游标支持。 当使用这些功能时，OLE DB 驱动程序适用于 SQL Server 仅提供数据库连接。 MDAC 可提供诸如跟踪、管理控件和性能计数器等功能。  

-   应用程序可将 OLE DB 核心服务与适用于 SQL Server 的 OLE DB 驱动程序配合使用，但如果使用 OLE DB 游标引擎，则应使用数据类型兼容性选项，从而避免可能由于游标引擎不能识别新的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 数据类型而引起的任何潜在问题。  

-   OLE DB 驱动程序适用于 SQL Server 支持访问以前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。  

-   OLE DB 驱动程序适用于 SQL Server 不包含 XML 集成。 OLE DB Driver for SQL Server 支持选择... XML 查询，但不支持任何其他 XML 功能。 但是，支持 OLE DB 驱动程序适用于 SQL Server **xml**中的数据类型引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  

-   适用于 SQL Server 的 OLE DB 驱动程序支持仅使用连接字符串属性来配置客户端网络库。 如果需要更完整的网络库配置，您必须使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器。  

-   MDAC 连接字符串允许通过布尔值 (**，则返回 true**) 用于**Trusted_Connection**关键字。 SQL Server 连接字符串用于 OLE DB 驱动程序必须使用**是**或**没有**。  

-   警告和错误已发生小的改动。 现在，服务器返回的警告和错误在传递给适用于 SQL Server 的 OLE DB 驱动程序时会保留相同的严重性。 如果要依赖于捕获特定的警告和错误，则应当确保已经全面测试了应用程序。  

-   适用于 SQL Server 的 OLE DB 驱动程序的错误检查比 MDAC 更为严格，也就是说，某些不严格遵从 OLE DB 规范的应用程序可能会有不同的表现。 例如，SQLOLEDB 访问接口不强制执行结果参数的参数名称必须以“\@”开头这一规则，而适用于 SQL Server 的 OLE DB 驱动程序会强制执行此规则。  

-   OLE DB 驱动程序适用于 SQL Server 的行为以不同的方式从 MDAC 有关失败的连接。 例如连接失败的情况，MDAC 会返回缓存的属性值，而适用于 SQL Server 的 OLE DB 驱动程序会向调用应用程序报告错误。  

-   适用于 SQL Server 的 OLE DB 驱动程序不会生成 Visual Studio Analyzer 事件，而是生成 Windows 跟踪事件。  

-   OLE DB 驱动程序适用于 SQL Server 不能使用与 perfmon 一起使用。 Perfmon 是一种 Windows 工具，它仅可与使用 Windows 附带的 MDAC SQLODBC 驱动程序的 DSN 一起使用。  

-   当 OLE DB 驱动程序适用于 SQL Server 连接到[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]和更高版本，服务器错误 16947 会作为 sql_error 返回返回。 定位更新无法更新行或定位删除无法删除行时，会出现此错误。 当 MDAC 连接到任何版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，服务器错误 16947 会作为警告 (SQL_SUCCESS_WITH_INFO) 返回。  

-   适用于 SQL Server 的 OLE DB 驱动程序实现 IDBDataSourceAdmin 接口（是一个以前未实现的可选 OLE DB 接口），但只实现了此可选接口的 CreateDataSource 方法。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   在 TABLE_TYPE 设置为 SYNONYM 的情况下，适用于 SQL Server 的 OLE DB 驱动程序返回 TABLES 和 TABLE_INFO 架构行集中的同义词。  

-   数据类型 varchar(max)、nvarchar(max)、varbinary(max)、xml、udt 或其他大型对象类型的返回值不能返回到早于 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的客户端版本。 如果想要将这些类型用作返回值，则必须使用适用于 SQL Server OLE DB 驱动程序。  

-   MDAC 允许在手动事务和隐式事务启动时执行以下语句，但适用于 SQL Server 的 OLE DB 驱动程序不允许。 这些语句必须以自动提交模式执行。  

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
    |**varbinary(max)**|**图像**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     此类型映射会影响为列元数据返回的值。 例如，**文本**列的最大大小为 2147483647，但 OLE DB 驱动程序适用于 SQL Server 报告的最大大小**varchar （max)** 为 2,147,483,647 或-1，具体取决于平台的列。  

-   考虑到后向兼容性，适用于 SQL Server 的 OLE DB 驱动程序允许连接字符串中存在多义性（例如，可能多次指定某些关键字，并且可能允许基于位置或优先级对发生冲突的关键字进行解析）。 OLE DB Driver for SQL Server 的未来版本可能不允许在连接字符串中的多义性。 在修改要使用适用于 SQL Server 的 OLE DB 驱动程序的应用程序时，最好消除连接字符串多义性上的任何依赖项。  

-   如果使用的 OLE DB 调用来启动事务，则 OLE DB 驱动程序适用于 SQL Server 和 MDAC; 之间的行为差异事务将立即开始使用 OLE DB 驱动程序对于 SQL Server，但使用 MDAC 的第一个数据库访问后，将开始事务。 这可能会影响存储过程和批处理的行为，因为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 要求不管是在批处理或存储过程执行结束后还是在该批处理或存储过程启动时 @@TRANCOUNT 均应相同。  

-   使用 OLE DB 驱动程序适用于 SQL Server，ITransactionLocal::BeginTransaction 将导致事务立即启动。 如果使用 MDAC，则事务会延迟，直到应用程序已执行要求事务处于隐式事务模式的语句后才启动。 有关详细信息，请参阅 [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  


 用于 SQL Server 和 MDAC 都支持这两个 OLE DB 驱动程序读取已提交的事务隔离对 SQL Server 支持快照事务隔离使用行版本控制，但仅 OLE DB 驱动程序。 （就编程而言，使用行版本控制的已提交读事务隔离等同于已提交读事务。）  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
