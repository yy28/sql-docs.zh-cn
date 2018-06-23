---
title: 错误消息 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ba9c50f600caf23a6948752ce34e816e493a41b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016835"
---
# <a name="error-messages"></a>错误消息
  返回的消息的文本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序放入*MessageText*参数**SQLGetDiagRec**。 错误源由消息标头指示：  
  
 [Microsoft][ODBC 驱动程序管理器]  
 这些错误由 ODBC 驱动程序管理器引发。  
  
 [Microsoft][ODBC 游标库]  
 这些错误由 ODBC 游标库引发。  
  
 [Microsoft][SQL Server Native Client]  
 通过在引发这些错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。 如果没有名为 Net-Library 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他节点，驱动程序就会发生该错误。  
  
 [Microsoft][SQL Server Native Client][*Net Transportname*]  
 通过在引发这些错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Net-library，其中*Net Transportname*是的显示名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络传输 （例如，命名管道、 共享内存、 TCP/IP 套接字或 VIA）。 错误消息的提醒内容含有调用的 Net-Library 函数以及 TDS 函数在基础网络 API 中调用的函数。 *PfNative*出现这些错误返回错误代码是基础的网络协议堆栈中的错误代码。  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 这些错误由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引发。 错误消息中的提醒内容是来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的错误消息文本。 *PfNative*返回与这些错误代码是从的错误号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关可以返回的错误消息 （和其数字） 的列表详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅的说明和错误列**sysmessages**系统表位于**master**数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [处理错误和消息](handling-errors-and-messages.md)  
  
  