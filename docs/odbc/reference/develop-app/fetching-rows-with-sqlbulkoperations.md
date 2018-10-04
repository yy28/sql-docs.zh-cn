---
title: 使用 SQLBulkOperations 提取行 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a99592210ff315db026d60b8743d4a3bca13c969
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791535"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 提取行
可以通过调用到行集使用书签 refetched 数据**SQLBulkOperations。** 由绑定的书签列中的书签标识要提取的行。 不会获取 SQL_COLUMN_IGNORE 值的列。  
  
 若要执行大容量提取操作与**SQLBulkOperations**，应用程序执行以下：  
  
1.  检索并缓存的更新的所有行的书签。 如果存在多个书签，并且使用按列绑定，书签将存储在数组中;如果存在多个书签，并且使用按行绑定，书签存储数组中的行结构。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为要提取的行数，并将绑定包含书签值或书签，到第 0 列的数组的缓冲区。  
  
3.  根据需要在每个列的长度/指示器缓冲区中设置的值。 这是 sql_nts; 的数据的列绑定到字符串缓冲区绑定到二进制缓冲区和 SQL_NULL_DATA 的任何列设置为 NULL 的列的数据的字节长度的字节长度。 应用程序设置的值设置为其默认值 （如果存在） 的列或 SQL_COLUMN_IGNORE 到 NULL （如果一个不使用） 的长度/指示器缓冲区中。  
  
4.  调用**SQLBulkOperations**与*操作*参数设置为 SQL_FETCH_BY_BOOKMARK。  
  
 没有此应用程序使用行操作数组以防止操作无需执行对某些列。 应用程序选择想要通过将这些行的书签复制到绑定的书签数组提取的行。
