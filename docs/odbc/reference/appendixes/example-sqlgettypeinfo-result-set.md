---
title: 示例 SQLGetTypeInfo 结果集 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8264f1dfad8bff5d676cd4de8c8b9d7763b39b52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948754"
---
# <a name="example-sqlgettypeinfo-result-set"></a>示例 SQLGetTypeInfo 结果集
应用程序调用**SQLGetTypeInfo**来确定哪些数据类型支持的数据源以及这些数据类型的特征。 下表显示了示例结果集返回的**SQLGetTypeInfo**支持 SQL_CHAR、 SQL_LONGVARCHAR、 SQL_DECIMAL、 SQL_REAL、 SQL_DATETIME、 SQL_INTERVAL_YEAR 和 SQL_INTERVAL_DAY_TO_SECOND 为数据源。  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"char"|SQL_CHAR|255|"'"|"'"|"长度"|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<空 >|SQL_TRUE|  
|"decimal"|SQL_DECIMAL|28|\<空 >|\<空 >|"精度，<br />扩展"|SQL_TRUE|  
|"实际"|SQL_REAL|7|\<空 >|\<空 >|\<空 >|SQL_TRUE|  
|"datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<空 >|SQL_TRUE|  
|"到一年的时间间隔 YEAR()"|SQL_INTERVAL_YEAR|9|"'"|"'"|"精度"|SQL_TRUE|  
|"间隔 DAY() 到 FRACTION(5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"精度"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<空 >|SQL_FALSE|\<空 >|"char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<空 >|SQL_FALSE|\<空 >|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"decimal"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"实际"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<空 >|SQL_FALSE|\<空 >|"datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<空 >|SQL_FALSE|\<空 >|"到一年的时间间隔 YEAR()"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<空 >|SQL_FALSE|\<空 >|"间隔 DAY() 到 FRACTION(5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<空 >|\<空 >|SQL_CHAR|\<空 >|\<空 >|\<空 >|  
|**SQL_LONGVARCHAR**|\<空 >|\<空 >|SQL_LONGVARCHAR|\<空 >|\<空 >|\<空 >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<空 >|10|\<空 >|  
|**SQL_REAL**|\<空 >|\<空 >|SQL_REAL|\<空 >|10|\<空 >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<空 >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<空 >|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<空 >|9|
