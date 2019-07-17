---
title: 环境、 连接和语句属性 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114355"
---
# <a name="environment-connection-and-statement-attributes"></a>环境、连接和语句属性
ODBC 定义的与环境、 连接或语句相关联的属性。  
  
 环境属性会影响整个环境中的，例如，是否启用连接池。 环境属性设置与**SQLSetEnvAttr**和与检索到**SQLGetEnvAttr**。  
  
 连接属性会影响每个连接单独，如驱动程序尝试连接到数据源在超时前应等待长时间。使用设置连接属性**SQLSetConnectAttr**和与检索到**SQLGetConnectAttr**。 有关连接属性的详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 语句属性影响每个语句分别，如是否应以异步方式执行一个语句。 使用设置语句属性**SQLSetStmtAttr**和与检索到**SQLGetStmtAttr**。 几个语句属性是只读属性，不能进行设置。 例如，用于检索游标中的当前行数的 SQL_ATTR_ROW_NUMBER 语句属性是只读的。 有关语句属性的详细信息，请参阅[语句属性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了由 ODBC 定义的特性，驱动程序可以定义其自己的连接和语句属性。 打开组，以确保两个驱动程序供应商现在将相同的整数值分配给不同的专有特性必须注册驱动程序定义的特性。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有关属性的完整列表，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，并[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 它们会影响的 ODBC 函数的说明中也描述了大多数属性。
