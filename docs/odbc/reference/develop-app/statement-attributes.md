---
title: 语句属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299640"
---
# <a name="statement-attributes"></a>语句属性
语句特性是语句的特征。 例如，是否使用书签以及与语句的结果集一起使用的游标类型是语句特性。  
  
 语句属性设置为**SQLSetStmtAttr** ，其当前设置通过**SQLGetStmtAttr**检索。 不要求应用程序设置任何语句属性;所有语句属性都具有默认值，其中一些属性是特定于驱动程序的。  
  
 如果可以设置语句特性，则依赖于特性本身。 在执行语句之前，必须设置 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 语句特性。 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_NOSCAN 语句特性可以随时设置，但在再次使用该语句之前不会应用。 SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS 和 SQL_ATTR_QUERY_TIMEOUT 语句特性可以随时设置，但它是特定于驱动程序的，无论是否在再次使用该语句之前应用这些特性。 可以随时设置其余的语句属性。  
  
> [!NOTE]  
>  通过调用**SQLSetConnectAttr**在连接级别设置语句属性的功能已在 ODBC 3 中弃用。*x*。 ODBC 3。*x*应用程序不应在连接级别设置语句属性。 ODBC 3。*x*驱动程序只有在使用 ODBC 2 时才需要支持此功能。*x*应用程序。 有关详细信息，请参阅附录 G：驱动程序准则中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)，以实现向后兼容性。  
>   
>  这种情况的一个例外是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，它们都是连接属性和语句属性，并且可以在连接级别或语句级别设置。  
>   
>  ODBC 3 中未引入任何语句属性。*x* （SQL_ATTR_METADATA_ID 除外）可以在连接级别设置。  
  
 有关详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。
