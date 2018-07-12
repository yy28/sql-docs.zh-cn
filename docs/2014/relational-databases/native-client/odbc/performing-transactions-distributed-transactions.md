---
title: 执行分布式的事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac35e6d366834e2d75e2aacd8311bd3f0ace1f5f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411506"
---
# <a name="performing-distributed-transactions"></a>执行分布式事务
  Microsoft 分布式事务处理协调器 (MS DTC) 允许应用程序跨两个或多个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例扩展事务。 此外，该协调器还允许应用程序参与由符合 Open Group DTP XA 标准的事务管理器管理的事务。  
  
 通常，所有事务管理命令都是通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序发送到服务器的。 应用程序通过调用启动一个事务[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)关闭自动提交模式。 然后，应用程序执行构成事务和调用的更新[SQLEndTran](../../native-client-odbc-api/sqlendtran.md)使用 SQL_COMMIT 或 SQL_ROLLBACK 选项。  
  
 当使用 MS DTC，但是，MS DTC 将成为事务管理器和应用程序不能再使用**SQLEndTran**。  
  
 在分布式事务中登记，然后在第二个分布式事务中登记时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序脱离原始分布式事务并在新事务中登记。 有关详细信息，请参阅[DTC 程序员参考](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)。  
  
## <a name="see-also"></a>请参阅  
 [执行事务&#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
