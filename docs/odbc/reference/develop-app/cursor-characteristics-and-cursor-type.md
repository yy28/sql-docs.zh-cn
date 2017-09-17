---
title: "光标特征和游标类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19a9e44523e1dc550b593bc83589177c03d8a842
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-characteristics-and-cursor-type"></a>光标特征和游标类型
应用程序可以指定而不是指定游标类型 （只进、 静态、 键集驱动的或动态） 游标的特性。 为此，应用程序选择光标的可滚动性 （通过设置 SQL_ATTR_CURSOR_SCROLLABLE 语句属性） 和大小写 （通过设置 SQL_ATTR_CURSOR_SENSITIVITY 语句属性） 在打开将光标放在该语句之前句柄。 然后将驱动程序选择的最有效地提供特征的光标类型请求的应用程序。  
  
 每当应用程序设置的任何语句属性 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_SCROLLABLE、 SQL_ATTR_CURSOR_SENSITIVITY 或 SQL_ATTR_CURSOR_TYPE，驱动程序，可以任何必要的更改到此组中的其他语句特性四个属性，以便它们的值保持一致。 因此，当应用程序指定游标特征，驱动程序可以更改属性，指示游标类型基于此隐式的选择;当应用程序指定一个类型，该驱动程序可以更改任何其他特性以与所选类型的特征保持一致。 有关这些语句特性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。  
  
 应用程序设置语句特性来指定游标类型和光标特征面临获取不是最低效的方法可在满足应用程序的要求该驱动程序上的游标。  
  
 语句特性的隐式设置是驱动程序定义的只不过它必须遵循下列规则：  
  
-   只进游标永远不会是可滚动;请参阅 SQL_ATTR_CURSOR_SCROLLABLE 中的定义[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
-   不敏感游标永远不会更新 （并且因此其并发是只读的）;这基于 ISO SQL 标准中的不敏感游标其定义。  
  
 因此，语句特性的隐式设置出现在下表中所述的情况。  
  
|应用程序将属性设置为|将隐式设置其他属性|  
|-----------------------------------|-------------------------------------|  
|到 SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY|到 SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。|  
|到 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY|SQL_ATTR_CURSOR_SENSITIVITY 到 SQL_UNSPECIFIED 或 SQL_SENSITIVE，定义由驱动程序。 它可以永远不会设置为 SQL_INSENSITIVE，因为不敏感游标始终是只读的。|  
|到 SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|到 SQL_CURSOR_FORWARD_ONLY SQL_ATTR_CURSOR_TYPE|  
|到 SQL_SCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|SQL_ATTR_CURSOR_TYPE 到 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，指定驱动程序。 它将永远不会设置为 SQL_CURSOR_FORWARD_ONLY。|  
|到 SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY|到 SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY。<br /><br /> 到 SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE。|  
|到 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY|SQL_ATTR_CONCURRENCY 到 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，指定驱动程序。 它将永远不会设置为 SQL_CONCUR_READ_ONLY。<br /><br /> SQL_ATTR_CURSOR_TYPE 到 SQL_CURSOR_FORWARD_ONLY、 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，指定驱动程序。|  
|到 SQL_UNSPECIFIED SQL_ATTR_CURSOR_SENSITIVITY|SQL_ATTR_CONCURRENCY 到 SQL_CONCUR_READ_ONLY、 SQL_CONCUR_LOCK、 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，指定驱动程序。<br /><br /> SQL_ATTR_CURSOR_TYPE 到 SQL_CURSOR_FORWARD_ONLY、 SQL_CURSOR_STATIC、 SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC，指定驱动程序。|  
|到 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE|到 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> 到 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY。 （但仅当 SQL_ATTR_CONCURRENCY 是否不等于 SQL_CONCUR_READ_ONLY。 可更新的动态游标始终是敏感到其自己的事务中所做的更改。）|  
|到 SQL_CURSOR_FORWARD_ONLY SQL_ATTR_CURSOR_TYPE|到 SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE。|  
|到 SQL_CURSOR_KEYSET_DRIVEN SQL_ATTR_CURSOR_TYPE|到 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY 到 SQL_UNSPECIFIED 或 SQL_SENSITIVE （根据驱动程序定义的条件，如果 SQL_ATTR_CONCURRENCY 不 SQL_CONCUR_READ_ONLY）。|  
|到 SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE|到 SQL_SCROLLABLE SQL_ATTR_SCROLLABLE。<br /><br /> SQL_ATTR_SENSITIVITY 到 SQL_INSENSITIVE （如果 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY）。<br /><br /> SQL_ATTR_SENSITIVITY 到 SQL_UNSPECIFIED 或 SQL_SENSITIVE （如果 SQL_ATTR_CONCURRENCY 没有 SQL_CONCUR_READ_ONLY）。|
