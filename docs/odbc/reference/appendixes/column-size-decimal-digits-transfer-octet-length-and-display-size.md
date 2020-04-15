---
title: 列大小、十进制数字、传输八点长度、显示大小 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55b8e9dd305764a89601e9ffd5a337e42a8d8db3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306568"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>列大小、十进制数字、传输八点长度和显示大小 - ODBC
数据类型的特征是其列（或参数）大小、小数位数、长度和显示大小。 以下 ODBC 函数返回 SQL 语句中的参数或数据源上的 SQL 数据类型的这些属性。 每个 ODBC 函数返回一组不同的这些属性，如下所示：  
  
-   **SQLDescribeCol**返回它描述的列的列大小和十进制数字。  
  
-   **SQLDescribeParam**返回它描述的参数的参数大小和十进制数字。 **SQLBind参数**在 SQL 语句中设置参数的参数大小和十进制数字。  
  
-   目录函数**SQLColumn、SQL****过程列**和**SQLGetTypeInfo**返回表中列、结果集或过程参数和数据源中数据类型的目录属性的属性。 **SQLColumn**返回指定表中（如基表、视图或系统表）中的列大小、小数位数和长度。 **SQL程序列**返回过程中列的大小、小数位数和长度。 **SQLGetTypeInfo**返回数据源上 SQL 数据类型的最大列大小以及最小和最大十进制数字。  
  
 这些函数为列或参数大小返回的值对应于 ODBC 2 中定义的"精度"。*x*. . 但是，这些值不一定对应于SQL_DESC_PRECISION或任何其他描述符字段中返回的值。 十进制数字也是如此，对应于 ODBC 2 中定义的"刻度"。*x*. . 它不一定对应于SQL_DESC_SCALE或任何其他描述符字段中返回的值，但来自不同的描述符字段，具体取决于数据类型。 有关详细信息，请参阅[列大小](../../../odbc/reference/appendixes/column-size.md)和[十进制数字](../../../odbc/reference/appendixes/decimal-digits.md)。  
  
 同样，传输八位字节长度的值不来自SQL_DESC_LENGTH。 它们来自所有字符和二进制类型的描述符字段的SQL_DESC_OCTET_LENGTH。 没有用于其他类型的此信息的描述符字段。  
  
 所有数据类型的显示大小值对应于单个描述符字段中的值，SQL_DESC_DISPLAY_SIZE。  
  
 描述符字段描述结果集的特征。 描述符字段在语句执行之前不包含有关数据的有效值。 另一方面 **，SQLColumn、SQL****程序列**和**SQLGetTypeInfo**返回的列大小、小数位数和显示大小的值返回数据源目录中存在的数据库对象的特征，如表列和数据类型。 同样，在其结果集中 **，SQLColAttribute**返回数据源中的列大小、小数位数和传输八位字节长度的列;这些值不一定与SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_OCTET_LENGTH描述符字段中的值相同。  
  
 有关这些描述符字段的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 相关主题：  
  
-   [列大小](../../../odbc/reference/appendixes/column-size.md)  
-   [十进制数字](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [传输八位字节长度](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [显示大小](../../../odbc/reference/appendixes/display-size.md)
