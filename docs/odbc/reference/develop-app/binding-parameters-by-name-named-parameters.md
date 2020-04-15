---
title: 按名称绑定参数（命名参数） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306368"
---
# <a name="binding-parameters-by-name-named-parameters"></a>按名称绑定参数（命名参数）
某些 DBMS 允许应用程序按名称而不是按过程调用中的位置指定存储过程的参数。 此类参数称为*命名参数*。 ODBC 支持使用命名参数。 在 ODBC 中，命名参数仅用于对存储过程的调用，不能在其他 SQL 语句中使用。  
  
 驱动程序检查 IPD SQL_DESC_UNNAMED字段的值，以确定是否使用了命名参数。 如果未将SQL_DESC_UNNAMED设置为SQL_UNNAMED，则驱动程序将使用 IPD SQL_DESC_NAME 字段中的名称来标识参数。 要绑定参数，应用程序可以调用**SQLBindparameter**来指定参数信息，然后可以调用**SQLSetDescField**来设置 IPD 的SQL_DESC_NAME字段。 使用命名参数时，过程调用中的参数顺序并不重要，并且忽略该参数的记录编号。  
  
 未命名参数和命名参数之间的差异在于描述符的记录编号与过程中参数编号之间的关系。 使用未命名参数时，第一个参数标记与参数描述符中的第一个记录相关，而该记录又与过程调用中的第一个参数（按创建顺序）相关。 使用命名参数时，第一个参数标记仍与参数描述符的第一个记录相关，但过程中的记录编号与参数编号之间的关系不再存在。 命名参数不使用描述符记录编号映射到过程参数位置;相反，描述符记录名称映射到过程参数名称。  
  
> [!NOTE]  
>  如果启用了 IPD 的自动填充，驱动程序将填充描述符，以便描述符记录的顺序将与过程定义中参数的顺序匹配，即使使用了命名参数也是如此。  
  
 如果使用命名参数，则必须命名所有参数。 如果任何参数不是命名参数，则没有命名参数。 如果存在命名参数和未命名参数的混合，则行为将依赖于驱动程序。  
  
 作为命名参数的示例，假设 SQL Server 存储过程的定义如下：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此过程中，第一个参数@title_id， 的默认值为 1。 应用程序可以使用以下代码调用此过程，以便它只指定一个动态参数。 此参数是名称为"报价"\@的命名参数。  
  
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
