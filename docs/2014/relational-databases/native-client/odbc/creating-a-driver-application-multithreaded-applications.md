---
title: 多线程应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
author: rothja
ms.author: jroth
ms.openlocfilehash: b680086f76e0c1a1e8c8cfc2f4ef82099957b3fd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055905"
---
# <a name="multithreaded-applications"></a>多线程应用程序
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序是多线程驱动程序。 编写多线程应用程序是使用异步调用处理多个 ODBC 调用的替代方法。 线程可以进行同步 ODBC 调用，而在第一个线程被阻塞以等待其调用的响应时可以处理其他线程。 此模型比进行异步调用效率更高，因为它避免了诸如网络流量的开销以及对 SQL_STILL_EXECUTING 执行重复的 ODBC 函数调用测试。  
  
 异步模式仍是一种有效的处理方法。 尽管多线程模型的性能不断改进，但是仍没有必要对异步应用程序进行重新编写。 如果用户正在转换使用 DB-Library 异步模型的 DB-Library 应用程序，将它们转换为 ODBC 异步模型更为容易。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SQL Server Native Client ODBC 驱动程序应用程序](creating-a-driver-application.md)  
  
  
