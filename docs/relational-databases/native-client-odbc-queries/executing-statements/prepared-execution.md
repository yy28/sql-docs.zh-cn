---
title: 准备好执行 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8ae1bfdadd360b41f451d7b0e7840af9e3f6ff94
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696898"
---
# <a name="prepared-execution"></a>准备好的执行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC API 会定义准备好的执行，以此来减少反复执行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句时所需的分析和编译开销。 该应用程序生成一个包含 SQL 语句的字符串，然后分两个阶段执行该语句。 它调用[SQLPrepare 函数](http://go.microsoft.com/fwlink/?LinkId=59360)一次具有分析和编译到执行计划的语句[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。 然后，它调用**SQLExecute**每次执行准备好的执行计划。 这节省了每次执行的分析和编译开销。 应用程序通常使用准备好的执行来重复执行相同的参数化 SQL 语句。  
  
 对于多数数据库中的需要执行三次或四次以上的语句，准备好的执行要比直接执行更快速。这主要是因为准备好的执行仅需编译一次语句，而直接执行的语句在每次执行时都需要编译。 准备好的执行还可以减少网络流量，因为驱动程序在每次执行语句时都可以向数据源发送执行计划标识符及参数值，而不是整个 SQL 语句。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 减少了通过改进的算法来检测和重用从的执行计划的直接和已准备好执行之间的性能差异**SQLExecDirect**。 这使直接执行的语句也具备了准备好的执行的某些性能优势。 有关详细信息，请参阅[直接执行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还提供针对准备好的执行的本机支持。 执行计划基于**SQLPrepare**和更高版本时执行**SQLExecute**调用。 因为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]不需要在上生成临时存储的过程**SQLPrepare**中的系统表上没有任何额外的开销**tempdb**。  
  
 出于性能原因，语句准备将推迟至**SQLExecute**称为或元属性操作 (如[SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)或[SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)ODBC 中) 执行。 这是默认行为。 正在准备的语句如有任何错误，需等到执行该语句或执行元属性操作后才会发现。 将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序特定的语句属性 SQL_SOPT_SS_DEFER_PREPARE 设置为 SQL_DP_OFF 可以关闭此默认行为。  
  
 延迟的情况下的准备、 调用**SQLDescribeCol**或**SQLDescribeParam**之前调用**SQLExecute**生成一个额外往返到服务器。 上**SQLDescribeCol**，驱动程序从查询中移除的 WHERE 子句，并将其发送到具有 SET FMTONLY ON，若要获取的列的说明中由查询返回的第一个结果集的服务器。 上**SQLDescribeParam**，驱动程序将调用服务器要得到的表达式或查询中的任何参数标记所引用的列的说明。 此方法也存在一些限制，如无法解析子查询中的参数。  
  
 额外的使用**SQLPrepare**与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，因此会降低性能，尤其是当连接到早期版本的 SQL Server。 不应对执行一次的语句使用准备好的执行。 对于执行一次的语句，准备好的执行要比直接执行慢，因为它需要多进行一次从客户端到服务器的网络往返。 在早期版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，它还生成临时存储过程。  
  
 预定义语句不能用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上创建临时对象。  
  
 使用某些早期的 ODBC 应用程序**SQLPrepare**随时[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)已使用。 **SQLBindParameter**不需要使用**SQLPrepare**，它可以用于**SQLExecDirect**。 例如，使用**SQLExecDirect**与**SQLBindParameter**要检索的返回代码或输出从仅执行一次的存储过程的参数。 不要使用**SQLPrepare**与**SQLBindParameter**除非同一语句将执行多次。  
  
## <a name="see-also"></a>请参阅  
 [执行语句&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
