---
title: 直接执行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 725e89a937dbbd663f0e34bc24c1e8ee7e9a6eed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937275"
---
# <a name="direct-execution"></a>直接执行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  直接执行是最基本的语句执行方式。 应用程序生成一个字符字符串，包含[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句并将其提交执行使用**SQLExecDirect**函数。 当该语句到达服务器时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将其编译为执行计划，然后立即运行该执行计划。  
  
 直接执行是在运行时生成和执行语句的应用程序的常用执行方式，它也是只需执行一次的语句的最有效方法。 对于许多数据库而言，它的缺点就是每次执行 SQL 语句都必须对该语句进行分析和编译，如果该语句多次执行，就会增加开销。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 显著提高了在多用户环境中直接执行通常执行的语句的性能；如果将 SQLExecDirect 与参数标记配合用于通常执行的 SQL 语句，其效率可接近准备好的执行。  
  
 连接到的实例时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，则[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将使用[sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)传输的 SQL 语句或批处理中指定**SQLExecDirect**。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含的逻辑来快速确定如果 SQL 语句或批处理执行**sp_executesql**匹配的语句或批处理在内存中生成执行计划已存在。 如果匹配，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 只需重用现有计划，而无需编译新计划。 这意味着，通常执行的与执行 SQL 语句**SQLExecDirect**在系统中具有许多用户将受益于许多仅适用于早期版本的中的存储过程的计划重用率权益[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 仅当多个用户执行同一 SQL 语句或批处理时，才会从重用执行计划中受益。 请遵照以下编码约定，提高不同客户端执行的 SQL 语句的相似性，以便能够重用执行计划：  
  
-   不要在 SQL 语句中包括数据常量；改用绑定到程序变量的参数标记。 有关详细信息，请参阅[使用语句参数](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)。  
  
-   使用完全限定对象名。 如果未限定对象名，则不重用执行计划。  
  
-   令应用程序连接尽量使用常用的一组连接和语句选项。 从具有某一组选项（如 ANSI_NULLS）的连接生成的执行计划不会重复用于具有另一组选项的连接。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口的这些选项都具有相同的默认设置。  
  
 如果使用的所有语句都执行**SQLExecDirect**使用这些约定，编码[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可以重复使用执行计划，一旦有机会。  
  
## <a name="see-also"></a>请参阅  
 [执行语句&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
