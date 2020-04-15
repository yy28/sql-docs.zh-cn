---
title: 使用 SQLBulk 操作按书签更新行 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283195"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 按书签更新行
按书签更新行时 **，SQLBulk操作**使数据源更新表的一行或多行。 行由绑定书签列中的书签标识。 行使用每个绑定列的应用程序缓冲区中的数据进行更新（除非列的长度/指标缓冲区中的值SQL_COLUMN_IGNORE）。 未绑定列将不会更新。  
  
 要使用**SQLBulk 操作**按书签更新行，应用程序：  
  
1.  检索并缓存要更新的所有行的书签。 如果有多个书签和按列绑定，则书签存储在数组中;如果使用多个书签和按列绑定，则书签将存储在数组中。如果有多个书签和逐行绑定，则书签存储在行结构数组中。  
  
2.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为书签数，并将包含书签值的缓冲区或书签数组绑定到列 0。  
  
3.  将新的数据值放在行集缓冲区中。 有关如何使用**SQLBulk 操作**发送长数据的信息，请参阅[长数据和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  根据需要设置每列的长度/指示器缓冲区中的值。 这是数据或SQL_NTS的字节长度，用于绑定到字符串缓冲区的列、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的任何列SQL_NULL_DATA。  
  
5.  设置不更新为SQL_COLUMN_IGNORE列的长度/指示器缓冲区中的值。 尽管应用程序可以跳过此步骤并重新发送现有数据，但这效率低下，并且可能会将值发送到读取时被截断的数据源。  
  
6.  调用**SQLBulk 操作**，*操作*参数设置为SQL_UPDATE_BY_BOOKMARK。  
  
 对于作为更新发送到数据源的每一行，应用程序缓冲区应具有有效的行数据。 如果通过提取填充应用程序缓冲区，则如果已维护行状态数组，并且行的状态值为SQL_ROW_DELETED、SQL_ROW_ERROR 或SQL_ROW_NOROW，则无效数据可能会无意中发送到数据源。
