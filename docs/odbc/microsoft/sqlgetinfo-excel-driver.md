---
title: SQLGetInfo （Excel 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Excel Driver
ms.assetid: fed4aea2-6d3d-4199-a5db-3d033eb63927
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a96b135bbd8d44b82e645fac59ddea795666f3f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298577"
---
# <a name="sqlgetinfo-excel-driver"></a>SQLGetInfo（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLGetInfo**支持 SQL_FILE_USAGE 信息类型。 返回的值是一个16位整数，该整数指示驱动程序如何直接处理数据源中的文件：  
  
-   SQL_FILE_NOT_SUPPORTED-驱动程序不是单层驱动程序。  
  
-   SQL_FILE_TABLE-单层驱动程序以表的形式处理数据源中的文件。  
  
-   SQL_FILE_QUALIFIER-单层驱动程序将数据源中的文件视为限定符。  
  
 由于每个文件都是一个表，ODBC 驱动程序将返回 Microsoft.windowsazure.cloudconfigurationmanager Exceldriver SQL_FILE_TABLE。  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本号的格式|  
|----------|-------------|-------------------------------|  
|Microsoft Excel|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0/7。0|05.00.0000|  
||97/2000|08.00.0000|  
  
## <a name="sql_file_usage"></a>SQL_FILE_USAGE  
 SQL_FILE_TABLE （Excel 3.0/4.0）  
  
 SQL_FILE_CATALOG （Excel 5.0/7.0）  
  
## <a name="sql_max_char_literal_len"></a>SQL_MAX_CHAR_LITERAL_LEN  
 255（Excel 3.0/4.0/5.0/7.0）  
  
 65535（Excel 97）  
  
## <a name="sql_max_column_name_len"></a>SQL_MAX_COLUMN_NAME_LEN  
 30（Excel 3.0/4.0）  
  
 64（Excel 5.0/7.0/97）  
  
## <a name="sql_max_table_name_len"></a>SQL_MAX_TABLE_NAME_LEN  
 12（Excel 3.0/4.0）  
  
 31（Excel 5.0/7.0/97）  
  
## <a name="sql_catalog_name_separator"></a>SQL_CATALOG_NAME_SEPARATOR  
 "\\" （Excel 3.0/4.0）  
  
 "."（Excel 5.0/7.0/97）  
  
## <a name="sql_catalog_term"></a>SQL_CATALOG_TERM  
 "目录" （Excel 3.0/4.0）  
  
 "工作簿" （Excel 5.0/7.0/97）  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
