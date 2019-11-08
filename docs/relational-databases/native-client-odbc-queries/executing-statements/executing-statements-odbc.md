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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efd0b9ba46975512491dadccb5a44940af52ec28
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73791024"
---
# <a name="executing-statements-odbc"></a>执行语句 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序提供了在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中执行 SQL 语句的多种方法：  
  
-   直接执行  
  
-   准备好的执行  
  
 直接执行涉及构建包含 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句的字符串，并使用**SQLExecDirect**函数提交它以执行执行。 准备好的执行即生成一个包含 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句的字符串，然后分两个阶段执行。 第一个阶段使用[SQLPrepare 函数](https://go.microsoft.com/fwlink/?LinkId=59360)函数分析和编译 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]中语句的执行计划。 第二个阶段使用**SQLExecute**函数执行之前准备好的执行计划。 这节省了每次执行的分析和编译开销。 应用程序通常使用准备好的执行来重复执行相同的参数化 SQL 语句。  
  
 直接执行和准备好的执行都可以执行单个 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句或批处理 SQL 语句，也可以调用存储过程。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [直接执行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [准备好的执行](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [过程](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [语句的批处理](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [ISO 选项的作用](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行查询&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
