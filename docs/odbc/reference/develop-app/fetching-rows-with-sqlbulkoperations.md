---
title: 获取具有 SQLBulkOperations 行 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d3223ddb5c97fb35e57cb4e2344d6dae8b389d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>获取具有 SQLBulkOperations 行
可以通过调用转换为行，该集合使用书签 refetched 数据**SQLBulkOperations。** 由绑定的书签列中的书签标识要提取的行。 不会提取具有 SQL_COLUMN_IGNORE 值的列。  
  
 若要执行与大容量提取**SQLBulkOperations**，应用程序执行以下：  
  
1.  检索并缓存要更新的所有行的书签。 如果存在多个书签并且使用专用于列的绑定，书签将存储在数组; 例如：如果存在多个书签并且使用按行绑定，书签将存储在行结构的数组。  
  
2.  将该 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置要提取的行数，并将绑定包含的书签值或书签，列 0 到数组的缓冲区。  
  
3.  根据需要在每个列的长度/指示器缓冲区设置的值。 这是数据或 sql_nts 以绑定到字符串缓冲区的字节长度的列绑定到二进制缓冲区和 SQL_NULL_DATA 任何要设置为 NULL 的列的数据的列的字节长度。 应用程序的这些列都可以设置为其默认值 （如果存在） 或 NULL （如果一个不使用） 到 SQL_COLUMN_IGNORE 长度/指示器缓冲区中设置的值。  
  
4.  调用**SQLBulkOperations**与*操作*参数设置为 SQL_FETCH_BY_BOOKMARK。  
  
 没有此应用程序使用行操作数组以防止操作无需执行对某些列。 应用程序选择想要通过将仅书签的那些行复制到绑定的书签数组提取的行。
