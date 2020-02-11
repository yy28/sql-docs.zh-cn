---
title: 提取 SQLBulkOperations 的行 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60b6673c4a6d618e52c78b48fe7307c20c8628f0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069844"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 提取行
可以通过调用 SQLBulkOperations，使用书签将数据制约到行集 **。** 要提取的行由绑定书签列中的书签标识。 不提取值为 SQL_COLUMN_IGNORE 的列。  
  
 若要通过**SQLBulkOperations**执行批量提取，应用程序执行以下操作：  
  
1.  检索并缓存要更新的所有行的书签。 如果使用多个书签和逐列绑定，则书签存储在数组中;如果使用多个书签和按行绑定，书签将存储在行结构的数组中。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句特性设置为要提取的行数，并将包含书签值或书签数组的缓冲区绑定到列0。  
  
3.  根据需要设置每列的长度/指示器缓冲区中的值。 这是绑定到字符串缓冲区的列的数据或 SQL_NTS 的字节长度、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的所有列的 SQL_NULL_DATA。 应用程序将设置为默认值（如果存在）的列的长度/指示器缓冲区中的值设置为默认值（如果存在）或 NULL （如果没有） SQL_COLUMN_IGNORE。  
  
4.  调用**SQLBulkOperations** ，并将*操作*参数设置为 SQL_FETCH_BY_BOOKMARK。  
  
 应用程序不需要使用行操作数组来阻止对某些列执行操作。 应用程序将选择要提取的行，方法是将这些行的书签仅复制到绑定书签数组中。
