---
title: 特定于驱动程序的类型 - 数据、描述符、信息、诊断 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19bb2dd113fbeae871892ea510713c638c886e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305759"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性
驱动程序可以为以下分配特定于驱动程序的值：  
  
-   **SQL 数据类型指示器**这些在**SQLBind 参数**中的*参数类型*和**SQLGetTypeInfo**中的*数据类型*中使用，并由**SQLCol 属性**、SQL、SqlDescribeCol、SQLGetTypeinfo、SQL**描述栏****、SQL程序列**和**SQL 特殊列**返回。 **SQLColumns** **SQLDescribeCol** **SQLGetTypeInfo**  
  
-   **描述符字段**这些用于**在 SQLColattribute、SQLGetDescField**和**SQLSetDescField**中的*字段标识符*中。 **SQLGetDescField**  
  
-   **诊断字段**这些在**SQLGetDiagField**和**SQLGetDiagRec**中用于*Diag标识符*。  
  
-   **信息类型**这些在**SQLGetInfo**中*的信息类型*中使用。  
  
-   **连接和语句属性**这些在**SQLGetConnectAttr、SQLGetStmtAttr、SQLSetConnectAttr**和*Attribute***SQLSetStmtAttr**中使用。 **SQLGetStmtAttr** **SQLSetConnectAttr**  
  
 对于每个项目，有两组值：为 ODBC 保留的值，以及保留供驱动程序使用的值。 在实现特定于驱动程序的值之前，驱动程序编写器必须请求 Open Group 中每个特定于驱动程序的类型、字段或属性的值。 对于新的驱动程序开发，请使用下表中描述的范围。 如果使用的未知值不在下面描述的范围内，ODBC 3.8 驱动程序管理器不会生成错误。 但是，如果收到不在范围中的未知值，则驱动程序管理器的更高版本可能会生成错误。  
  
 当这些值中的任何一个传递给 ODBC 函数时，驱动程序必须检查该值是否有效。 驱动程序返回 SQLSTATE HYC00（未实现可选功能）以执行适用于其他驱动程序的特定于驱动程序的值。  
  
 从 ODBC 3.8 开始，驱动程序编写器可以在保留范围内分配特定于驱动程序的属性。  
  
> [!NOTE]  
>  ODBC 3.8 驱动程序管理器既不验证也不强制这些范围的向后兼容性。 但是，驱动程序管理器的未来版本可能会强制执行它们。  
  
|属性类型|ODBC 数据类型|特定于驱动程序的范围底座|特定于驱动程序的范围限制|用于特定于驱动程序的值范围基础的 ODBC 常量|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 数据类型指示器|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述符字段|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|诊断字段|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|信息类型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|连接属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|语句属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  驱动程序文档中必须描述特定于驱动程序的数据类型、描述符字段、诊断字段、信息类型、语句属性和连接属性。 当这些值中的任何一个传递给 ODBC 函数时，驱动程序必须检查该值是否有效。 驱动程序返回 SQLSTATE HYC00（未实现可选功能）以执行适用于其他驱动程序的特定于驱动程序的值。  
  
 定义基值是为了促进驱动程序的开发。 例如，驱动程序特定的诊断属性可以定义以下格式：  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
