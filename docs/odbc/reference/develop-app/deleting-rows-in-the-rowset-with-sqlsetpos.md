---
description: 使用 SQLSetPos 删除行集中的行
title: 删除包含 SQLSetPos 的行集中的行 |Microsoft Docs
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
ms.openlocfilehash: 42b61aa9af15526420b6f2d4ef7e8c945e0da105
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476769"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 删除行集中的行
**SQLSetPos**的 delete 操作使数据源删除表中的一个或多个选定行。 若要删除 **SQLSetPos**的行，应用程序将调用 **SQLSetPos** ，并将 *操作* 设置 SQL_DELETE 为，并将 *RowNumber* 设置为要删除的行号。 如果 *RowNumber* 为0，则删除行集中的所有行。  
  
 **SQLSetPos**返回后，删除的行是当前行，其状态为 SQL_ROW_DELETED。 该行不能用于任何更进一步的定位操作，例如对 **SQLGetData** 或 **SQLSetPos**的调用。  
  
 当删除行集的所有行 (*RowNumber* 等于 0) 时，应用程序可以通过使用行操作数组阻止该驱动程序删除某些行，这与 **SQLSetPos**的更新操作的方式相同。  (参阅 [通过 SQLSetPos 更新行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md))   
  
 每个删除的行都应该是结果集中存在的行。 如果已通过提取填充应用程序缓冲区，并且已维护行状态数组，则在这些行位置的每个位置上的值不应为 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。
