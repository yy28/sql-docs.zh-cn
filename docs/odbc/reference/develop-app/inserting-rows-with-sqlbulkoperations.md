---
title: 使用 SQLBulk 操作插入行 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6fa384292f02026b8390aa92525144dce6f549b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300107"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入行
使用**SQLBulk 操作**插入数据类似于使用**SQLBulk 操作**更新数据，因为它使用绑定应用程序缓冲区中的数据。  
  
 因此，新行中的每个列都有一个值，所有长度/指示器值为 SQL_COLUMN_IGNORE 的绑定列都必须接受 NULL 值或具有默认值。  
  
 若要使用**SQLBulk 操作**插入行，应用程序执行以下操作：  
  
1.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为要插入的行数，并将新数据值放在绑定的应用程序缓冲区中。 有关如何使用**SQLBulk 操作**发送长数据的信息，请参阅[长数据和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要设置每列的长度/指示器缓冲区中的值。 这是数据或SQL_NTS的字节长度，用于绑定到字符串缓冲区的列、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的任何列SQL_NULL_DATA。 应用程序将要设置为默认（如果存在）或 NULL（如果不存在）的列的长度/指示器缓冲区中的值设置为SQL_COLUMN_IGNORE。  
  
3.  使用设置为SQL_ADD*的操作*参数调用**SQLBulk 操作**。  
  
 **SQLBulk 操作**返回后，当前行将保持不变。 如果绑定书签列（列**0），SQLBulk 操作**将返回绑定到该列的行集缓冲区中插入的行的书签。
