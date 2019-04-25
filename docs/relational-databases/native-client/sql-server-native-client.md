---
title: SQL Server 本机客户端 |Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3ce8d425aeb1c1b66f198efb4b222dc94c6e24ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62627976"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC 或 SQL Server Native Client 是一个术语，它已用于互换使用的 SQL Server，请参阅 ODBC 和 OLE DB 驱动程序。

**注意**：建议不要用于新的开发使用此驱动程序。 新的 OLE DB 访问接口称为[Microsoft OLE DB 驱动程序适用于 SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) 这将更新与今后的最新的服务器功能。


**有关详细信息并下载 SNAC 或 ODBC 驱动程序，请访问[所述的 SNAC 生命周期](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。**

SQL Server ODBC 驱动程序的更多信息，请参阅[Windows 上的 SQL Server 的 Microsoft ODBC 驱动程序](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx)。  此外，请参阅[引入新的 Microsoft ODBC Driver for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)，并[ODBC Driver 13.1 for SQL Server 发布](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/)。  

 信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 功能发布与[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，SQL Server 本机客户端的最后一个可用版本：

-   [SQL Server Native Client 对 LocalDB 的支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 中的 UTF-16 支持](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [对高可用性、灾难恢复的 SQL Server Native Client 支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [访问扩展事件日志中的诊断信息](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

中的 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端支持已添加到 Windows 7 SDK 中的标准 ODBC 的三个功能：  

-   异步执行与连接相关的操作。 有关详细信息，请参阅[异步执行](https://go.microsoft.com/fwlink/?LinkID=191493)。  

-   C 数据类型扩展能力。 有关详细信息，请参阅[ODBC 中的 C 数据类型](https://go.microsoft.com/fwlink/?LinkID=191495)。  

     若要支持此功能的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端，可以返回 SQLGetDescField **SQL_C_SS_TIME2** (对于**时间**类型) 或**SQL_C_SS_TIMESTAMPOFFSET** （适用于**datetimeoffset**) 而不是**SQL_C_BINARY**，如果你的应用程序使用 ODBC 3.8。 有关详细信息，请参阅[ODBC 日期和时间改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  

-   调用**SQLGetData**用小缓冲区多次来检索大型参数值。 有关详细信息，请参阅[使用 SQLGetData 检索输出参数](https://go.microsoft.com/fwlink/?LinkID=191494)。  

 下列主题描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行为更改。  

-   调用时**icommandwithparameters:: Setparameterinfo**，传递给的值*pwszName*参数必须是有效的标识符。 有关详细信息，请参阅[ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)。  

-   **SQLDescribeParam**将一致地返回符合 ODBC 规范的值。 有关详细信息，请参阅[SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)。  

-   [处理字符转换时 ODBC 驱动程序行为的变化](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>另请参阅  
[安装 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
