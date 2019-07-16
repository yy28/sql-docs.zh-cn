---
title: SQLGetInfo （文本文件驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 892fdabc319b1d495120cdce20d77f05cd232418
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898832"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo（文本文件驱动程序）
> [!NOTE]  
>  本主题提供了文本文件驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLGetInfo**支持 SQL_FILE_USAGE 信息类型。 返回的值是一个 16 位整数，指示如何驱动程序直接处理数据源中的文件：  
  
-   SQL_FILE_NOT_SUPPORTED-驱动程序不是单个层驱动程序。  
  
-   SQL_FILE_TABLE-单层驱动程序将视为表中的数据源的文件。  
  
-   SQL_FILE_QUALIFIER-单层驱动程序将视为一个限定符的数据源中的文件。  
  
 ODBC 驱动程序返回 SQL_FILE_TABLE Textdriver，因为每个文件是一个表。  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Version|版本号的格式|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW&#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
