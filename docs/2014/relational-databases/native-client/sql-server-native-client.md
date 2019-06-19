---
title: 什么&#39;SQL Server Native Client 中的新增功能的 s |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2a01b9d9d13bf5e9135d287553beb8b87c2dcd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638851"
---
# <a name="what39s-new-in-sql-server-native-client"></a>什么&#39;s SQL Server Native Client 中的新增功能
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 会安装 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client。 没有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client。  
  
 未来 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 ODBC 驱动程序将不会再更新。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中 ODBC 驱动程序的后继版本（在 Windows 上称为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）将随 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 一同安装。 有关详细信息[!INCLUDE[msCoName](../../includes/msconame-md.md)]ODBC Driver 11 for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上 Windows，请参阅[Microsoft ODBC Driver 11 for SQL Server-Windows](https://www.microsoft.com/download/details.aspx?id=36434)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 最近更新了 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 中的 OLE DB Provider。 想要使用 OLE DB 访问接口连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最新版本的开发人员必须使用在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 中随附的 OLE DB 访问接口。  
  
 下列主题说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中新增的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 重要功能。  
  
-   [SQL Server Native Client 对 LocalDB 的支持](features/sql-server-native-client-support-for-localdb.md)  
  
-   [元数据发现](features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0 中的 UTF-16 支持](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [对高可用性、灾难恢复的 SQL Server Native Client 支持](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [访问扩展事件日志中的诊断信息](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 ODBC 现在支持添加到 Windows 7 SDK 中的标准 ODBC 的三项功能：  
  
-   异步执行与连接相关的操作。 有关详细信息，请参阅[异步执行](https://go.microsoft.com/fwlink/?LinkID=191493)。  
  
-   C 数据类型扩展能力。 有关详细信息，请参阅[ODBC 中的 C 数据类型](https://go.microsoft.com/fwlink/?LinkID=191495)。  
  
     以支持此功能的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端，可以返回 SQLGetDescField `SQL_C_SS_TIME2` (对于`time`类型) 或`SQL_C_SS_TIMESTAMPOFFSET`(对于`datetimeoffset`) 而不是`SQL_C_BINARY`，如果你的应用程序使用 ODBC 3.8。 有关详细信息，请参阅[ODBC 日期和时间改进的数据类型支持](features/date-and-time-improvements.md)。  
  
-   用小缓冲区多次调用 `SQLGetData` 来检索一个大型参数值。 有关详细信息，请参阅[使用 SQLGetData 检索输出参数](https://go.microsoft.com/fwlink/?LinkID=191494)。  
  
 下列主题描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行为更改。  
  
-   调用时`ICommandWithParameters::SetParameterInfo`，传递给的值*pwszName*参数必须是有效的标识符。 有关详细信息，请参阅[ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md)。  
  
-   `SQLDescribeParam` 现在将一致地返回符合 ODBC 规范的值。 有关详细信息，请参阅[SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md)。  
  
-   [处理字符转换时 ODBC 驱动程序行为的变化](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](features/sql-server-native-client-features.md)  
  
  
