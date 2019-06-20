---
title: 可滚动游标 |Microsoft Docs
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
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80be6994c7094b365bc24dd135bdda6ec4e561ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468383"
---
# <a name="scrollable-cursors"></a>可滚动游标
在现代基于屏幕的应用程序，在用户滚动向后和向前浏览数据。 对于此类应用程序，返回到之前提取的行是一个问题。 一种可能性是关闭和重新打开游标，然后提取行，直到光标达到所需的行。 另一种可能性是读取结果集、 其缓存到本地，并实现应用程序中滚动。 这两种可能性也仅使用较小的结果集和第二种可能性是难以实现。 更好的解决方案是使用*可滚动游标，* 这可以向后移动并转发结果集中。  
  
 一个*可滚动游标*通常用于现代基于屏幕的应用程序在用户滚动来回浏览数据。 但是，应用程序时应使用可滚动游标仅只进游标不会执行该作业，因为可滚动游标是通常比只进游标开销更大。  
  
 向后移动的能力会引发问题与只进游标不适用：可滚动游标应检测到以前提取行所做的更改？ 也就是说，它应检测更新、 删除和新插入的行？  
  
 由于当行检查以确定它们是否匹配该条件的结果集-的行集与匹配特定条件的定义不规定，因此会出现此问题也不会状态行是否必须包含相同的数据在提取每个时间。 以前省略使可滚动游标，以检测是否已插入或删除，而后者使它可以检测到更新后的数据行。  
  
 检测更改的能力有时很有用，有时不是。 例如，会计应用程序需要一个游标，将忽略所有更改;均衡丛书是光标显示了最新更改的情况下不可能。 另一方面，航空订票系统需要显示的数据; 的最新更改的游标而无需这样的游标，它必须不断地重新查询数据库以显示最新的航班可用性。  
  
 为了涵盖了不同的应用程序的需求，ODBC 定义了四种不同类型的可滚动游标。 这些游标改变在费用，以及在检测到的结果更改其功能设置。 请注意，是否可滚动游标可以检测到对行的更改，它只能检测到它们时它会尝试重新提取这些行;没有为数据源无法通知游标对当前提取行的更改的方法。 同时注意，更改的可见性还受事务隔离级别;有关详细信息，请参阅[事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 本部分包含以下主题。  
  
-   [可滚动游标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可滚动游标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相对和绝对滚动](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)
