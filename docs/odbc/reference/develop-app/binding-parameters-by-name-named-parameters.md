---
title: "绑定参数按名称 （命名参数） |Microsoft 文档"
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
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 54298b1c08235452f5717888754569d55442a47a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="binding-parameters-by-name-named-parameters"></a>绑定参数按名称 （命名参数）
某些 Dbms 允许应用程序按名称而不是按位置在过程调用中指定的存储过程的参数。 此类参数称为*命名参数*。 ODBC 支持命名参数的使用。 ODBC 中, 命名的参数仅在对存储过程调用中使用，并且不在其他 SQL 语句中使用。  
  
 该驱动程序检查以确定是否可以使用名为使用参数 IPD SQL_DESC_UNNAMED 字段的值。 如果未设置为 SQL_UNNAMED SQL_DESC_UNNAMED，驱动程序会使用 IPD SQL_DESC_NAME 字段中名称来标识参数。 若要将该参数绑定，应用程序可以调用**SQLBindParameter**到指定的参数信息，然后可以调用**SQLSetDescField**设置 IPD SQL_DESC_NAME 字段。 当使用命名的参数时，在过程调用中的参数的顺序并不重要，忽略参数的记录数。  
  
 中的描述符记录编号和过程中的参数 %之间的关系是未命名的参数和命名的参数之间的差异。 当使用未命名的参数时，第一个参数标记都与参数描述符，反过来都与在过程调用中的第一个参数 （按创建顺序） 中的第一个记录。 当使用命名的参数时，第一个参数标记仍相关参数描述符，第一条记录，但不再存在的描述符记录编号和过程中的参数 %之间的关系。 命名的参数到过程的参数位置; 不使用描述符记录号的映射相反，映射到过程参数名称中的描述符记录名称。  
  
> [!NOTE]  
>  如果启用了自动填充的 IPD，驱动程序将填充描述符以便描述符记录的顺序将匹配在过程定义中，参数的顺序即使使用命名的参数。  
  
 如果使用命名的参数，则所有参数必须命名都为参数。 如果任何参数不是一个命名的参数，然后无参数 ca 命名参数。 如果没有命名的参数和未命名的参数的组合，则行为将驱动程序相关。  
  
 作为命名参数的示例，假设 SQL Server 存储过程已定义，如下所示：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此过程中，第一个参数， @title_id，默认值为 1。 应用程序可以使用下面的代码来调用此过程，以便它指定只有一个动态参数。 此参数是名称的命名的参数"@quote"。  
  
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
