---
title: 可滚动光标 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304208"
---
# <a name="scrollable-cursors"></a>可滚动游标
在现代基于屏幕的应用程序中，用户通过数据向前滚动。 对于此类应用程序，返回到以前提取的行是一个问题。 一种可能性是关闭并重新打开游标，然后提取行，直到光标到达所需的行。 另一种可能性是读取结果集，将其本地缓存，并在应用程序中实现滚动。 这两种可能性只有在结果集时才很良好，而后一种可能性很难实现。 更好的解决方案是使用*可滚动的游标，* 它可以在结果集中向后和向前移动。  
  
 *可滚动光标*通常用于基于屏幕的现代应用程序，用户在其中通过数据来回滚动。 但是，应用程序应仅在仅转发游标无法执行作业时才使用可滚动游标，因为可滚动游标通常比仅转发游标更昂贵。  
  
 向后移动的能力引发了一个不适用于仅向前游标的问题：可滚动游标是否应检测以前获取的行所做的更改？ 也就是说，它应该检测更新、删除和新插入的行吗？  
  
 出现此问题的原因是，结果集的定义（与特定条件匹配的行集）不说明何时检查行以查看它们是否与该条件匹配，也不说明每次提取行时是否必须包含相同的数据。 前一个遗漏使可滚动的游标能够检测行是否已插入或删除，而后者则使它们能够检测更新的数据。  
  
 检测更改的能力有时很有用，有时不是。 例如，会计应用程序需要忽略所有更改的游标;如果光标显示最新的更改，则无法平衡书籍。 另一方面，航空公司预订系统需要一个光标，用于显示数据的最新更改;如果没有这样的游标，它必须不断重新查询数据库以显示最新的飞行可用性。  
  
 为了满足不同应用的需求，ODBC 定义了四种不同类型的可滚动游标。 这些游标在费用和检测结果集更改的能力上都有所不同。 请注意，如果可滚动的游标可以检测行的更改，则它只能在尝试重新提取这些行时检测它们;数据源无法通知游标当前提取的行的更改。 另请注意，更改的可见性也受事务隔离级别控制;有关详细信息，请参阅[事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 本部分包含以下主题。  
  
-   [可滚动游标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可滚动游标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相对和绝对滚动](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)
