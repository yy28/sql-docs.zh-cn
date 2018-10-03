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
manager: craigg
ms.openlocfilehash: c5af3cad39739c3b85a0c6298d682d8e75a5918d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765796"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>按书签更新、删除或提取
可以使用书签来标识要更新在结果集中，删除从结果集中，则从结果集行集的缓冲区中提取数据。 这些操作通过调用执行**SQLBulkOperations**与*选项*SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK 的参数。 这些操作中使用书签存储在第 0 列的行集缓冲区中。 按书签更新时将更新结果集列的数据检索从行集缓冲区。 有关详细信息，请参阅[使用 SQLBulkOperations 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
