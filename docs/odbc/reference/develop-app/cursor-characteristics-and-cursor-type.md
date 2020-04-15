---
title: 光标特征和光标类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8354fdabf6830780ec2d128492c86cc1edd582ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301624"
---
# <a name="cursor-characteristics-and-cursor-type"></a>游标特征和游标类型
应用程序可以指定游标的特征，而不是指定游标类型（仅转发、静态、键集驱动或动态）。 为此，应用程序在打开语句句柄上的游标之前选择游标的可滚动性（通过设置SQL_ATTR_CURSOR_SCROLLABLE语句属性）和灵敏度（通过设置SQL_ATTR_CURSOR_SENSITIVITY语句属性）。 然后，驱动程序选择最有效地提供应用程序请求的特征的游标类型。  
  
 每当应用程序设置SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_SCROLLABLE、SQL_ATTR_CURSOR_SENSITIVITY 或SQL_ATTR_CURSOR_TYPE的任何语句属性时，驱动程序都会对这组四个属性中的其他语句属性进行任何必需的更改，以便其值保持一致。 因此，当应用程序指定游标特征时，驱动程序可以基于此隐式选择更改指示游标类型的属性;因此，驱动程序可以更改指示游标类型的属性。当应用程序指定类型时，驱动程序可以更改任何其他属性，以便与所选类型的特征保持一致。 有关这些语句属性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。  
  
 设置语句属性以指定游标类型和游标特征的应用程序可能会获取游标，而游标不是满足应用程序要求的驱动程序上最有效的方法。  
  
 语句属性的隐式设置是驱动程序定义的，只不过它必须遵循以下规则：  
  
-   仅转发的游标永远不会滚动;请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)中SQL_ATTR_CURSOR_SCROLLABLE的定义。  
  
-   不敏感的游标永远不会被提升（因此它们并发是只读的）;这是基于他们在 ISO SQL 标准中对不敏感游标的定义。  
  
 因此，语句属性的隐式设置发生在下表中描述的情况下。  
  
|应用程序集属性到|隐式设置的其他属性|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY到SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITYSQL_INSENSITIVE。|  
|SQL_ATTR_CONCURRENCYSQL_CONCUR_LOCK、SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITYSQL_UNSPECIFIED或SQL_SENSITIVE，由驱动程序定义。 它永远不会设置为SQL_INSENSITIVE，因为不敏感的游标始终是只读的。|  
|SQL_ATTR_CURSOR_SCROLLABLE到SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLESQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE到驱动程序指定的SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或SQL_CURSOR_DYNAMIC。 它永远不会设置为SQL_CURSOR_FORWARD_ONLY。|  
|SQL_ATTR_CURSOR_SENSITIVITY到SQL_INSENSITIVE|SQL_ATTR_CONCURRENCYSQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPESQL_CURSOR_STATIC。|  
|SQL_ATTR_CURSOR_SENSITIVITY到SQL_SENSITIVE|SQL_ATTR_CONCURRENCY驱动程序指定的SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。 它永远不会设置为SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE驱动程序指定的SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN或SQL_CURSOR_DYNAMIC。|  
|SQL_ATTR_CURSOR_SENSITIVITY到SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY到驱动程序指定的SQL_CONCUR_READ_ONLY、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或SQL_CONCUR_VALUES。<br /><br /> SQL_ATTR_CURSOR_TYPE驱动程序指定的SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN或SQL_CURSOR_DYNAMIC。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLESQL_SCROLLABLE。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY到SQL_SENSITIVE。 （但前提是SQL_ATTR_CONCURRENCY不等于SQL_CONCUR_READ_ONLY。 可向上的动态游标始终对在其自己的事务中所做的更改敏感。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLESQL_NONSCROLLABLE。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLESQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITYSQL_UNSPECIFIED或SQL_SENSITIVE（根据驾驶员定义的条件，如果SQL_ATTR_CONCURRENCY未SQL_CONCUR_READ_ONLY）。|  
|SQL_ATTR_CURSOR_TYPE到SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLESQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY到SQL_INSENSITIVE（如果SQL_ATTR_CONCURRENCYSQL_CONCUR_READ_ONLY）。<br /><br /> SQL_ATTR_SENSITIVITYSQL_UNSPECIFIED或SQL_SENSITIVE（如果SQL_ATTR_CONCURRENCY不SQL_CONCUR_READ_ONLY）。|
