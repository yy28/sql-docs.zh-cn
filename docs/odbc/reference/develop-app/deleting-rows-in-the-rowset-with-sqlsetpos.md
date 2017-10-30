---
title: "删除与 SQLSetPos 行集中的行 |Microsoft 文档"
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
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac33a8370cbd76a3dde43df68c12c9417fc78e07
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>删除与 SQLSetPos 行集中的行
删除操作的**SQLSetPos**使删除一个或多个选定的行的表的数据源。 若要删除的行**SQLSetPos**，应用程序调用**SQLSetPos**与*操作*设置为 SQL_DELETE 和*RowNumber*设置为要删除的行数。 如果*RowNumber*为 0，则删除在行集中的所有行。  
  
 后**SQLSetPos**返回时，已删除的行是当前行，并且其状态为 SQL_ROW_DELETED。 行不能在任何进一步定位操作，例如调用**SQLGetData**或**SQLSetPos**。  
  
 如果要删除的行集的所有行 (*RowNumber*等于 0)，应用程序可以阻止驱动程序用于更新操作的相同方式使用行操作数组中，都删除某些行**SQLSetPos**. (请参阅[SQLSetPos 使用更新的行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。)  
  
 每个删除的行都应该是结果集中存在的行。 如果应用程序缓冲区已填写通过提取并保持了行状态数组，它在每个这些行位置的值不应为 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。

