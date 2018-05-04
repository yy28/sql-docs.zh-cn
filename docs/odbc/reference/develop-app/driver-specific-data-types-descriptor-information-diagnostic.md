---
title: 特定于驱动程序的类型的数据，描述符，信息，诊断 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a28efa0a82135e871817c137af6bffd7608261e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性
驱动程序可以为以下分配特定于驱动程序的值：  
  
-   **SQL 数据类型指示器**中使用这些*ParameterType*中**SQLBindParameter**并在*DataType*中**SQLGetTypeInfo**以及返回**SQLColAttribute**， **SQLColumns**， **SQLDescribeCol**， **SQLGetTypeInfo**， **SQLDescribeParam**， **SQLProcedureColumns**，和**SQLSpecialColumns**。  
  
-   **描述符字段**中使用这些*FieldIdentifier*中**SQLColAttribute**， **SQLGetDescField**，和**SQLSetDescField**.  
  
-   **诊断字段**中使用这些*DiagIdentifier*中**SQLGetDiagField**和**SQLGetDiagRec**。  
  
-   **信息类型**中使用这些*信息类型*中**SQLGetInfo**。  
  
-   **连接和语句属性**中使用这些*属性*中**SQLGetConnectAttr**， **SQLGetStmtAttr**， **SQLSetConnectAttr**，和**SQLSetStmtAttr**。  
  
 为每个这些项，有两组值： 值保留供 ODBC 和驱动程序保留供的值。 在实现特定于驱动程序的值之前, 的驱动程序编写器必须从 Open Group 请求每个特定于驱动程序的类型、 字段或属性的值。 对于新的驱动程序开发，使用下表中所述的范围。 如果使用的未知的值不在范围内，如下所述的 ODBC 3.8 驱动程序管理器将不会生成错误。 但是，更高版本的驱动程序管理器可能会生成错误，如果未知的值接收，不在范围内。  
  
 当任何这些值传递到 ODBC 函数时，驱动程序必须检查值是否有效。 驱动程序返回 SQLSTATE HYC00 （未实现的可选功能） 的适用于其他驱动程序的特定于驱动程序的值。  
  
 从 ODBC 3.8 开始，则可以将驱动程序编写器分配一个保留范围中的特定于驱动程序的属性。  
  
> [!NOTE]  
>  ODBC 3.8 驱动程序管理器不会验证该事务，也不会强制实施这些范围为了向后兼容。 未来版本的驱动程序管理器可能会强制执行它们，但是。  
  
|属性类型|ODBC 数据类型|特定于驱动程序的范围基|特定于驱动程序的范围限制|ODBC 驱动程序的特定值范围基常量|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 数据类型指示器|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述符字段|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|诊断字段|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|信息类型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|连接属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|语句属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  特定于驱动程序的数据类型、 描述符字段、 诊断字段、 信息类型、 语句属性和连接属性必须驱动程序文档中所述。 当任何这些值传递到 ODBC 函数时，驱动程序必须检查值是否有效。 驱动程序返回 SQLSTATE HYC00 （未实现的可选功能） 的适用于其他驱动程序的特定于驱动程序的值。  
  
 定义的基的值以加快驱动程序的开发。 例如，可以采用以下格式定义驱动程序特定的诊断属性：  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
