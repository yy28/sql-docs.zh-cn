---
title: SQL 服务器本机客户端 |微软文档
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 30ef404501c498fca2c722e9eb88bb13997a17b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305014"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC 或 SQL Server 本机客户端是一个已互换用于引用 SQL Server 的 ODBC 和 OLE DB 驱动程序的术语。

> [!IMPORTANT] 
> SQL Server 本机客户端 （SQLNCLI） 仍然被弃用，不建议将其用于新的开发工作。 相反，请使用新的 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL)，其将使用最新的服务器功能进行更新。

> [!NOTE]
> 有关详细信息并下载 SNAC 或 ODBC 驱动程序，请参阅[SNAC 生命周期解释博客文章](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。
> 有关 SQL 服务器的 ODBC 驱动程序的详细信息，请参阅[SQL Server 的 Microsoft ODBC 驱动程序](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。  

 与[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]释放[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本机客户端功能的信息，这是 SQL Server 本机客户端的最后一个可用版本：

-   [SQL Server Native Client 对 LocalDB 的支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 中的 UTF-16 支持](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [对高可用性、灾难恢复的 SQL Server Native Client 支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [访问扩展事件日志中的诊断信息](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

本机客户端中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ODBC 支持在 Windows 7 SDK 中添加到标准 ODBC 的三个功能：  

-   异步执行与连接相关的操作。 有关详细信息，请参阅[异步执行](https://go.microsoft.com/fwlink/?LinkID=191493)。  

-   C 数据类型扩展能力。 有关详细信息，请参阅[ODBC 中的 C 数据类型](https://go.microsoft.com/fwlink/?LinkID=191495)。  

     为了在本机客户端中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持此功能，如果您的应用程序使用 ODBC 3.8，SQLGetDescField 可以返回**SQL_C_SS_TIME2（** 对于**时间**类型）或**SQL_C_SS_TIMESTAMPOFFSET（** 用于**日期时间偏移**），而不是**SQL_C_BINARY。** 有关详细信息，请参阅[ODBC 日期和时间改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  

-   多次使用小缓冲区调用**SQLGetData**以检索大型参数值。 有关详细信息，请参阅使用[SQLGetData 检索输出参数](https://go.microsoft.com/fwlink/?LinkID=191494)。  

 下列主题描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行为更改。  

-   调用**ICommand 与参数：：：set参数信息**时，传递给*pwszName*参数的值必须是一个有效的标识符。 有关详细信息，请参阅[ICommand 与参数](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  

-   **SQLDescribeParam**将始终如一地返回符合 ODBC 规范的值。 有关详细信息，请参阅[SQL 描述Param](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  

-   [处理字符转换时 ODBC 驱动程序行为的变化](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>请参阅  
[安装 SQL 服务器本机客户端](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
