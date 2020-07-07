---
title: 执行语句（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2680d1d65e051abfdcb22e239d9c97a9fc535745
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001396"
---
# <a name="executing-statements-odbc"></a>执行语句 (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序提供了在数据库中执行 SQL 语句的多种方法 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ：  
  
-   直接执行  
  
-   准备好的执行  
  
 直接执行涉及构建包含语句的字符串 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ，并使用**SQLExecDirect**函数提交它以执行执行。 准备好的执行即生成一个包含 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句的字符串，然后分两个阶段执行。 第一个阶段使用[SQLPrepare 函数](https://go.microsoft.com/fwlink/?LinkId=59360)函数分析和编译中的语句的执行计划 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 。 第二个阶段使用**SQLExecute**函数执行之前准备好的执行计划。 这节省了每次执行的分析和编译开销。 应用程序通常使用准备好的执行来重复执行相同的参数化 SQL 语句。  
  
 直接执行和准备好的执行都可以执行单个 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句或批处理 SQL 语句，也可以调用存储过程。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [直接执行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [准备好的执行](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [过程](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [语句的批处理](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [ISO 选项的作用](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;执行查询](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
