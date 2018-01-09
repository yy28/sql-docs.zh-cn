---
title: "处理结果 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c73a96fec76119cbe1739a1752e22e7acee25f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="processing-results-odbc"></a>处理结果 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  应用程序提交 SQL 语句之后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将得到的任何数据作为一个或多个结果集返回。 结果集是一组与查询条件匹配的行和列。 SELECT 语句、目录函数和某些存储过程可产生以表格格式供应用程序使用的结果集。 如果执行的 SQL 语句为存储过程、包含多个命令的批处理或包含关键字的 SELECT 语句，则会有多个要处理的结果集。  
  
 ODBC 目录函数也可以检索数据。 例如， [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)检索有关数据源中的列的数据。 这些结果集可以包含零行或更多行。  
  
 其他 SQL 语句（如 GRANT 或 REVOKE）不返回结果集。 对于这些语句返回的代码从**SQLExecute**或**SQLExecDirect**通常是语句的唯一指示成功。  
  
 每个 INSERT、UPDATE 和 DELETE 语句均返回一个仅包含受修改影响的行数的结果集。 此计数进行时应用程序可调用[SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)。 ODBC 3。*x*应用程序必须调用**SQLRowCount**若要检索的结果设置或[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)取消它。 如果应用程序执行的批处理或包含多个 INSERT、 UPDATE 或 DELETE 语句的存储的过程，必须使用处理中每个修改语句的结果集**SQLRowCount**或取消使用**SQLMoreResults**。 通过在批处理或存储过程中包含 SET NOCOUNT ON 语句，可以取消这些计数。  
  
 Transact-SQL 包括 SET NOCOUNT 语句。 当 NOCOUNT 选项设置上时，SQL Server 不返回语句所影响的行的计数和**SQLRowCount**返回 0。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序版本引入了特定于驱动程序的[SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)选项，SQL_SOPT_SS_NOCOUNT_STATUS，若要报告 NOCOUNT 选项是打开还是关闭。 随时**SQLRowCount**返回 0 时，应用程序应测试 SQL_SOPT_SS_NOCOUNT_STATUS。 如果 SQL_NC_ON 返回，从 0 的值**SQLRowCount**仅指示 SQL Server 未返回行计数。 如果返回 SQL_NC_OFF，这意味着 NOCOUNT 处于关闭状态和值从 0 **SQLRowCount**指示语句未影响任何行。 应用程序不应显示的值**SQLRowCount** SQL_SOPT_SS_NOCOUNT_STATUS 时 SQL_NC_OFF。 大型批处理或存储过程可能包含多个 SET NOCOUNT 语句，因此程序员不能假定 SQL_SOPT_SS_NOCOUNT_STATUS 保持不变。 每次都应测试选项**SQLRowCount**返回 0。  
  
 有若干其他 Transact-SQL 语句在消息中而不是在结果集中返回它们的值。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序收到这些消息时，它将返回 SQL_SUCCESS_WITH_INFO 让知道是否提供了信息性消息的应用程序。 然后，应用程序可以调用**SQLGetDiagRec**检索这些消息。 以这种方式工作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句如下：  
  
-   DBCC  
  
-   SET SHOWPLAN（在早期版本的 SQL Server 中提供）  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序返回 SQL_ERROR 上的 RAISERROR。 严重性为 11 或更高版本。 如果 RAISERROR 的严重性级别为 19 或更高，则连接也会断开。  
  
 为了处理 SQL 语句产生的结果集，应用程序会执行以下操作：  
  
-   确定结果集的特征。  
  
-   将列绑定到程序变量。  
  
-   检索单个值、整行值或多行值。  
  
-   进行测试以查看是否存在多个结果集，如果存在，则进行环回以确定新结果集的特征。  
  
 从数据源中检索行并将其返回给应用程序的过程称为提取。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [确定的特征的结果集 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [分配存储](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [提取结果数据](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [映射数据类型 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [数据类型用法](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [字符数据的自动转换](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [处理结果操作指南主题 &#40; ODBC &#41;](http://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
