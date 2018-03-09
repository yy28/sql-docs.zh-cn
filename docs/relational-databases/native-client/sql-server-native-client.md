---
title: "SQL Server Native Client |Microsoft 文档"
ms.date: 04/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7474d620d96880396e8fe7dc44e55b4cdcf7f440
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC 或 SQL Server Native Client，是一个术语，它已用于互换的 SQL Server，请参阅 ODBC 和 OLE DB 驱动程序。 

**有关详细信息和下载 SNAC 或 ODBC 驱动程序，请访问[SNAC 生命周期所述](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。**

SQL Server ODBC 驱动程序的更多信息，请参阅[Microsoft ODBC Driver for SQL Server on Windows](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx)。  此外，请参阅[为 SQL Server 中引入新的 Microsoft ODBC 驱动程序](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)，和[ODBC Driver 13.1 for SQL Server 发布](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/)。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布时的本机客户端功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，SQL Server native Client 的最后一个可用版本： 
  
-   [SQL Server Native Client 对 LocalDB 的支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
  
-   [元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0 中的 UTF-16 支持](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [对高可用性、 灾难恢复的 SQL Server Native Client 支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [访问扩展事件日志中的诊断信息](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
中的 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端支持三种功能，已添加到 Windows 7 SDK 中的标准 ODBC:  
  
-   异步执行与连接相关的操作。 有关详细信息，请参阅[异步执行](http://go.microsoft.com/fwlink/?LinkID=191493)。  
  
-   C 数据类型扩展能力。 有关详细信息，请参阅[ODBC 中的 C 数据类型](http://go.microsoft.com/fwlink/?LinkID=191495)。  
  
     为了支持此功能在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端，可以返回 SQLGetDescField **SQL_C_SS_TIME2** (有关**时间**类型) 或**SQL_C_SS_TIMESTAMPOFFSET** （适用于**datetimeoffset**) 而不是**SQL_C_BINARY**，如果你的应用程序使用 ODBC 3.8。 有关详细信息，请参阅[ODBC 日期和时间的改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  
  
-   调用**SQLGetData**使用较小的缓冲区多次检索大型参数值。 有关详细信息，请参阅[检索输出参数使用 SQLGetData](http://go.microsoft.com/fwlink/?LinkID=191494)。  
  
 下列主题描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行为更改。  
  
-   在调用时**ICommandWithParameters::SetParameterInfo**，传递给值*pwszName*参数必须是有效的标识符。 有关详细信息，请参阅[ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  
  
-   **SQLDescribeParam**将始终返回一个 ODBC 规范一致的值。 有关详细信息，请参阅[SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  
  
-   [处理字符转换时 ODBC 驱动程序行为的变化](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>另请参阅  
[安装 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
