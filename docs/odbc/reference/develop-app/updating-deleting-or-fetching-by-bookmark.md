---
title: 更新、 删除或提取按书签 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091627"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>按书签更新、删除或提取
可以使用书签来标识要更新在结果集中，删除从结果集中，则从结果集行集的缓冲区中提取数据。 这些操作通过调用执行**SQLBulkOperations**与*选项*SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK 的参数。 这些操作中使用书签存储在第 0 列的行集缓冲区中。 按书签更新时将更新结果集列的数据检索从行集缓冲区。 有关详细信息，请参阅[使用 SQLBulkOperations 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
