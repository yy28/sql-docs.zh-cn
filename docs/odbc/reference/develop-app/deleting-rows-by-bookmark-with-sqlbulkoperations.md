---
title: 使用 SQLBulkOperations 按书签删除行 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305958"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 按书签删除行
在按书签删除行时， **SQLBulkOperations**会使数据源删除表中的一个或多个选定行。 行由绑定书签列中的书签标识。  
  
 若要使用**SQLBulkOperations**按书签删除行，应用程序需要执行以下操作：  
  
1.  检索并缓存要删除的所有行的书签。 如果使用多个书签和逐列绑定，则书签存储在数组中;如果使用多个书签和按行绑定，书签将存储在行结构的数组中。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句特性设置为书签的数目，并将包含书签值的缓冲区和书签的数组绑定到列0。  
  
3.  调用**SQLBulkOperations** ，并将*操作*设置为 SQL_DELETE_BY_BOOKMARK。
