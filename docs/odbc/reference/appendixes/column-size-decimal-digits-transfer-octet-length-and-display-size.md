---
title: 列大小、 十进制数字、 传输八位字节长度的显示大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8d7f1b8ec5647a34b09f0636fc8fcc2ad070f72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019241"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>列大小、 十进制数字、 传输八位字节长度和显示大小-ODBC
数据类型的特征体现在其列 （或参数） 的大小、 小数位数、 长度和显示大小。 以下 ODBC 函数返回对数据源中的 SQL 语句的参数或 SQL 数据类型的这些属性。 每个 ODBC 函数返回一组不同的这些属性，如下所示：  
  
-   **SQLDescribeCol**返回它所描述的列的大小和小数位数的列。  
  
-   **SQLDescribeParam**返回它所描述的参数的大小和小数位数的参数。 **SQLBindParameter** SQL 语句中设置的参数的参数的大小和小数位数。  
  
-   目录函数**SQLColumns**， **SQLProcedureColumns**，并**SQLGetTypeInfo**表、 结果集或过程参数中返回的列的属性和数据源中的数据类型的目录属性。 **SQLColumns** （例如基础表、 视图或系统表） 的指定表中返回的列的大小、 十进制数和列的长度。 **SQLProcedureColumns**在过程中返回的列的大小、 十进制数和列的长度。 **SQLGetTypeInfo**对数据源返回的最大列大小和 SQL 数据类型的最小值和最大十进制位数。  
  
 这些函数的列返回的值或参数的大小对应于"精度"作为 ODBC 2 中定义。*x*。 但是，在 SQL_DESC_PRECISION 或任何其他一个描述符字段中返回的值不一定对应值。 同样适用于十进制数字，它们分别对应于"规模"作为 ODBC 2 中定义。*x*。 它不一定对应中 SQL_DESC_SCALE 或任何其他的一个描述符字段，返回的值，但来自不同的描述符字段，具体取决于数据类型。 有关详细信息，请参阅[列的大小](../../../odbc/reference/appendixes/column-size.md)并[十进制数字](../../../odbc/reference/appendixes/decimal-digits.md)。  
  
 同样，传输八位字节长度的值不是来自 SQL_DESC_LENGTH。 它们来自的所有字符和二进制类型的描述符字段的 SQL_DESC_OCTET_LENGTH。 没有任何保存此信息对于其他类型的描述符字段。  
  
 所有数据类型的显示大小值对应于单个描述符字段，SQL_DESC_DISPLAY_SIZE 中的值。  
  
 描述符字段描述结果集的特征。 描述符字段不包含有关语句执行之前的数据有效的值。 列的值的大小，十进制数，并显示返回的大小**SQLColumns**， **SQLProcedureColumns**，并**SQLGetTypeInfo**另一方面只手，返回数据库对象，如表中的列和数据类型的特征的数据源的目录中存在。 同样，其结果集中， **SQLColAttribute**返回列的大小、 十进制数，以及传输八位字节长度的列的数据源; 这些值不一定是 SQL_DESC_PRECISION，SQL_ 中的值相同DESC_SCALE 和的 SQL_DESC_OCTET_LENGTH 描述符字段。  
  
 有关这些描述符字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 相关主题：  
  
-   [列大小](../../../odbc/reference/appendixes/column-size.md)  
-   [十进制数字](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [传输八位字节长度](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [显示大小](../../../odbc/reference/appendixes/display-size.md)
