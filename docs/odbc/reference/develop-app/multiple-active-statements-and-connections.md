---
title: "多个活动语句和连接 |Microsoft 文档"
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
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17be494898610bffba590548767a9d7c3e2915f8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="multiple-active-statements-and-connections"></a>多个活动语句和连接
某些驱动程序和 Dbms 限制语句和一次可以处于活动状态的连接的数。 这些数字可以是最小可为一个。 有关详细信息，请参阅中的 SQL_MAX_CONCURRENT_ACTIVITIES 和 SQL_MAX_DRIVER_CONNECTIONS 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明，和[语句处理](../../../odbc/reference/develop-app/statement-handles.md)和[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
