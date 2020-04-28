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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9972ab61f041385ae4ca616df093ae63ad7a47d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300383"
---
# <a name="updating-data-overview"></a>更新数据概述
应用程序可以通过执行 SQL 语句或通过调用**SQLSetPos**或**SQLBulkOperations**来更新数据。 **UPDATE**、 **DELETE**和**INSERT**语句直接对数据源执行操作，并且通常由驱动程序支持。 搜索的 update 和 delete 语句包含要更改的行的规范。 定位的 update 和 delete 语句和**SQLSetPos**通过游标对数据源执行操作，但不受广泛支持。  
  
 如果游标能检测到对结果集所做的更改，则此部分中所述的方法取决于游标的类型和实现方式。 只进游标不会重新访问行，因此将不会检测到任何更改。 有关可滚动游标能否检测更改的信息，请参阅可[滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 本部分包含以下主题。  
  
-   [UPDATE、DELETE 和 INSERT 语句](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [模拟定位更新和删除语句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [确定受影响的行数](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
