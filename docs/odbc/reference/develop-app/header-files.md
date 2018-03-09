---
title: "标头文件 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 197c7ef28124fb1b1c52facbec541913330c69c5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="header-files"></a>标头文件
Sql.h 标头文件包含函数和核心 ODBC 接口一致性级别中的功能的原型。 Sqlext.h 标头文件包含为函数和中的级别 1 和级别 2 API 一致性级别的功能的原型。 Sqltypes.h 标头文件包含类型定义和 SQL 数据类型的指示符。  
  
 所有包含的标头文件**#define**，ODBCVER，应用程序或驱动程序可设置为针对不同版本的 ODBC 进行编译。  
  
 若要使用的 ISO CLI 和打开组 CLI 对齐，标头文件包含对的调用中使用的信息类型的别名**SQLGetInfo**。 下表中，在"ODBC name"的列指示中的信息类型的 ODBC 名称[ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)。 列"标头文件中的别名"指示 ISO CLI 和打开组 CLI 中使用的名称。 这些清单名称的实际数值是 ODBC 和标准 Cli 中相同。 这些别名启用符合标准的应用程序或驱动程序使用 ODBC 3 进行编译*.x*标头文件。  
  
 这些别名 ODBC 名称中包括的缩写的扩展，以便的名称是更易于理解。 "最大"扩展为"最大值"，"LEN"为"LENGTH"，"MULT"到"多个"，"OJ"到"OUTER_JOIN"和"TXN"到"事务"。  
  
|ODBC 名称|标头文件中的别名|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
