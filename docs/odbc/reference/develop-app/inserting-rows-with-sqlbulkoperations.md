---
title: 使用 SQLBulkOperations 插入行 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b5dac8ae14f01dd464aab42eaed42480f1e715c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618835"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入行
将使用的数据插入**SQLBulkOperations**类似于更新数据与**SQLBulkOperations**因为它使用绑定的应用程序缓冲区中的数据。  
  
 以便在新行中的每个列具有值，所有绑定具有 SQL_COLUMN_IGNORE 长度/指示器值的列，所有未绑定的列必须接受 NULL 值或具有默认值。  
  
 要插入的行**SQLBulkOperations**，应用程序执行以下：  
  
1.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为要插入的行数并将新的数据值放在绑定的应用程序缓冲区中。 有关如何将长数据与发送的信息**SQLBulkOperations**，请参阅[长整型数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根据需要在每个列的长度/指示器缓冲区中设置的值。 这是 sql_nts; 的数据的列绑定到字符串缓冲区绑定到二进制缓冲区和 SQL_NULL_DATA 的任何列设置为 NULL 的列的数据的字节长度的字节长度。 应用程序设置的值设置为其默认值 （如果存在） 的列或 SQL_COLUMN_IGNORE 到 NULL （如果一个不使用） 的长度/指示器缓冲区中。  
  
3.  调用**SQLBulkOperations**与*操作*参数设置为 SQL_ADD。  
  
 之后**SQLBulkOperations**返回当前行是不变。 如果绑定书签列 （列 0）， **SQLBulkOperations**返回的行集缓冲区中插入行的书签绑定到该列。
