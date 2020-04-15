---
title: 可滚动光标类型 |微软文档
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
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f29269ea209875a2e775cf8d523302fcb9a976
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304228"
---
# <a name="scrollable-cursor-types"></a>可滚动游标类型
四种类型的可滚动游标是静态的、动态的、按键集驱动的和混合的。 静态游标检测到很少或没有更改，但实现成本相对较低。 动态游标可检测所有更改，但实现成本高昂。 键集驱动和混合游标位于两者之间，检测大多数更改，但费用低于动态游标。  
  
 以下术语用于定义每种类型的可滚动游标的特征：  
  
-   **拥有更新、删除和插入。** 通过游标进行更新、删除和插入，无论是调用**SQLBulk 操作还是** **SQLSetPos，** 要么使用定位的更新或删除语句。  
  
-   **其他更新、删除和插入。** 更新、删除和插入游标未进行的更新、删除和插入，包括同一事务中其他操作所做的更新、删除和插入、通过其他事务进行的操作以及其他应用程序所做的操作。  
  
-   **会员。** 结果集中的行集。  
  
-   **以。** 游标返回行的顺序。  
  
-   **值。** 结果集中的每行中的值。  
  
 有关如何更新、删除和插入数据的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 静态游标](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 动态游标](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [由键集驱动的游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合游标](../../../odbc/reference/develop-app/mixed-cursors.md)
