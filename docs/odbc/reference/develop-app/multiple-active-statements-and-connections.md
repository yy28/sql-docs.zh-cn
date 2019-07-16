---
title: 多个活动语句和连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76b74ff748a62a401955e4ea4a995f507314124e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942829"
---
# <a name="multiple-active-statements-and-connections"></a>多个活动语句和连接
某些驱动程序和 Dbms 限制语句和一次可处于活动状态的连接的数。 这些数字可以最小可为其中一个。 有关详细信息，请参阅中的 SQL_MAX_CONCURRENT_ACTIVITIES 和 SQL_MAX_DRIVER_CONNECTIONS 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明，并[语句处理](../../../odbc/reference/develop-app/statement-handles.md)和[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
