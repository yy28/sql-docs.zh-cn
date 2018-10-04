---
title: 使用 SQLBulkOperations 更新行的书签 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f0c59324542793301965c7d3555cf35ad40f5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653078"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 按书签更新行
通过书签，更新行时**SQLBulkOperations**使数据源进行更新的表的一个或多个行。 通过绑定的书签列中的书签标识行。 在应用程序缓冲区中的每个绑定列 （除非中列的长度/指示器缓冲区的值是 SQL_COLUMN_IGNORE） 使用数据更新的行。 未绑定的列将不会更新。  
  
 若要更新的行具有书签**SQLBulkOperations**，应用程序：  
  
1.  检索并缓存的更新的所有行的书签。 如果存在多个书签，并且使用按列绑定，书签将存储在数组中;如果存在多个书签，并且使用按行绑定，书签存储数组中的行结构。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为书签数并将绑定包含书签值或书签，到第 0 列的数组的缓冲区。  
  
3.  将新的数据值放在行集缓冲区中。 有关如何将长数据与发送的信息**SQLBulkOperations**，请参阅[长整型数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  根据需要在每个列的长度/指示器缓冲区中设置的值。 这是 sql_nts; 的数据的列绑定到字符串缓冲区绑定到二进制缓冲区和 SQL_NULL_DATA 的任何列设置为 NULL 的列的数据的字节长度的字节长度。  
  
5.  不会更新为 SQL_COLUMN_IGNORE 这些列的长度/指示器缓冲区中设置的值。 不过应用程序可以跳过此步骤，并重新发送的现有数据，这会导致效率低下，并将值发送到已被截断，在读取时的数据源的风险。  
  
6.  调用**SQLBulkOperations**与*操作*参数设置为 SQL_UPDATE_BY_BOOKMARK。  
  
 对于发送到数据源作为更新提供，每个行，应用程序缓冲区应具有有效的行数据。 如果应用程序缓冲区被提取，如果保持了行状态数组，并且如果某行的状态值为 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW，无效的数据可能会无意中发送到数据源。
