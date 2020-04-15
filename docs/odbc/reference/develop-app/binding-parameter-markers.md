---
title: 绑定参数标记 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be99bc884a8baa66f3d632ee4731985f0cc85732
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306388"
---
# <a name="binding-parameter-markers"></a>绑定参数标记
应用程序通过调用**SQLBind 参数**来绑定参数。 **SQLBind 参数**一次绑定一个参数。 使用它，应用程序指定以下内容：  
  
-   参数编号。 参数按 SQL 语句中增加参数顺序进行编号，从数字 1 开始。 虽然指定高于 SQL 语句中的参数数的参数编号是合法的，但在执行语句时将忽略参数值。  
  
-   参数类型（输入、输入/输出或输出）。 除过程调用中的参数外，所有参数都是输入参数。 有关详细信息，请参阅本部分后面的[过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)。  
  
-   绑定到参数的变量的 C 数据类型、地址和字节长度。 驱动程序必须能够将数据从 C 数据类型转换为 SQL 数据类型，否则将返回错误。 有关受支持的转化列表，请参阅附录 D：数据类型中[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
-   参数本身的 SQL 数据类型、精度和缩放。  
  
-   长度/指示器缓冲区的地址。 它提供二进制或字符数据的字节长度，指定数据为 NULL，或指定数据将与**SQLPutData**一起发送。 有关详细信息，请参阅[使用长度/指标值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 例如，以下代码将*销售人员*和*库斯特ID*绑定到销售人员和库斯特ID列的参数。 由于*SalesPerson*包含字符数据（即可变长度），因此代码指定*SalesPerson* （11） 的字节长度，并将*SalesPersonLenOrInd*绑定以包含*SalesPerson*中数据的字节长度。 *对于 CustID*来说，此信息是不需要的，因为它包含整数数据，数据长度固定。  
  
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
  
 调用**SQLBind参数**时，驱动程序将此信息存储在语句的结构中。 执行语句时，它使用信息检索参数数据并将其发送到数据源。  
  
> [!NOTE]  
>  在 ODBC 1.0 中，参数与**SQLSetParam**绑定。 驱动程序管理器映射**SQLSetParam**和**SQLBind参数**之间的调用，具体取决于应用程序和驱动程序使用的 ODBC 版本。
