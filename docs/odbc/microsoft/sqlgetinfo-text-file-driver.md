---
title: SQLGetInfo（文本文件驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09ca2e42e20a6f314de3b68fe5d5b143f41269c3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298498"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLGetInfo**支持SQL_FILE_USAGE信息类型。 返回的值是一个 16 位整数，指示驱动程序如何处理数据源中的文件：  
  
-   SQL_FILE_NOT_SUPPORTED - 驱动程序不是单层驱动程序。  
  
-   SQL_FILE_TABLE - 单层驱动程序将数据源中的文件视为表。  
  
-   SQL_FILE_QUALIFIER - 单层驱动程序将数据源中的文件视为限定符。  
  
 ODBC 驱动程序返回文本驱动程序的SQL_FILE_TABLE，因为每个文件都是一个表。  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本号的格式|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS&#124;SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE SQL_FN_TD_WEEK SQL_FN_TD_SECOND SQL_FN_TD_NOW SQL_FN_TD_MONTH &#124; SQL_FN_TD_MINUTE SQL_FN_TD_HOUR &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_DAYOFMONTH &#124;&#124;SQL_FN_TD_CURTIMESQL_FN_TD_DAYOFWEEKSQL_FN_TD_DAYOFWEEK&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124; &#124;SQL_FN_TD_YEAR
