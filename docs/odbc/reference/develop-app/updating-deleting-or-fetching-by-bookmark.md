---
title: "更新、 删除或按书签提取 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 520d33c12b88fd6cd1c03cd7fd64ec254662ae3d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>更新、 删除或按书签提取
书签可以用于标识要在结果集，从结果设置，或从结果集行集的缓冲区中提取出来删除中更新数据。 这些操作通过调用执行**SQLBulkOperations**与*选项*SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK，或 SQL_FETCH_BY_BOOKMARK 的自变量。 在这些操作中使用书签存储在列 0 的行集缓冲区中。 在更新书签时，将更新结果集列的数据，以检索从行集缓冲区。 有关详细信息，请参阅[更新数据与 SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
