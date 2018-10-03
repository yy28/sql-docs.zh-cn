---
title: 直接执行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73c061718dc326e43f72be369a28ad12726a3cab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603045"
---
# <a name="direct-execution-odbc"></a>直接执行 ODBC
直接执行是执行语句的最简单方法。 提交要执行该语句后，数据源将它编译成访问计划，然后执行该访问计划。  
  
 生成和运行时执行语句的通用应用程序通常使用直接执行。 例如，下面的代码生成的 SQL 语句，并执行它一次：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接执行最适合于执行一次的语句。 其主要缺点是每次执行时，分析 SQL 语句。 此外，应用程序无法检索有关创建语句 （如果有） 之前执行该语句; 后的结果集信息如果该语句已准备且在两个单独的步骤中执行，这是可能的。  
  
 执行语句，直接在应用程序执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。  
  
2.  调用**SQLExecDirect**并将其传递包含 SQL 语句的字符串。  
  
3.  当**SQLExecDirect**调用时，该驱动程序：  
  
    -   修改 SQL 语句，而无需分析语句; 使用数据源的 SQL 语法这包括替换中所述的转义序列[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 应用程序可以通过调用检索 SQL 语句的已修改的窗体**SQLNativeSql**。 如果设置 SQL_ATTR_NOSCAN 语句属性不替换转义序列。  
  
    -   检索当前的参数值，并根据需要将其转换。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。  
  
    -   将语句和已转换的参数值发送到数据源进行执行。  
  
    -   返回的任何错误。 其中包括序列化或状态诊断如 SQLSTATE 24000 （无效的游标状态）、 SQLSTATE 42000 （语法错误或访问冲突），如语法错误和语义错误，如 SQLSTATE 42S02 （基数为表或视图找不到）。
