---
title: 环境、连接和语句属性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4606b4345cc52d1371649449890400e01dbc5f51
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114355"
---
# <a name="environment-connection-and-statement-attributes"></a>环境、连接和语句属性
ODBC 定义了与环境、连接或语句相关联的许多属性。  
  
 环境特性会影响整个环境，例如是否启用连接池。 环境特性是通过**SQLSetEnvAttr**设置的，并检索**SQLGetEnvAttr**。  
  
 连接属性分别影响每个连接，例如当尝试在超时之前连接到数据源时，驱动程序应等待的时间。连接属性通过**SQLSetConnectAttr**设置，并检索**SQLGetConnectAttr**。 有关连接属性的详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 语句属性分别影响每个语句，例如是否应异步执行语句。 语句特性是通过**SQLSetStmtAttr**设置的，并检索**SQLGetStmtAttr**。 有些语句特性是只读属性，无法设置。 例如，SQL_ATTR_ROW_NUMBER 语句特性用于检索游标中的当前行号，则为只读。 有关语句特性的详细信息，请参阅[语句特性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了 ODBC 定义的属性以外，驱动程序还可以定义自己的连接和语句属性。 驱动程序定义的属性必须注册到开放组，以确保两个驱动程序供应商不会将相同的整数值分配给不同的专有属性。 有关详细信息，请参阅[驱动程序特定的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有关属性的完整列表，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 大多数属性还在其影响的 ODBC 函数说明中进行了介绍。
