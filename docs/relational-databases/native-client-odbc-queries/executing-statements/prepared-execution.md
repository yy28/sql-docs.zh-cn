---
title: 已准备好的执行 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8265ed80028d5d8ac9696853a29474552f401f3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297913"
---
# <a name="prepared-execution"></a>准备好的执行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC API 会定义准备好的执行，以此来减少反复执行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句时所需的分析和编译开销。 该应用程序生成一个包含 SQL 语句的字符串，然后分两个阶段执行该语句。 它调用[SQLPrepare 函数](https://go.microsoft.com/fwlink/?LinkId=59360)一次，由 分析语句并将其编译为执行计划[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。 然后，它调用**SQLExecute**执行，每次执行准备好的执行计划。 这节省了每次执行的分析和编译开销。 应用程序通常使用准备好的执行来重复执行相同的参数化 SQL 语句。  
  
 对于多数数据库中的需要执行三次或四次以上的语句，准备好的执行要比直接执行更快速。这主要是因为准备好的执行仅需编译一次语句，而直接执行的语句在每次执行时都需要编译。 准备好的执行还可以减少网络流量，因为驱动程序在每次执行语句时都可以向数据源发送执行计划标识符及参数值，而不是整个 SQL 语句。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]通过改进的算法来检测和重用**SQLExecDirect**的执行计划，减少了直接执行和准备执行之间的性能差异。 这使直接执行的语句也具备了准备好的执行的某些性能优势。 有关详细信息，请参阅[直接执行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还提供针对准备好的执行的本机支持。 执行计划建立在**SQLPrepare**上，后来在调用**SQLExecute**时执行。 由于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]不需要在**SQLPrepare**上构建临时存储过程，因此**在 tempdb**中的系统表上没有额外的开销。  
  
 出于性能原因，语句准备将延迟到调用**SQLExecute**或执行元属性操作（如 ODBC 中的[SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)或[SQLDescribeParam）。](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) 这是默认行为。 正在准备的语句如有任何错误，需等到执行该语句或执行元属性操作后才会发现。 将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序特定的语句属性 SQL_SOPT_SS_DEFER_PREPARE 设置为 SQL_DP_OFF 可以关闭此默认行为。  
  
 在延迟准备的情况下，在调用**SQLExecute**之前调用**SQLDescribeCol**或**SQLDescribeParam**将生成额外的服务器往返行程。 在**SQLDescribeCol**上，驱动程序从查询中删除 WHERE 子句，并将其发送到具有 SET FMTONLY ON 的服务器，以获取有关查询返回的第一个结果集中列的说明。 在**SQLDescribeParam**上，驱动程序调用服务器来获取查询中任何参数标记引用的表达式或列的说明。 此方法也存在一些限制，如无法解析子查询中的参数。  
  
 对[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序过度使用**SQLPrepare**会降低性能，尤其是在连接到早期版本的 SQL Server 时。 不应对执行一次的语句使用准备好的执行。 对于执行一次的语句，准备好的执行要比直接执行慢，因为它需要多进行一次从客户端到服务器的网络往返。 在早期版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，它还生成临时存储过程。  
  
 预定义语句不能用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上创建临时对象。  
  
 一些早期的 ODBC 应用程序在使用[SQLBind 参数](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)时都使用**SQLPrepare。** **SQLBind参数**不需要使用**SQLPrepare，** 它可以与**SQLExecDirect**一起使用。 例如，将**SQLExecDirect**与**SQLBind 参数**一起从仅执行一次的存储过程中检索返回代码或输出参数。 除非将多次执行同一语句，否则不要将**SQLPrepare**与**SQLBind 参数**一起使用。  
  
## <a name="see-also"></a>另请参阅  
 [执行声明&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
