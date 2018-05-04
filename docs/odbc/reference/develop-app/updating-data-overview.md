---
title: 更新数据概述 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce36f2467ce4da80f726c0f9370180422edddf49
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-overview"></a>更新数据概述
应用程序可以更新数据，通过执行 SQL 语句或通过调用**SQLSetPos**或**SQLBulkOperations**。 **更新**，**删除**，和**插入**语句直接在数据源上执行操作和驱动程序通常支持。 搜索 update 和 delete 语句包含要更改的行的说明。 定位更新和 delete 语句和**SQLSetPos**作用于数据源通过游标和不太受广泛支持。  
  
 游标是否可以检测到的结果集与在本部分中所述的方法所做的更改取决于游标和如何实现的类型。 只进游标不重新访问行，因此不会检测到的任何更改。 有关可滚动游标是否可以检测更改的信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 本部分包含以下主题。  
  
-   [UPDATE、DELETE 和 INSERT 语句](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [模拟定位更新和删除语句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
