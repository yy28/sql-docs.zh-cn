---
title: 环境、连接和语句属性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86cecaf0b82c7b6d15b3f37262507d2cff0c3c10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300927"
---
# <a name="environment-connection-and-statement-attributes"></a>环境、连接和语句属性
ODBC 定义了许多与环境、连接或语句关联的属性。  
  
 环境属性会影响整个环境，例如是否启用了连接池。 环境属性使用**SQLSetEnvAttr**设置，并使用**SQLGetEnvAttr**检索。  
  
 连接属性会单独影响每个连接，例如驱动程序在尝试连接到数据源时应等待多长时间，然后再超时。连接属性使用**SQLSetConnectAttr**设置，并使用**SQLGetConnectAttr**检索。 有关连接属性的详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 语句属性单独影响每个语句，例如是否应异步执行语句。 语句属性使用**SQLSetStmtAttr**设置，并使用**SQLGetStmtAttr**检索。 少数语句属性是只读属性，无法设置。 例如，用于检索游标中当前行数SQL_ATTR_ROW_NUMBER语句属性是只读的。 有关语句属性的详细信息，请参阅[语句属性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了由 ODBC 定义的属性外，驱动程序还可以定义其自己的连接和语句属性。 驱动程序定义的属性必须注册到 Open Group，以确保两个驱动程序供应商不会将相同的整数值分配给不同的专有属性。 有关详细信息，请参阅[特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有关属性的完整列表，请参阅[SQLSetEnvAttr、SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)和[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 大多数属性在它们影响的 ODBC 函数的描述中也作了描述。
