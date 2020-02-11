---
title: 按名称绑定参数（命名参数） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3fdd8d00bd6af5479079e66c1ca42f249e033d29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107643"
---
# <a name="binding-parameters-by-name-named-parameters"></a>按名称绑定参数（命名参数）
某些 Dbms 允许应用程序按名称（而不是在过程调用中的位置）来指定存储过程的参数。 此类参数称为*命名参数*。 ODBC 支持使用命名参数。 在 ODBC 中，命名参数仅用于对存储过程的调用，而不能用于其他 SQL 语句。  
  
 驱动程序将检查 IPD 的 SQL_DESC_UNNAMED 字段的值，以确定是否使用了命名参数。 如果 SQL_DESC_UNNAMED 未设置为 SQL_UNNAMED，驱动程序将使用 IPD 的 SQL_DESC_NAME 字段中的名称来标识参数。 若要绑定参数，应用程序可以调用**SQLBindParameter**来指定参数信息，然后可以调用**SQLSETDESCFIELD**来设置 IPD 的 SQL_DESC_NAME 字段。 使用命名参数时，过程调用中参数的顺序并不重要，并且忽略参数的记录号。  
  
 未命名参数和命名参数之间的区别在于描述符的记录编号与过程中的参数编号之间的关系。 使用未命名参数时，第一个参数标记与参数描述符中的第一条记录相关，后者又与过程调用中的第一个参数（在创建顺序中）相关。 使用命名参数时，第一个参数标记仍与参数描述符的第一条记录相关，但在此过程中，说明符的记录号和参数号之间的关系将不再存在。 命名参数不使用描述符记录号到过程参数位置的映射;相反，描述符记录名称将映射到过程参数名称。  
  
> [!NOTE]  
>  如果启用了 IPD 的自动填充，则驱动程序将填充描述符，以便描述符记录的顺序与过程定义中的参数顺序匹配，即使使用的是命名参数也是如此。  
  
 如果使用命名参数，则所有参数都必须为命名参数。 如果任何参数不是命名参数，则任何参数 ca 都不是命名参数。 如果存在命名参数和未命名参数的混合，则行为取决于驱动程序。  
  
 作为命名参数的示例，假设已按如下所示定义 SQL Server 存储过程：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此过程中，第一个参数@title_id的默认值为1。 应用程序可以使用以下代码调用此过程，以便仅指定一个动态参数。 此参数是名为 "\@quote" 的命名参数。  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
