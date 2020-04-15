---
title: 示例 SQLGetTypeInfo 结果集 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5cf62f8a95f4c91095c21a6d603317fe1f73500
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307008"
---
# <a name="example-sqlgettypeinfo-result-set"></a>示例 SQLGetTypeInfo 结果集
应用程序调用**SQLGetTypeInfo**以确定数据源支持哪些数据类型以及这些数据类型的特征。 下表显示了**SQLGetTypeInfo**为支持SQL_CHAR、SQL_LONGVARCHAR、SQL_DECIMAL、SQL_REAL、SQL_DATETIME、SQL_INTERVAL_YEAR和SQL_INTERVAL_DAY_TO_SECOND的数据源返回的示例结果集。  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"字符"|SQL_CHAR|255|"'"|"'"|"长度"|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<空>|SQL_TRUE|  
|"十进制"|SQL_DECIMAL|28|\<空>|\<空>|"精度，<br />比例"|SQL_TRUE|  
|"真实"|SQL_REAL|7|\<空>|\<空>|\<空>|SQL_TRUE|  
|"日期时间"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<空>|SQL_TRUE|  
|"间隔年（）到年"|SQL_INTERVAL_YEAR|9|"'"|"'"|"精度"|SQL_TRUE|  
|"间隔日（） 到分数（5）"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"精度"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<空>|SQL_FALSE|\<空>|"字符"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<空>|SQL_FALSE|\<空>|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"十进制"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"真实"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<空>|SQL_FALSE|\<空>|"日期时间"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<空>|SQL_FALSE|\<空>|"间隔年（）到年"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<空>|SQL_FALSE|\<空>|"间隔日（） 到分数（5）"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<空>|\<空>|SQL_CHAR|\<空>|\<空>|\<空>|  
|**SQL_LONGVARCHAR**|\<空>|\<空>|SQL_LONGVARCHAR|\<空>|\<空>|\<空>|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<空>|10|\<空>|  
|**SQL_REAL**|\<空>|\<空>|SQL_REAL|\<空>|10|\<空>|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<空>|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<空>|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<空>|9|
