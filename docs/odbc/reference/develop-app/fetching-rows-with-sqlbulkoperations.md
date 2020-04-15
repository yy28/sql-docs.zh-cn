---
title: 使用 SQLBulk 操作提取行 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305646"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 提取行
可以通过调用**SQLBulk 操作**将数据重新提取到行集中。 要提取的行由绑定书签列中的书签标识。 不提取值为SQL_COLUMN_IGNORE的列。  
  
 要使用**SQLBulk 操作**执行批量提取，应用程序执行以下操作：  
  
1.  检索并缓存要更新的所有行的书签。 如果有多个书签和按列绑定，则书签存储在数组中;如果使用多个书签和按列绑定，则书签将存储在数组中。如果有多个书签和逐行绑定，则书签存储在行结构数组中。  
  
2.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为要提取的行数，并将包含书签值的缓冲区或书签数组绑定到列 0。  
  
3.  根据需要设置每列的长度/指示器缓冲区中的值。 这是数据或SQL_NTS的字节长度，用于绑定到字符串缓冲区的列、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的任何列SQL_NULL_DATA。 应用程序将要设置为默认（如果存在）或 NULL（如果不存在）的列的长度/指示器缓冲区中的值设置为SQL_COLUMN_IGNORE。  
  
4.  调用**SQLBulk 操作**，*操作*参数设置为SQL_FETCH_BY_BOOKMARK。  
  
 应用程序无需使用行操作数组来防止对某些列执行操作。 应用程序通过仅将这些行的书签复制到绑定书签数组来选择要获取的行。
