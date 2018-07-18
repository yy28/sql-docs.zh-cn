---
title: 绑定参数 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 138df3eec425b0400acdcd5be538a8b490e7572b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410269"
---
# <a name="using-statement-parameters---binding-parameters"></a>使用语句参数-绑定参数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在执行 SQL 语句前，该语句中的每个参数标记都必须与应用程序中的某个变量关联或绑定到某个变量。 这是通过调用[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)函数。 **SQLBindParameter**描述程序变量 （地址、 C 数据类型等） 向驱动程序。 它还通过指示其序数值来标识参数标记，然后描述它所表示的 SQL 对象的特点（SQL 数据类型、精度等）。  
  
 在执行语句前，可以随时绑定或重新绑定参数标记。 直到发生下列事件之一时，参数绑定才会失效：  
  
-   调用[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)与*选项*参数设置为 SQL_RESET_PARAMS 释放绑定到语句句柄的所有参数。  
  
-   调用**SQLBindParameter**与*ParameterNumber*设置为绑定的参数标记的序号自动释放以前的绑定。  
  
 应用程序还可以将参数绑定到程序变量数组以成批处理 SQL 语句。 数组绑定有两种不同的类型：  
  
-   当每个参数绑定到自身的变量数组时，将完成按列绑定。  
  
     指定按列绑定通过调用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)与*特性*设置为 SQL_ATTR_PARAM_BIND_TYPE 和*ValuePtr*为 sql_param_bind_by_column，可以设置。  
  
-   当 SQL 语句中的所有参数作为一个单元绑定到包含这些参数的各个变量的结构数组时，将完成按行绑定。  
  
     指定按行绑定通过调用**SQLSetStmtAttr**与*特性*设置为 SQL_ATTR_PARAM_BIND_TYPE 和*ValuePtr*设置为结构持有锁的大小程序变量。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将字符或二进制字符串参数发送到服务器，它将填充这些值中指定的长度与**SQLBindParameter** *ColumnSize*参数。 如果 ODBC 2.x 应用程序指定为 0 *ColumnSize*，驱动程序来填充到数据类型的精度的参数值。 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器时，精度为 8000；连接到早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，精度为 255。 *ColumnSize*以字节为单位的变体列。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持为存储过程参数定义名称。 ODBC 3.5 还支持在调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程时使用的命名参数。 此支持可用于：  
  
-   调用存储过程，并向为该存储过程定义的参数的子集提供值。  
  
-   以不同于创建存储过程时指定的顺序指定应用程序中的参数。  
  
 使用时才支持命名的参数[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE**语句或 ODBC CALL 转义序列执行存储的过程。  
  
 如果**SQL_DESC_NAME**设置对于存储的过程参数，则在查询中的所有存储的过程参数还应设置**SQL_DESC_NAME**。  如果使用文字在存储的过程调用中，其中参数具有**SQL_DESC_NAME**设置，则这些文字应该使用格式*名称*=*值*，其中*名称*是存储的过程的参数名称 (例如， @p1)。 有关详细信息，请参阅[按名称 （命名参数） 绑定参数](http://go.microsoft.com/fwlink/?LinkId=167215)。  
  
## <a name="see-also"></a>请参阅  
 [使用语句参数](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
