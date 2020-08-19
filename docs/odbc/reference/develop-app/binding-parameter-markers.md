---
description: 绑定参数标记
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 259faf84e0388f74662471583657da1fd95bb007
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476849"
---
# <a name="binding-parameter-markers"></a>绑定参数标记
应用程序通过调用 **SQLBindParameter**绑定参数。 **SQLBindParameter** 一次绑定一个参数。 在此应用程序中，应用程序指定了以下内容：  
  
-   参数编号。 参数在 SQL 语句中以递增参数顺序编号，以数字1开头。 虽然指定的参数号大于 SQL 语句中参数的数目是合法的，但在执行该语句时将忽略参数值。  
  
-   参数类型 (输入、输入/输出或输出) 。 除了过程调用中的参数，所有参数都是输入参数。 有关详细信息，请参阅本部分后面的 [过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)。  
  
-   绑定到参数的变量的 C 数据类型、地址和字节长度。 驱动程序必须能够将数据从 C 数据类型转换为 SQL 数据类型，否则将返回错误。 有关支持的转换的列表，请参阅附录 D：数据类型中的 [将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 。  
  
-   参数本身的 SQL 数据类型、精度和小数位数。  
  
-   长度/指示器缓冲区的地址。 它提供二进制或字符数据的字节长度，指定数据为 NULL，或指定将数据与 **SQLPutData**一起发送。 有关详细信息，请参阅 [使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 例如，以下代码将 *销售人员* 和 *CustID* 绑定到业务员和 CustID 列的参数。 由于 *销售人员* 包含字符数据（可变长度），因此代码指定 (11) 的 *销售人员* 的字节长度，并绑定 *SalesPersonLenOrInd* 以包含 *销售人员*的数据字节长度。 *CustID*不需要此信息，因为它包含固定长度的整数数据。  
  
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
  
 调用 **SQLBindParameter** 时，驱动程序会将此信息存储在语句的结构中。 执行语句时，它将使用该信息检索参数数据并将其发送到数据源。  
  
> [!NOTE]  
>  在 ODBC 1.0 中，参数与 **SQLSetParam**绑定。 驱动程序管理器根据应用程序和驱动程序使用的 ODBC 版本来映射 **SQLSetParam** 和 **SQLBindParameter**之间的调用。
