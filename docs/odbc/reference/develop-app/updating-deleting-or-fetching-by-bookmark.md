---
title: 按书签更新、删除或提取 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e94a98bb577ef906afbb04539761fd07d15f772
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286147"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>按书签更新、删除或提取
书签可用于标识要在结果集中更新、从结果集中删除或从结果集提取到行集缓冲区的数据。 这些操作通过调用**SQLBulk 操作**执行，*选项*参数为 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK 或SQL_FETCH_BY_BOOKMARK。 这些操作中使用的书签存储在行集缓冲区的第 0 列中。 按书签更新时，将更新结果集列的数据从行集缓冲区检索到。 有关详细信息，请参阅使用[SQLBulk 操作更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
