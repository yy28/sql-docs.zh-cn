---
title: 错误消息 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d632d1d22cd8439a3d787e22301ec06ec4e0d93
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291668"
---
# <a name="error-messages"></a>错误消息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序返回的消息文本放置在**SQLGetDiagRec**的*MessageText*参数中。 错误源由消息标头指示：  
  
 [Microsoft][ODBC 驱动程序管理器]  
 这些错误由 ODBC 驱动程序管理器引发。  
  
 [Microsoft][ODBC 游标库]  
 这些错误由 ODBC 游标库引发。  
  
 [Microsoft][SQL Server Native Client]  
 这些错误由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序引发。 如果没有名为 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他节点，驱动程序就会发生该错误。  
  
 [微软][SQL 服务器本机客户端][*净传输名称*]  
 这些错误由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Net-库引发，其中*Net 传输名称*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络传输的显示名称（例如，命名管道、共享内存、TCP/IP 套接字或 VIA）。 错误消息的提醒内容含有调用的 Net-Library 函数以及 TDS 函数在基础网络 API 中调用的函数。 随这些错误返回的*pfNative*错误代码是基础网络协议堆栈中的错误代码。  
  
 [微软][SQL 服务器本机客户端][ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 这些错误由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引发。 错误消息中的提醒内容是来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的错误消息文本。 随这些错误返回的*pfNative*代码是从 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回的错误编号。 有关 可以返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的错误消息列表（及其编号）的详细信息，请参阅 中**master**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主数据库中**sysmessages**系统表的说明和错误列。  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
