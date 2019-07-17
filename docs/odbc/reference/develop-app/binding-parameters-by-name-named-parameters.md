---
title: 绑定参数按名称 （命名参数） |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107643"
---
# <a name="binding-parameters-by-name-named-parameters"></a>按名称绑定参数（命名参数）
某些 Dbms 允许应用程序能够通过名称而不是按位置在过程调用中指定的存储过程的参数。 此类参数称为*命名参数*。 ODBC 支持使用命名参数。 在 ODBC 中，命名的参数仅在存储过程调用中使用和不能在其他 SQL 语句中使用。  
  
 该驱动程序检查的 SQL_DESC_UNNAMED 字段 IPD 以确定是否名为使用参数的值。 如果未设置为 SQL_UNNAMED SQL_DESC_UNNAMED，驱动程序会使用 IPD 的 SQL_DESC_NAME 字段中名称来标识参数。 若要将该参数的绑定，应用程序可以调用**SQLBindParameter**到指定的参数信息，然后可以调用**SQLSetDescField**设置 IPD SQL_DESC_NAME 字段。 当使用命名的参数时，过程调用中的参数的顺序并不重要，参数的记录号将被忽略。  
  
 未命名的参数和命名的参数之间的区别是中的描述符记录数和在该过程的参数编号之间的关系。 当使用未命名的参数时，第一个参数标记与参数描述符，又与在过程调用中的第一个参数 （按创建顺序） 中的第一个记录。 当使用命名的参数时，第一个参数标记仍然相关参数描述符，第一条记录，但不再存在的描述符记录数和在该过程的参数编号之间的关系。 命名的参数不使用过程参数位置; 到描述符记录号的映射相反，描述符记录名称映射到过程参数名称。  
  
> [!NOTE]  
>  如果启用了自动填充 IPD，驱动程序将填充描述符，以便描述符记录的顺序将匹配过程定义中参数的顺序即使使用命名的参数。  
  
 如果使用命名的参数，则所有参数必须被都命名参数。 如果任何参数不是一个命名的参数，none 参数 ca 被命名参数。 如果混合使用命名的参数和未命名的参数，则行为将驱动程序相关。  
  
 作为命名参数的示例，假设 SQL Server 存储过程已定义，如下所示：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此过程中，第一个参数， @title_id，默认值为 1。 应用程序可以使用以下代码以调用此过程，以便它指定只有一个动态参数。 此参数是一个命名的参数名"\@报价"。  
  
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
