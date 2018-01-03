---
title: "可滚动游标 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1992b3fc6d6013859c1bdd46d119f633db46acfc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="scrollable-cursors"></a>可滚动游标
在现代基于屏幕的应用程序，在用户滚动向后和向前数据。 对于此类应用程序，将返回到以前读取的行是一个问题。 一种可能性是关闭并重新打开游标，然后提取行，直到光标达到所需的行。 另一种可能性是读取结果集，它以本地方式，缓存并实现应用程序中滚动。 这两种可能性也只能与小结果集和第二种可能性很难实现。 更好的解决方案是使用*可滚动游标，*可以向后移动并将其转发结果集中。  
  
 A*可滚动游标*通常用于在现代基于屏幕的应用程序在用户滚动来回到的数据。 但是，应用程序应可滚动游标仅当使用只进游标不会执行该作业，因为可滚动游标是通常比只进游标开销更大。  
  
 向后移动的能力引发不适用于只进游标的问题： 应可滚动游标检测到以前提取的行所做的更改？ 也就是说，它应检测更新、 删除和新插入的行？  
  
 因为结果的定义设置，将出现此问题-匹配特定条件的行集-不状态时检查行以确定是否匹配该条件，也不状态是否行必须包含相同的数据提取出来后每次。 以前省略使得可滚动游标来检测是否已插入或删除，而后者使它可以检测到更新的数据行。  
  
 检测更改的能力有时很有用，有时不是。 例如，会计应用程序需要将忽略所有更改的游标平衡丛书，则无法如果光标显示最新的更改。 另一方面，航空订票系统需要显示数据; 的最新更改的游标而无需这样的游标，它必须不断地重新查询数据库以显示最新的航班可用性。  
  
 为了满足不同应用程序的需求，ODBC 定义了四种不同类型的可滚动游标。 这些游标不同时处于支出和在其能够检测到的结果更改设置。 请注意，是否可滚动游标可以检测对行的更改，它可以仅会检测它们时它将尝试重新提取这些行;没有为此数据源通知对当前读取的行的更改的游标方法。 注意，更改的可见性还受事务隔离级别; 以及有关详细信息，请参阅[事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 本部分包含以下主题。  
  
-   [可滚动游标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可滚动游标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相对和绝对滚动](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)
