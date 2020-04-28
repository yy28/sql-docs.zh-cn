---
title: 使用 SQLBulkOperations 按书签更新行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c755297e8beadad92b5be81d78ca534bb96ecae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283195"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 按书签更新行
按书签更新行时， **SQLBulkOperations**使数据源更新表中的一行或多行。 行由绑定书签列中的书签标识。 将使用每个绑定列的应用程序缓冲区中的数据更新该行（在列的长度/指示器缓冲区中的值 SQL_COLUMN_IGNORE 时除外）。 未绑定列将不会更新。  
  
 若要使用**SQLBulkOperations**按书签更新行，应用程序：  
  
1.  检索并缓存要更新的所有行的书签。 如果使用多个书签和逐列绑定，则书签存储在数组中;如果使用多个书签和按行绑定，书签将存储在行结构的数组中。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句特性设置为书签的数目，并将包含书签值的缓冲区和书签的数组绑定到列0。  
  
3.  将新数据值置于行集缓冲区中。 有关如何通过**SQLBulkOperations**发送长数据的信息，请参阅[Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  根据需要设置每列的长度/指示器缓冲区中的值。 这是绑定到字符串缓冲区的列的数据或 SQL_NTS 的字节长度、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的所有列的 SQL_NULL_DATA。  
  
5.  设置那些不会更新为 SQL_COLUMN_IGNORE 的列的长度/指示器缓冲区中的值。 尽管应用程序可以跳过此步骤并重新发送现有数据，但这种情况很低效，将值发送到数据源（在读取时被截断）。  
  
6.  调用**SQLBulkOperations** ，并将*操作*参数设置为 SQL_UPDATE_BY_BOOKMARK。  
  
 对于作为更新发送到数据源的每一行，应用程序缓冲区应具有有效的行数据。 如果已通过提取填充应用程序缓冲区，并且已维护行状态数组，并且如果行的状态值为 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW，则可能会无意中将无效数据发送到数据源。
