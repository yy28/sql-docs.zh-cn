---
title: 标头文件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e6d0806a7c3eabd1c6f4cd1836308eba99a6d5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656735"
---
# <a name="header-files"></a>头文件
Sql.h 标头文件包含的函数和核心 ODBC 接口一致性级别中的功能的原型。 Sqlext.h 标头文件包含的函数和级别 1 和级别 2 API 一致性级别中的功能的原型。 Sqltypes.h 头文件包含类型定义和 SQL 数据类型的指示符。  
  
 所有包含的标头文件 **#define**，ODBCVER，应用程序或驱动程序可设置为针对不同版本的 ODBC 进行编译。  
  
 若要使用 ISO CLI 和打开组 CLI 对齐，标头文件包含对的调用中使用的信息类型的别名**SQLGetInfo**。 下表中的列"ODBC name"指示 ODBC 中的信息类型的名称[ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)。 "标头文件中的别名"列指示在 ISO CLI 和打开组 CLI 中使用的名称。 这些清单名称的实际数值是 ODBC 和标准 Cli 中相同的。 这些别名启用符合标准的应用程序或驱动程序使用 ODBC 3 进行编译 *.x*标头文件。  
  
 这些别名 ODBC 名称中包含的缩写的扩展，以便更易于理解的名称是。 "最大"扩展为"最大值"，"LEN"为"长度"，"MULT"到"多"，"OJ"到"OUTER_JOIN"和"事务"到"事务"。  
  
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
