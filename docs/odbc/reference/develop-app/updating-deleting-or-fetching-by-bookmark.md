---
title: 使用书签更新、删除或获取 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce43cb1d5563128e840aa3c0df26190524774a38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091627"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>按书签更新、删除或提取
书签可用于标识要在结果集中更新、从结果集删除或从结果集提取到行集缓冲区的数据。 这些操作通过使用 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK 的*选项*参数调用**SQLBulkOperations**来执行。 这些操作中使用的书签存储在行集缓冲区的第0列中。 如果按书签进行更新，则会从行集缓冲区中检索结果集列更新为的数据。 有关详细信息，请参阅[更新数据和 SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
