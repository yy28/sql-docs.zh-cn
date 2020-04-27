---
title: 错误消息 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b38734544ac3accb3ddfdbcae8ae92f67b252e54
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805851"
---
# <a name="error-messages"></a>错误消息
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序返回的消息文本将放在**SQLGetDiagRec**的*MessageText*参数中。 错误源由消息标头指示：  
  
 [Microsoft][ODBC 驱动程序管理器]  
 这些错误由 ODBC 驱动程序管理器引发。  
  
 [Microsoft][ODBC 游标库]  
 这些错误由 ODBC 游标库引发。  
  
 [Microsoft][SQL Server Native Client]  
 这些错误是由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序引发的。 如果没有名为 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他节点，驱动程序就会发生该错误。  
  
 微软[SQL Server Native Client][*Net-transportname*]  
 这些错误由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]网络库引发，其中*net-transportname*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络传输（例如，命名管道、共享内存、tcp/ip 套接字或 VIA）的显示名称。 错误消息的提醒内容含有调用的 Net-Library 函数以及 TDS 函数在基础网络 API 中调用的函数。 返回的*pfNative*错误代码是基础网络协议堆栈中的错误代码。  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 这些错误由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引发。 错误消息中的提醒内容是来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的错误消息文本。 返回的*pfNative*代码是来自[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的错误号。 有关可返回的错误消息（及其数字）列表的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅中**master** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]master 数据库中**sysmessages**系统表的 "描述" 和 "错误" 列。  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](handling-errors-and-messages.md)  
  
  
