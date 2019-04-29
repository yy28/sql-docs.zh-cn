---
title: 删除行集中的行使用 SQLSetPos |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78ee14838b467cfe6e555c97f1e74c65cccf98ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049827"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 删除行集中的行
删除操作的**SQLSetPos**使数据源中删除一个或多个所选的表的行。 若要删除的行**SQLSetPos**，应用程序调用**SQLSetPos**与*操作*设置为 SQL_DELETE 和*RowNumber*设置为若要删除的行数。 如果*RowNumber*为 0，则删除行集中的所有行。  
  
 之后**SQLSetPos**返回时，已删除的行是当前行，其状态为 SQL_ROW_DELETED。 行不能用于任何进一步定位操作，如调用**SQLGetData**或**SQLSetPos**。  
  
 删除行集的所有行时 (*RowNumber*等于 0)，该应用程序可以防止驱动程序中的更新操作时一样使用行操作数组，都删除某些行**SQLSetPos**. (请参阅[使用 SQLSetPos 更新行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。)  
  
 每个删除的行都应该是结果集中存在的行。 如果应用程序缓冲区被提取并保持了行状态数组，它在每个这些行位置的值不应 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。
