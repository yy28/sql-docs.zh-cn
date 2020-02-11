---
title: 游标特性和游标类型 |Microsoft Docs
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
ms.openlocfilehash: e8803e7827102f564be63454b0387df938064d84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002054"
---
# <a name="cursor-characteristics-and-cursor-type"></a>游标特征和游标类型
应用程序可以指定游标的特征，而不是指定游标类型（只进、静态、键集驱动或动态）。 为此，应用程序将选择游标的可滚动性（通过设置 SQL_ATTR_CURSOR_SCROLLABLE 语句特性）和敏感度（通过设置 SQL_ATTR_CURSOR_SENSITIVITY 语句特性），然后在该语句上打开游标柄. 然后，该驱动程序将选择最有效地提供应用程序所请求的特征的游标类型。  
  
 每当应用程序设置任意语句属性 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_SCROLLABLE、SQL_ATTR_CURSOR_SENSITIVITY 或 SQL_ATTR_CURSOR_TYPE 时，驱动程序就会对此组中的其他语句特性进行任何所需的更改。四个属性，使其值保持一致。 因此，当应用程序指定游标特性时，驱动程序可以根据此隐式选择更改指示游标类型的属性;当应用程序指定类型时，驱动程序可以更改任何其他属性，使其与所选类型的特征一致。 有关这些语句特性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。  
  
 设置语句属性以指定游标类型和游标特征的应用程序可在满足应用程序要求的该驱动程序上，使获得游标的风险不是最有效的方法。  
  
 语句特性的隐式设置是驱动程序定义的，但必须遵循以下规则：  
  
-   只进游标绝不能滚动;请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)中 SQL_ATTR_CURSOR_SCROLLABLE 的定义。  
  
-   不敏感游标永远不会更新（因此它们的并发性为只读）;这基于 ISO SQL 标准中不敏感游标的定义。  
  
 因此，在下表所述的情况下，将出现语句特性的隐式设置。  
  
|应用程序将属性设置为|隐式设置的其他属性|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE。|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES|根据驱动程序的定义 SQL_UNSPECIFIED 或 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。 永远不能设置为 SQL_INSENSITIVE，因为不敏感的游标始终是只读的。|  
|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，如驱动程序所指定。 它永远不会设置为 SQL_CURSOR_FORWARD_ONLY。|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC。|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，如驱动程序所指定。 它永远不会设置为 SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，如驱动程序所指定。|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，如驱动程序所指定。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，如驱动程序所指定。|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE。 （但仅当 SQL_ATTR_CONCURRENCY 不等于 SQL_CONCUR_READ_ONLY 时。 可更新动态游标始终对其自身事务中所做的更改敏感。）|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE。|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （根据驱动程序定义的条件，如果 SQL_ATTR_CONCURRENCY 不 SQL_CONCUR_READ_ONLY）。|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY SQL_INSENSITIVE （如果 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY）。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 或 SQL_SENSITIVE （如果 SQL_ATTR_CONCURRENCY 未 SQL_CONCUR_READ_ONLY）。|
