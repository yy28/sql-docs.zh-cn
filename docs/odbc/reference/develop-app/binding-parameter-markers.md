---
title: 绑定参数标记 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e625e01b9bf4771f18dd8e9807ab09100ca580c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107650"
---
# <a name="binding-parameter-markers"></a>绑定参数标记
应用程序将参数绑定通过调用**SQLBindParameter**。 **SQLBindParameter**将一个参数绑定一次。 使用它，该应用程序指定以下：  
  
-   参数数目。 参数是以参数按升序排列在 SQL 语句中，从数字 1 开始编号。 而是合法指定较高的参数数量时执行的语句，则将忽略的 SQL 语句中的参数数量，参数值。  
  
-   参数类型 （输入、 输入/输出或输出）。 除了在过程调用中的参数，所有参数都是输入的参数。 有关详细信息，请参阅[过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)，在本部分中更高版本。  
  
-   该变量的 C 数据类型、 地址和字节长度绑定到参数。 该驱动程序必须能够将数据从 C 数据类型转换到 SQL 数据类型或返回错误。 有关支持的转换的列表，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)中附录 d:数据类型。  
  
-   SQL 数据类型、 精度和小数位数参数本身。  
  
-   长度/指示器缓冲区的地址。 它提供了二进制或字符数据的字节长度，指定数据为 NULL，或指定的数据将发送具有**SQLPutData**。 有关详细信息，请参阅[使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 例如，下面的代码绑定*销售人员*并*CustID*到销售人员和 CustID 列的参数。 因为*销售人员*包含字符数据，这是可变长度，该代码指定的字节长度*销售人员*(11)，并将绑定*SalesPersonLenOrInd*到包含中的数据的字节长度*销售人员*。 此信息不是所需*CustID*因为它包含固定长度的整数数据。  
  
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
  
 当**SQLBindParameter**是调用，该驱动程序将此信息存储在该语句的结构。 该语句执行时，它使用的信息来检索参数数据并将其发送到数据源。  
  
> [!NOTE]  
>  在 ODBC 1.0 中，参数绑定与**SQLSetParam**。 驱动程序管理器将调用之间映射**SQLSetParam**并**SQLBindParameter**，取决于应用程序和驱动程序使用 ODBC 的版本。
