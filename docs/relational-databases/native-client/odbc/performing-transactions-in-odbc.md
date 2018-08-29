---
title: ODBC 中的事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba7af1fa77fc310860a3f0fdca84c9b203549c7b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058926"
---
# <a name="performing-transactions-in-odbc"></a>在 ODBC 中执行事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 中的事务按连接级别进行管理。 在应用程序完成某一事务时，它提交或回滚通过该连接上的所有语句句柄完成的所有工作。 若要提交或回滚事务，应用程序应调用[SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md)而非提交 COMMIT 或 ROLLBACK 语句。  
  
 应用程序调用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)管理事务的两个 ODBC 模式之间切换：  
  
-   自动提交模式  
  
     每个语句都在成功完成后自动提交。 当您在自动提交模式中运行时，不要求其他事务管理功能。  
  
-   手动提交模式  
  
     所有执行的语句包含在同一事务中，直到通过调用明确停止它**SQLEndTran**。  
  
 自动提交模式是针对 ODBC 的默认的事务模式。 建立连接，它是自动提交模式，直到**SQLSetConnectAttr**调用来切换到手动提交模式，从而自动提交模式设置。 在应用程序关闭自动提交后，发送到数据库的下一个语句将开始某一事务。 该事务随后仍然有效，直到应用程序调用**SQLEndTran**使用 SQL_COMMIT 或 SQL_ROLLBACK 选项。 命令发送到数据库后**SQLEndTran**启动下一个事务。  
  
 如果应用程序从手动提交模式切换到自动提交模式，则驱动程序将提交在该连接上当前打开的所有事务。  
  
 ODBC 应用程序不应使用 Transact-SQL 事务语句（例如 BEGIN TRANSACTION、COMMIT TRANSACTION 或 ROLLBACK TRANSACTION），因为这可能导致驱动程序中的不确定行为。 ODBC 应用程序应在自动提交模式下运行和不使用任何事务管理函数或语句，或在手动提交模式下运行并使用 ODBC **SQLEndTran**函数提交或回滚事务。  
  
## <a name="see-also"></a>请参阅  
 [执行事务&#40;ODBC&#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
