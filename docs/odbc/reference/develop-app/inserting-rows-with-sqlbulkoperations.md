---
title: 插入行与 SQLBulkOperations |Microsoft 文档
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
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e501d05ea282690d8cc295c77927ab02989de5c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>与 SQLBulkOperations 插入行
插入数据与**SQLBulkOperations**类似于更新数据与**SQLBulkOperations**因为它使用的绑定应用程序缓冲区中的数据。  
  
 以便在新行中每列均具有一个值，所有绑定具有 SQL_COLUMN_IGNORE 长度/指示器值的列，并且未绑定的所有列必须接受 NULL 值或具有默认值。  
  
 要插入的行**SQLBulkOperations**，应用程序执行以下：  
  
1.  将该 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置要插入的行数并放置在绑定的应用程序缓冲区的新的数据值。 有关如何将长数据与发送信息**SQLBulkOperations**，请参阅[长数据、 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要在每个列的长度/指示器缓冲区设置的值。 这是数据或 sql_nts 以绑定到字符串缓冲区的字节长度的列绑定到二进制缓冲区和 SQL_NULL_DATA 任何要设置为 NULL 的列的数据的列的字节长度。 应用程序的这些列都可以设置为其默认值 （如果存在） 或 NULL （如果一个不使用） 到 SQL_COLUMN_IGNORE 长度/指示器缓冲区中设置的值。  
  
3.  调用**SQLBulkOperations**与*操作*参数设置为 SQL_ADD。  
  
 后**SQLBulkOperations**返回时，当前行保持不变。 如果绑定书签列 （列 0）， **SQLBulkOperations**返回行集缓冲区中插入的行的书签绑定到该列。
