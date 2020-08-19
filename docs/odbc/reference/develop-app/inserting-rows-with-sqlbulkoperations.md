---
description: 使用 SQLBulkOperations 插入行
title: 用 SQLBulkOperations 插入行 |Microsoft Docs
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
ms.openlocfilehash: 36f04a393d2053389f823c33a55050f24dd87020
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424629"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入行
使用 **SQLBulkOperations** 插入数据类似于使用 **SQLBulkOperations** 更新数据，因为它使用绑定的应用程序缓冲区中的数据。  
  
 为了使新行中的每一列都具有值，所有绑定列的长度/指示器值都为 SQL_COLUMN_IGNORE 和所有未绑定列都必须接受 NULL 值或具有默认值。  
  
 若要在 **SQLBulkOperations**中插入行，应用程序需要执行以下操作：  
  
1.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句特性设置为要插入的行数，并将新的数据值放入绑定应用程序缓冲区。 有关如何通过 **SQLBulkOperations**发送长数据的信息，请参阅 [Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要设置每列的长度/指示器缓冲区中的值。 这是绑定到字符串缓冲区的列的数据或 SQL_NTS 的字节长度、绑定到二进制缓冲区的列的数据字节长度，以及要设置为 NULL 的所有列的 SQL_NULL_DATA。 应用程序将设置为默认 (的列的长度/指示器缓冲区中的值（如果) 存在），如果不) SQL_COLUMN_IGNORE，则设置为 NULL (。  
  
3.  调用 **SQLBulkOperations** ，并将 *操作* 参数设置为 SQL_ADD。  
  
 **SQLBulkOperations**返回后，当前行保持不变。 如果 "书签" 列 ("列 0) " 绑定 "，则 **SQLBulkOperations** 将返回绑定到该列的行集缓冲区中插入行的书签。
