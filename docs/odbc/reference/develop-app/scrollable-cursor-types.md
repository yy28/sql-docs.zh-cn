---
title: 可滚动游标类型 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304228"
---
# <a name="scrollable-cursor-types"></a>可滚动游标类型
四种类型的可滚动游标为静态、动态、键集驱动和混合。 静态游标只检测少量的更改，但要实现的成本相对较低。 动态游标检测所有更改，但实现成本高昂。 键集驱动游标和混合游标位于之间，检测大多数更改，但代价比动态游标更小。  
  
 以下术语用于定义每种类型的可滚动游标的特征：  
  
-   **自己的更新、删除和插入。** 通过调用**SQLBulkOperations**或**SQLSetPos**或者使用定位的 update 或 delete 语句，可以通过游标进行更新、删除和插入操作。  
  
-   **其他更新、删除和插入。** 不是由游标进行的更新、删除和插入操作，包括由同一事务中的其他操作所做的更改、通过其他事务进行的操作以及其他应用程序所做的更改。  
  
-   **成员身份.** 结果集中的行集。  
  
-   **为了.** 游标返回行的顺序。  
  
-   **分隔.** 结果集中每一行的值。  
  
 有关如何更新、删除和插入数据的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 静态游标](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 动态游标](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [由键集驱动的游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合游标](../../../odbc/reference/develop-app/mixed-cursors.md)
