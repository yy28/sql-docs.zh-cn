---
description: 状态记录
title: 状态记录 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96d871814ac22e52eece4d6db7fff68fa2dacd48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482899"
---
# <a name="status-records"></a>状态记录
状态记录中的字段包含有关驱动程序管理器、驱动程序或数据源返回的特定错误或警告的信息，其中包括 SQLSTATE、本机错误号、诊断消息、列号和行号。 仅当函数返回 SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或 SQL_STILL_EXECUTING 时，才可以创建状态记录。 有关状态记录中字段的完整列表，请参阅 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 函数说明。  
  
 本部分包含以下主题。  
  
-   [状态记录的序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)
