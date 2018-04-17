---
title: 使用 SQLBulkOperations 更新书签的行 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5a561fe33a54f31bcbe554dbf34525812c234e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新书签的行
书签，在更新某一行时**SQLBulkOperations**使更新的表的一个或多个行的数据源。 由绑定的书签列中的书签标识行。 使用数据的应用程序缓冲区 （除非列的长度/指示器缓冲区中的值是 SQL_COLUMN_IGNORE） 每个绑定列中的更新行。 未绑定的列将不会更新。  
  
 通过具有书签中更新行**SQLBulkOperations**，应用程序：  
  
1.  检索并缓存要更新的所有行的书签。 如果存在多个书签并且使用专用于列的绑定，书签将存储在数组; 例如：如果存在多个书签并且使用按行绑定，书签将存储在行结构的数组。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设为书签的数，并将绑定包含的书签值或书签，列 0 到数组的缓冲区。  
  
3.  位置的行集缓冲区中的新数据值。 有关如何将长数据与发送信息**SQLBulkOperations**，请参阅[长数据、 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  根据需要在每个列的长度/指示器缓冲区设置的值。 这是数据或 sql_nts 以绑定到字符串缓冲区的字节长度的列绑定到二进制缓冲区和 SQL_NULL_DATA 任何要设置为 NULL 的列的数据的列的字节长度。  
  
5.  中不会更新为 SQL_COLUMN_IGNORE 这些列的长度/指示器缓冲区设置的值。 尽管应用程序可以跳过此步骤，并重新发送现有数据，这将是效率低下，风险将值发送到被截断时它们已读取的数据源。  
  
6.  调用**SQLBulkOperations**与*操作*参数设置为 SQL_UPDATE_BY_BOOKMARK。  
  
 对于发送到数据源作为更新每一行，应用程序缓冲区应具有有效的行数据。 如果应用程序缓冲区已填写的提取，如果已保留的行状态数组，并且行的状态值是 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW，无效的数据可能无意中发送到数据源中。
