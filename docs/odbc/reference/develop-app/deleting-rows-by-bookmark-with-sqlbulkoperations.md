---
title: 删除使用 SQLBulkOperations 按书签的行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5895a106c389afe2d1979cf8d9c16e92f570538a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849455"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 按书签删除行
书签，通过删除行时**SQLBulkOperations**使数据源中删除一个或多个所选的表的行。 通过绑定的书签列中的书签标识行。  
  
 若要删除的行具有书签**SQLBulkOperations**，应用程序执行以下：  
  
1.  检索并缓存所有要删除的行的书签。 如果存在多个书签，并且使用按列绑定，书签将存储在数组中;如果存在多个书签，并且使用按行绑定，书签存储数组中的行结构。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为书签数并将绑定包含书签值或书签，到第 0 列的数组的缓冲区。  
  
3.  调用**SQLBulkOperations**与*操作*设置为 SQL_DELETE_BY_BOOKMARK。
