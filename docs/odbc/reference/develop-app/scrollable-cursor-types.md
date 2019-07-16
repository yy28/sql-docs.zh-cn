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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061627"
---
# <a name="scrollable-cursor-types"></a>可滚动游标类型
四种类型的可滚动游标是静态、 动态、 由键集驱动和混合。 静态游标检测少或没有更改，但相对比较便宜，来实现。 动态游标检测到的所有更改，但难以实现。 由键集驱动和混合游标介于二者之间，能检测到大部分变化，但在更少的开销比动态游标。  
  
 使用以下术语来定义每种类型的可滚动游标的特征：  
  
-   **自己的更新、 删除和插入。** 更新、 删除和插入通过游标，通过对调用进行**SQLBulkOperations**或**SQLSetPos**或使用定位更新或删除语句。  
  
-   **其他更新、 删除和插入。** 更新、 删除和不所做的光标，包括所做的其他操作在同一事务中插入、 所做通过其他事务和所做的其他应用程序。  
  
-   **成员身份。** 在结果集中的行集。  
  
-   **顺序。** 游标返回的行顺序。  
  
-   **值。** 在结果集中的每个行中的值。  
  
 有关如何更新、 删除和插入数据的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 静态游标](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 动态游标](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [由键集驱动的游标](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合游标](../../../odbc/reference/develop-app/mixed-cursors.md)
