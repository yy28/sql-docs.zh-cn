---
title: SQLGetInfo（悖论驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Paradox Driver
ms.assetid: 43aab762-68f4-4128-b8f5-8878ea5f1258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 354fa7f08797ee1fbfb057bfc2f2c192a8c5eddc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298567"
---
# <a name="sqlgetinfo-paradox-driver"></a>SQLGetInfo（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供特定于悖论驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLGetInfo**支持SQL_FILE_USAGE信息类型。 返回的值是一个 16 位整数，指示驱动程序如何处理数据源中的文件：  
  
-   SQL_FILE_NOT_SUPPORTED - 驱动程序不是单层驱动程序。  
  
-   SQL_FILE_TABLE - 单层驱动程序将数据源中的文件视为表。  
  
-   SQL_FILE_QUALIFIER - 单层驱动程序将数据源中的文件视为限定符。  
  
 ODBC 驱动程序返回SQL_FILE_TABLE因为每个文件都是一个表。  
  
## <a name="sql_alter_table"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN&#124;SQL_AT_DROP_COLUMN  
  
## <a name="sql_ddl_index"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本号的格式|  
|----------|-------------|-------------------------------|  
|悖论|3.x|03.00.0000|  
||4.x|04.00.0000|  
||5.x|05.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTSSQL_QU_TABLE_DEFINITION&#124;SQL_QU_INDEX_DEFINITION&#124;  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_MINUTE SQL_FN_TD_HOUR SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_DAYOFWEEK &#124;SQL_FN_TD_DAYOFMONTH&#124;&#124;&#124;&#124;SQL_FN_TD_SECONDSQL_FN_TD_WEEKSQL_FN_TD_WEEKSQL_FN_TD_SECOND&#124;&#124;&#124;SQL_FN_TD_DAYOFMONTH&#124;&#124;SQL_FN_TD_YEAR
