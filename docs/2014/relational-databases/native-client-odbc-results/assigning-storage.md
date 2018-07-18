---
title: 将存储分配 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- column-wise binding [ODBC]
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLBindCol function
- storing data [ODBC]
- result sets [ODBC], storage
- SQL Server Native Client ODBC driver, data storage
- row-wise binding
- binding result sets [SQL Server Native Client]
- array binding
ms.assetid: 11c81955-5300-495f-925f-9256f2587b58
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc3ce031d7f59395ec54abe1c21276e9b4be9054
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426346"
---
# <a name="assigning-storage"></a>分配存储区
  应用程序可以在执行 SQL 语句之前或之后为结果分配存储区。 如果应用程序首先准备或执行 SQL 语句，则它可以在为结果分配存储区之前询问有关结果集的情况。 例如，如果结果集是未知的，则应用程序在为它们分配存储区之前必须先检索列数。  
  
 要将关联的数据列的存储，应用程序调用[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)并将其传递：  
  
-   数据将要转换成的数据类型。  
  
-   数据的输出缓冲区的地址。  
  
     应用程序必须分配该缓冲区，并且必须足够大以容纳采用转换后目标格式的数据。  
  
-   输出缓冲区的长度。  
  
     如果返回数据在 C 中有固定宽度（比如整数、实数或日期结构），则忽略该值。  
  
-   用于返回可用数据字节数的存储缓冲区的地址。  
  
 应用程序还可以将结果集列绑定到程序变量的数组，以支持分块提取结果集行。 有两种不同类型的数组绑定：  
  
-   当每个列绑定到自身的变量数组时，将完成按列绑定。  
  
     指定按列绑定通过调用[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)与*特性*设置为 SQL_ATTR_ROW_BIND_TYPE 和*ValuePtr*设置为 SQL_BIND_BY_COLUMN。 所有数组的元素个数必须相同。  
  
-   当 SQL 语句中的所有参数作为一个单元绑定到包含这些参数中各个变量的结构数组时，将完成按行绑定。  
  
     指定按行绑定通过调用**SQLSetStmtAttr**与*特性*设置为 SQL_ATTR_ROW_BIND_TYPE 和*ValuePtr*设置为结构持有锁的大小变量将接收结果集列。  
  
 应用程序还将 SQL_ATTR_ROW_ARRAY_SIZE 设置为列或行数组中的元素个数，并设置 SQL_ATTR_ROW_STATUS_PTR 和 SQL_ATTR_ROWS_FETCHED_PTR。  
  
## <a name="see-also"></a>请参阅  
 [处理结果&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
