---
title: 标题文件 |微软文档
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
ms.openlocfilehash: 62364d828e7b1f1ed8c70cae7ae1fc7dc3bc33fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300187"
---
# <a name="header-files"></a>标头文件
Sql.h 标头文件包含核心 ODBC 接口一致性级别中函数和功能的原型。 Sqlext.h 标头文件包含级别 1 和 2 级 API 一致性级别中函数和功能的原型。 Sqltype.h 标头文件包含 SQL 数据类型的类型定义和指示器。  
  
 标头文件都包含一个 **#define**ODBCVER，应用程序或驱动程序可以设置为为不同版本的 ODBC 编译。  
  
 要与 ISO CLI 和打开组 CLI 保持一致，标头文件包含调用**SQLGetInfo**中使用的信息类型的别名。 在下表中，"ODBC 名称"列指示[ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)中信息类型的 ODBC 名称。 "标题文件中的别名"一栏指示在 ISO CLI 和开放组 CLI 中使用的名称。 这些清单名称的实际数值在 ODBC 和标准 CL 中都是相同的。 这些别名使符合标准的应用程序或驱动程序能够使用 ODBC *3.x*标头文件进行编译。  
  
 这些别名包括 ODBC 名称中缩写的扩展，以便名称更容易理解。 "MAX"扩展到"最大"，"LEN"扩展到"长度"，"MULT"到"多"，"OJ"扩展到"OUTER_JOIN"，"TXN"扩展到"交易"。  
  
|ODBC 名称|标题文件中的别名|  
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
