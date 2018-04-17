---
title: 可滚动游标类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a777db13717dcd2bda9e308e7d7df27c8edb237e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="scrollable-cursor-types"></a>可滚动游标类型
可滚动游标的四种类型是静态、 动态、 键集驱动和混合。 静态游标检测弱或根本没有更改，但相对比较便宜实现。 动态游标检测到的所有更改，但难以实现。 游标键集驱动的和混合游标位于之间，检测的大多数更改，但在更少的开销比动态游标。  
  
 以下术语用于定义每种类型的可滚动游标的特征：  
  
-   **拥有更新、 删除和插入。** 更新、 删除和插入通过游标，请通过调用进行**SQLBulkOperations**或**SQLSetPos**或使用定位更新或删除语句。  
  
-   **其他更新、 删除和插入。** 更新、 删除和不所做的光标，包括那些由同一个事务中的其他操作插入、 那些通过其他事务和所做的其他应用程序。  
  
-   **成员身份。** 在结果集中的行集。  
  
-   **顺序。** 将光标返回行的顺序。  
  
-   **值。** 结果集中的每一行中的值。  
  
 有关如何更新、 删除和插入数据的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 静态游标](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 动态游标](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [由键集驱动的游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合游标](../../../odbc/reference/develop-app/mixed-cursors.md)
