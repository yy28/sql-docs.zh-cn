---
title: 更新数据概述 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3edbd41bc5361d864abcc7d631a90521af98ef01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777825"
---
# <a name="updating-data-overview"></a>更新数据概述
应用程序可以更新数据，通过执行 SQL 语句或通过调用**SQLSetPos**或**SQLBulkOperations**。 **更新**，**删除**，和**插入**语句直接对数据源和驱动程序通常支持。 搜索 update 和 delete 语句包含要更改的行的规范。 定位 update 和 delete 语句和**SQLSetPos**作用于数据源通过游标并不太广泛支持。  
  
 游标是否可以检测到的结果集与在本部分中所述的方法所做的更改取决于游标和如何实现的类型。 只进游标不重新访问行，因此将不会检测任何更改。 有关是否可滚动游标可以检测到更改的信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 本部分包含以下主题。  
  
-   [UPDATE、DELETE 和 INSERT 语句](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [模拟定位更新和删除语句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
