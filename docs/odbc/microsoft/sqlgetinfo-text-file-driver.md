---
title: SQLGetInfo （文本文件驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9645b3148c3a3a391a65f158a4d8d28471239d36
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo （文本文件驱动程序）
> [!NOTE]  
>  本主题提供文本文件特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLGetInfo**支持 SQL_FILE_USAGE 信息类型。 返回的值是一个 16 位整数，指示如何驱动程序直接处理数据源中的文件：  
  
-   SQL_FILE_NOT_SUPPORTED-驱动程序不是单层驱动程序。  
  
-   SQL_FILE_TABLE-单层驱动程序将视为表中的数据源的文件。  
  
-   SQL_FILE_QUALIFIER-单层驱动程序将视为限定符数据源中的文件。  
  
 ODBC 驱动程序将返回 SQL_FILE_TABLE Textdriver，因为每个文件是一个表。  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本号的格式|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &AMP;#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &AMP;#124; SQL_FN_TD_CURTIME &AMP;#124; SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_NOW&AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
