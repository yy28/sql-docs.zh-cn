---
title: 语句属性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fe7fd9cb7436470b8eba9984a4427a9e43e8490
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="statement-attributes"></a>语句属性
语句属性是语句的特性。 例如，若要使用书签和什么类型的光标若要使用的语句的结果集是否是语句属性。  
  
 与设置语句属性**SQLSetStmtAttr**和使用它们的当前设置检索**SQLGetStmtAttr**。 应用程序设置语句任何属性，则不要求语句的所有属性都有默认值，其中有一些特定于驱动程序。  
  
 当设置语句属性依赖于本身的属性。 在执行语句前，必须设置 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 语句属性。 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_NOSCAN 语句属性可以在任何时候设置，但会再次使用该语句后才会应用。 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS 和 SQL_ATTR_QUERY_TIMEOUT 语句属性可以设置任何时候，但它是特定于驱动程序是否它们之前要应用该语句会再次使用。 可以在任何时间设置的其余语句属性。  
  
> [!NOTE]  
>  能够在连接级别设置语句特性，通过调用**SQLSetConnectAttr** ODBC 3 中已弃用。*x*。 ODBC 3。*x*应用应永远不会将语句属性设置在连接级别。 ODBC 3。*x*驱动程序仅需要支持此功能，如果它们应使用 ODBC 2。*x*应用程序。 有关详细信息，请参阅[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)为了向后兼容的附录 g： 驱动程序准则中。  
>   
>  与此异常是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，而连接属性和语句属性都可以在连接级别或在语句级设置。  
>   
>  ODBC 3 中引入的语句属性均不项。*x* （除外 SQL_ATTR_METADATA_ID) 可以设置在连接级别。  
  
 有关详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。
