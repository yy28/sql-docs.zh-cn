---
title: 游标特征和游标类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbef278f3f25b572ddc44e87d60b5cdcd33058c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043822"
---
# <a name="cursor-characteristics-and-cursor-type"></a>游标特征和游标类型
应用程序可以指定而不是指定游标类型 （只进、 静态、 由键集驱动或动态） 游标的特征。 若要执行此操作，该应用程序 （通过设置 SQL_ATTR_CURSOR_SCROLLABLE 语句属性） 的游标的可滚动性和敏感性 （通过设置 SQL_ATTR_CURSOR_SENSITIVITY 语句属性） 前选中打开的游标语句句柄。 然后，驱动程序选择的最有效地提供的特征的游标类型请求的应用程序。  
  
 每当应用程序设置的任何语句属性 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_SCROLLABLE、 SQL_ATTR_CURSOR_SENSITIVITY 或 SQL_ATTR_CURSOR_TYPE，则驱动程序将任何所需的更改对此组中的其他语句属性四个属性，以便其值保持一致。 因此，当应用程序指定游标特征时，驱动程序可以更改属性，用于指示游标类型基于此隐式选择;当应用程序指定一种类型，该驱动程序可以更改任何其他属性与所选类型的特征保持一致。 有关这些语句属性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。  
  
 设置语句属性来指定游标类型和游标特征的应用程序运行获取不是最高效的方法上的满足应用程序的要求该驱动程序提供的游标的风险。  
  
 隐式设置的语句属性是驱动程序定义的不同之处在于它必须遵循下列规则：  
  
-   只进游标从不是可滚动;请参阅的 SQL_ATTR_CURSOR_SCROLLABLE 中定义[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
-   不敏感游标永远不会是可更新 （和其并发因此是只读的）;这基于 ISO SQL 标准中的不敏感游标其定义。  
  
 因此，隐式设置的语句属性出现在下表中所述的情况。  
  
|应用程序将属性设置为|将隐式设置其他属性|  
|-----------------------------------|-------------------------------------|  
|Sql_attr_concurrency 设置为 SQL_CONCUR_READ_ONLY|为 SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。|  
|到 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES sql_attr_concurrency 设置|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE，驱动程序定义。 它可以永远不会设置为 SQL_INSENSITIVE，因为不敏感游标始终是只读的。|  
|为 SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|到 SQL_CURSOR_FORWARD_ONLY SQL_ATTR_CURSOR_TYPE|  
|为 SQL_SCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN，或 SQL_CURSOR_DYNAMIC，指定驱动程序。 它永远不会设置为 SQL_CURSOR_FORWARD_ONLY。|  
|为 SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY|Sql_attr_concurrency 设置为 SQL_CONCUR_READ_ONLY。<br /><br /> 到 SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE。|  
|为 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY|Sql_attr_concurrency 设置为 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，指定驱动程序。 它永远不会设置为 SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY、 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN，或 SQL_CURSOR_DYNAMIC，指定驱动程序。|  
|SQL_ATTR_CURSOR_SENSITIVITY 到 SQL_UNSPECIFIED|Sql_attr_concurrency 设置为 SQL_CONCUR_READ_ONLY、 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，指定驱动程序。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY、 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN，或 SQL_CURSOR_DYNAMIC，指定驱动程序。|  
|到 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE|为 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> 为 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。 （但仅当 SQL_ATTR_CONCURRENCY 不等于 SQL_CONCUR_READ_ONLY。 可更新动态游标始终是在它们自己的事务中所做的更改。）|  
|到 SQL_CURSOR_FORWARD_ONLY SQL_ATTR_CURSOR_TYPE|为 SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE。|  
|到 SQL_CURSOR_KEYSET_DRIVEN SQL_ATTR_CURSOR_TYPE|为 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （根据驱动程序定义的条件，如果 sql_attr_concurrency 设置不是 SQL_CONCUR_READ_ONLY）。|  
|到 SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE|为 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY 为 SQL_INSENSITIVE （如果 sql_attr_concurrency 设置为 SQL_CONCUR_READ_ONLY）。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （如果 SQL_ATTR_CONCURRENCY 没有 SQL_CONCUR_READ_ONLY）。|
