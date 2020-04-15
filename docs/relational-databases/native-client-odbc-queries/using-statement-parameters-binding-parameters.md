---
title: 绑定参数 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01e179d2abc6ef786f94b6d7938f0e21938c5a59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304618"
---
# <a name="using-statement-parameters---binding-parameters"></a>使用语句参数 - 绑定参数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在执行 SQL 语句前，该语句中的每个参数标记都必须与应用程序中的某个变量关联或绑定到某个变量。 这是通过调用[SQLBind参数](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)函数来完成的。 **SQLBind参数**向驱动程序描述程序变量（地址、C 数据类型等）。 它还通过指示其序数值来标识参数标记，然后描述它所表示的 SQL 对象的特点（SQL 数据类型、精度等）。  
  
 在执行语句前，可以随时绑定或重新绑定参数标记。 直到发生下列事件之一时，参数绑定才会失效：  
  
-   使用*选项*参数设置为SQL_RESET_PARAMS释放绑定到语句句柄的所有参数的[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)的调用。  
  
-   对**SQLBind 参数**的调用，参数*编号*设置为绑定参数标记的定位，可自动释放以前的绑定。  
  
 应用程序还可以将参数绑定到程序变量数组以成批处理 SQL 语句。 数组绑定有两种不同的类型：  
  
-   当每个参数绑定到自身的变量数组时，将完成按列绑定。  
  
     按列方向绑定是通过调用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)来指定的，*其属性*设置为*SQL_ATTR_PARAM_BIND_TYPE，ValuePtr*设置为SQL_PARAM_BIND_BY_COLUMN。  
  
-   当 SQL 语句中的所有参数作为一个单元绑定到包含这些参数的各个变量的结构数组时，将完成按行绑定。  
  
     行绑定通过调用**SQLSetStmtAttr**来指定 *，其属性*设置为SQL_ATTR_PARAM_BIND_TYPE，ValuePtr 设置为保存程序变量的结构的大小。 *ValuePtr*  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序向服务器发送字符或二进制字符串参数时，它将值填充到**SQLBind 参数***列大小*参数中指定的长度。 如果 ODBC 2.x 应用程序为*ColumnSize*指定 0，则驱动程序将参数值填充到数据类型的精度。 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器时，精度为 8000；连接到早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，精度为 255。 *列大小*是变体列的字节。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持为存储过程参数定义名称。 ODBC 3.5 还支持在调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程时使用的命名参数。 此支持可用于：  
  
-   调用存储过程，并向为该存储过程定义的参数的子集提供值。  
  
-   以不同于创建存储过程时指定的顺序指定应用程序中的参数。  
  
 仅当使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE**语句或 ODBC CALL 转义序列执行存储过程时，才支持命名参数。  
  
 如果为存储过程参数设置了**SQL_DESC_NAME，** 则查询中的所有存储过程参数也应**SQL_DESC_NAME**设置。  如果在存储过程调用中使用文本（其中参数已**SQL_DESC_NAME**设置），则文本应使用格式*为"name*=*值*"，其中*名称*是存储过程参数名称（例如）。 @p1 有关详细信息，请参阅[按名称（命名参数）绑定参数](https://go.microsoft.com/fwlink/?LinkId=167215)。  
  
## <a name="see-also"></a>另请参阅  
 [使用语句参数](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
