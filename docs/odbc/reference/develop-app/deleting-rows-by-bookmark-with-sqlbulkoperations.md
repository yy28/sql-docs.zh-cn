---
title: 使用 SQLBulk 操作按书签删除行 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b6a4c1b24ee276c86175392eb45ac5ce0aa45e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305958"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 按书签删除行
按书签删除行时 **，SQLBulk操作**使数据源删除表的一个或多个选定行。 行由绑定书签列中的书签标识。  
  
 要使用**SQLBulk 操作**通过书签删除行，应用程序执行以下操作：  
  
1.  检索并缓存要删除的所有行的书签。 如果有多个书签和按列绑定，则书签存储在数组中;如果使用多个书签和按列绑定，则书签将存储在数组中。如果有多个书签和逐行绑定，则书签存储在行结构数组中。  
  
2.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为书签数，并将包含书签值的缓冲区或书签数组绑定到列 0。  
  
3.  将**SQLBulk 操作***设置为SQL_DELETE_BY_BOOKMARK。*
