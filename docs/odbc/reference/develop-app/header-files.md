---
description: 标头文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec8eede80f88f10e0b1ca43696e75dddec121ffe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476649"
---
# <a name="header-files"></a>标头文件
Sql .h 头文件包含核心 ODBC 接口一致性级别中的函数和功能的原型。 Sqltypes.h 头文件包含第1级和第2级 API 一致性级别中的函数和功能的原型。 Sqltypes 头文件包含 SQL 数据类型的类型定义和指示器。  
  
 标头文件都包含一个 **#define**ODBCVER，该应用程序或驱动程序可以设置为针对不同版本的 ODBC 进行编译。  
  
 为了与 ISO CLI 和开放式组 CLI 保持一致，头文件包含对 **SQLGetInfo**的调用中使用的信息类型的别名。 在下表中，列 "ODBC name" 指示 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)中的信息类型的 odbc 名称。 列 "标头文件中的别名" 指示在 ISO CLI 和开放组 CLI 中使用的名称。 这些清单名称的实际数值在 ODBC 和标准 Cli 中是相同的。 这些别名使符合标准的应用程序或驱动程序可以 *使用 ODBC 1.x* 标头文件进行编译。  
  
 这些别名包括 ODBC 名称中的缩写，使名称更易于理解。 "最大值" 扩展到 "最大值"、"LEN" 到 "LENGTH"、"MULT" 到 "多"、"OJ" 到 "OUTER_JOIN" 和 "TXN" 到 "TRANSACTION"。  
  
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
