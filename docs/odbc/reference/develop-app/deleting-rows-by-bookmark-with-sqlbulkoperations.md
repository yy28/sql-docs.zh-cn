---
title: "删除通过具有 SQLBulkOperations 书签的行 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db7e04c5bf76855afdb24676c905c5cccbc60cbc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>删除通过具有 SQLBulkOperations 书签的行
当删除行的书签的地方， **SQLBulkOperations**使删除一个或多个选定的行的表的数据源。 由绑定的书签列中的书签标识行。  
  
 删除行具有书签**SQLBulkOperations**，应用程序执行以下：  
  
1.  检索并缓存的要删除的所有行的书签。 如果存在多个书签并且使用专用于列的绑定，书签将存储在数组; 例如：如果存在多个书签并且使用按行绑定，书签将存储在行结构的数组。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设为书签的数，并将绑定包含的书签值或书签，列 0 到数组的缓冲区。  
  
3.  调用**SQLBulkOperations**与*操作*设置为 SQL_DELETE_BY_BOOKMARK。

