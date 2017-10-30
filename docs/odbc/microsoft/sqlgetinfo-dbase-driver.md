---
title: "SQLGetInfo (dBASE 驱动程序) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetInfo
ms.assetid: 42ffdc9c-281b-4df5-ac6d-7b34f15ecd4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d79bc7a4f83c3c5eccc69bebc1e8f5c29ffe6ac3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-dbase-driver"></a>SQLGetInfo (dBASE 驱动程序)
> [!NOTE]  
>  本主题提供 dBASE 特定于驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLGetInfo**支持 SQL_FILE_USAGE 信息类型。 返回的值是一个 16 位整数，指示如何驱动程序直接处理数据源中的文件：  
  
-   SQL_FILE_NOT_SUPPORTED-驱动程序不是单层驱动程序。  
  
-   SQL_FILE_TABLE-单层驱动程序将视为表中的数据源的文件。  
  
-   SQL_FILE_QUALIFIER-单层驱动程序将视为限定符数据源中的文件。  
  
 ODBC 驱动程序返回 SQL_FILE_TABLE，由于每个文件是一个表。  
  
## <a name="sqlaltertable"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124;SQL_AT_DROP_COLUMN  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本号的格式|  
|----------|-------------|-------------------------------|  
|DBASE|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0|05.00.0000|  
  
## <a name="sqlddlindex"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124;SQL_QU_TABLE_DEFINITION &#124;SQL_QU_INDEX_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124;SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124;SQL_FN_TD_MINUTE &#124;SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124;SQL_FN_TD_WEEK &#124;SQL_FN_TD_YEAR

