---
title: 使用 SQLSetPos 删除行 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940bcc3e2ee6a042394797d6038028cce64862f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305948"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 删除行集中的行
**SQLSetPos**的删除操作使数据源删除表的一个或多个选定行。 要删除**SQLSetPos 的**行，应用程序调用**SQLSetPos，***操作*设置为SQL_DELETE，*行号*设置为要删除的行数。 如果*RowNumber*为 0，则删除行集中的所有行。  
  
 **SQLSetPos**返回后，已删除的行是当前行，其状态为SQL_ROW_DELETED。 该行不能用于任何进一步的定位操作，例如对**SQLGetData**或**SQLSetPos**的调用。  
  
 删除行集的所有行（*行号*等于 0）时，应用程序可以阻止驱动程序使用行操作数组删除某些行，其方式与**SQLSetPos**的更新操作相同。 （请参阅[使用 SQLSetPos 更新行。](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
 每个删除的行都应该是结果集中存在的行。 如果应用程序缓冲区是通过提取填充的，并且已维护行状态数组，则不应SQL_ROW_DELETED、SQL_ROW_ERROR或SQL_ROW_NOROW这些行位置的值。
