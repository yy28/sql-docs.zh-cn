---
title: 执行分布式事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2baaa43fdf638dcd1f6794eaa9f5cf76df424c06
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707078"
---
# <a name="performing-distributed-transactions"></a>执行分布式事务
  Microsoft 分布式事务处理协调器 (MS DTC) 允许应用程序跨两个或多个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例扩展事务。 此外，该协调器还允许应用程序参与由符合 Open Group DTP XA 标准的事务管理器管理的事务。  
  
 通常，所有事务管理命令都是通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序发送到服务器的。 应用程序通过在关闭自动提交模式的情况下调用[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)来启动事务。 然后，应用程序执行包含该事务的更新，并通过 SQL_COMMIT 或 SQL_ROLLBACK 选项调用[SQLEndTran](../../native-client-odbc-api/sqlendtran.md) 。  
  
 但是，在使用 MS DTC 时，MS DTC 成为事务管理器，应用程序不再使用**SQLEndTran**。  
  
 在分布式事务中登记，然后在第二个分布式事务中登记时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序脱离原始分布式事务并在新事务中登记。 有关详细信息，请参阅[DTC 程序员参考](https://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;执行事务](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
