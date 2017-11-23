---
title: "绑定参数标记 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea1c1ecd676c7a496f7856f0eb0b22b003183407
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="binding-parameter-markers"></a>绑定参数标记
应用程序的调用将参数绑定**SQLBindParameter**。 **SQLBindParameter**将一个参数绑定一次。 通过该对话框，指定以下应用程序：  
  
-   参数号。 参数是按在 SQL 语句中，从号 1 开始的递增参数顺序编号。 而是合法指定更高的参数数量时执行的语句，则将忽略超过的 SQL 语句中的参数数量，参数值。  
  
-   参数类型 （输入、 输入/输出，或输出）。 除了在过程调用中的参数，所有参数都是输入的参数。 有关详细信息，请参阅[过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)，本部分中更高版本。  
  
-   C 数据类型、 地址和字节长度的变量绑定到参数。 该驱动程序必须能够将数据从 C 数据类型转换为 SQL 数据类型或返回错误。 有关支持的转换的列表，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附录 d： 数据类型中。  
  
-   SQL 数据类型、 精度和小数位数本身。  
  
-   长度/指示器缓冲区的地址。 它提供的字节长度的二进制或字符数据、 指定数据为 NULL，或指定将与发送数据**SQLPutData**。 有关详细信息，请参阅[使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 例如，下面的代码绑定*销售人员*和*CustID*到销售和 CustID 列的参数。 因为*销售人员*包含字符数据，这是可变长度，该代码指定的字节长度的*销售人员*(11)，并将绑定*SalesPersonLenOrInd*到包含中的数据的字节长度*销售人员*。 此信息不需要*CustID*因为它包含的固定长度的整数数据。  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 当**SQLBindParameter**是调用，该驱动程序将存储此信息在该语句的结构。 当执行语句时，它使用的信息检索参数数据并将其发送到数据源。  
  
> [!NOTE]  
>  在 ODBC 1.0 中，参数绑定与**SQLSetParam**。 驱动程序管理器将调用之间映射**SQLSetParam**和**SQLBindParameter**，具体的 ODBC 应用程序和驱动程序使用的版本取决于。
