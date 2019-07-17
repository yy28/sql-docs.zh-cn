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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c74f1a79ef79b682bc2900d671e07bbe34c4dbf5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107272"
---
# <a name="statement-attributes"></a>语句属性
语句属性是语句的特征。 例如，若要使用书签和什么类型的游标语句的结果与使用设置语句属性。  
  
 使用设置语句属性**SQLSetStmtAttr**并使用其当前设置检索**SQLGetStmtAttr**。 应用程序设置任何语句属性，则不要求所有语句属性都具有默认值，其中一些特定于驱动程序。  
  
 语句属性可以设置当取决于该属性本身。 在执行语句前，必须设置 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR 和 SQL_ATTR_USE_BOOKMARKS 语句属性。 Sql_attr_async_enable 设置和 SQL_ATTR_NOSCAN 语句属性可以在任何时间设置，但再次使用该语句后才会应用。 SQL_ATTR_MAX_LENGTH 和 SQL_ATTR_MAX_ROWS，sql_attr_query_timeout 时，可语句属性可以设置在任何时候，但它是特定于驱动程序它们应用之前再次使用该语句。 可以在任何时间设置的其余的语句属性。  
  
> [!NOTE]  
>  设置在连接级别的语句属性通过调用的能力**SQLSetConnectAttr** ODBC 3 中已弃用。*x*。 ODBC 3。*x*应用程序应永远不会在连接级别设置语句属性。 ODBC 3。*x*驱动程序仅需要支持此功能，如果他们应适用于 ODBC 2。*x*应用程序。 有关详细信息，请参阅[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中附录 g:为了向后兼容的驱动程序指南。  
>   
>  一种例外是 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句属性，可在连接级别或语句级别设置。  
>   
>  在 ODBC 3 中引入的语句属性均不项。*x* （除外 SQL_ATTR_METADATA_ID) 可以设置在连接级别。  
  
 有关详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。
