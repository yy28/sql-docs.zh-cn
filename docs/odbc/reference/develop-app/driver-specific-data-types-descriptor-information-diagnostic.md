---
title: 特定于驱动程序的类型的数据，描述符的信息，诊断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa17a5552855916798c78e0e7d371b58e58a401e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046918"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性
驱动程序可以为以下分配特定于驱动程序的值：  
  
-   **SQL 数据类型指示符**在中使用这些*ParameterType*中**SQLBindParameter**然后在*数据类型*中**SQLGetTypeInfo**并返回**SQLColAttribute**， **SQLColumns**， **SQLDescribeCol**， **SQLGetTypeInfo**， **SQLDescribeParam**， **SQLProcedureColumns**，和**SQLSpecialColumns**。  
  
-   **描述符字段**在中使用这些*FieldIdentifier*中**SQLColAttribute**， **SQLGetDescField**，和**SQLSetDescField**.  
  
-   **诊断字段**在中使用这些*DiagIdentifier*中**SQLGetDiagField**并**SQLGetDiagRec**。  
  
-   **信息类型**在中使用这些*信息类型*中**SQLGetInfo**。  
  
-   **连接和语句属性**在中使用这些*特性*中**SQLGetConnectAttr**， **SQLGetStmtAttr**， **SQLSetConnectAttr**，并**SQLSetStmtAttr**。  
  
 对于每个这些项，有两个组的值： 值保留供 ODBC 和保留以供驱动程序的值。 实现特定于驱动程序的值之前, 的驱动程序编写器必须从 Open Group 请求每个特定于驱动程序的类型、 字段或属性的值。 新的驱动程序开发，使用下表中所述的范围。 如果使用了未知的值不在范围内，如下所述，ODBC 3.8 驱动程序管理器不会生成错误。 但是，如果将接收未知的值不在范围中的更高版本的驱动程序管理器可能会生成错误。  
  
 当任何这些值传递到 ODBC 函数时，驱动程序必须检查值是否有效。 驱动程序返回 SQLSTATE HYC00 （未实现的可选功能） 的适用于其他驱动程序的特定于驱动程序的值。  
  
 从 ODBC 3.8，驱动程序编写人员可以分配一个保留范围内的特定于驱动程序的属性。  
  
> [!NOTE]  
>  ODBC 3.8 驱动程序管理器不会验证该事务，也不会强制实施这些范围中的向后兼容性。 未来版本的驱动程序管理器可能会强制执行它们，但是。  
  
|属性类型|ODBC 数据类型|基本的特定于驱动程序的范围|特定于驱动程序的范围限制|ODBC 驱动程序特定值范围基常量|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 数据类型指示符|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述符字段|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|诊断字段|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|信息类型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|连接属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|语句属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  特定于驱动程序的数据类型、 描述符字段，诊断字段、 信息类型、 语句属性和连接属性必须驱动程序文档中所述。 当任何这些值传递到 ODBC 函数时，驱动程序必须检查值是否有效。 驱动程序返回 SQLSTATE HYC00 （未实现的可选功能） 的适用于其他驱动程序的特定于驱动程序的值。  
  
 定义基本的值以便于驱动程序开发。 例如，可以将驱动程序特定诊断属性定义采用以下格式：  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
