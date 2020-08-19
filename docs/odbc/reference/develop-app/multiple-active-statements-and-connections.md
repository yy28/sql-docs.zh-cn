---
description: 多个活动语句和连接
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56897dedbd1bf0d96dfa73f75a28db5f1ca46c43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429259"
---
# <a name="multiple-active-statements-and-connections"></a>多个活动语句和连接
某些驱动程序和 Dbms 限制一次可处于活动状态的语句和连接的数量。 这些数字可以小到一。 有关详细信息，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明中的 SQL_MAX_CONCURRENT_ACTIVITIES 和 SQL_MAX_DRIVER_CONNECTIONS 选项，以及 [语句句柄](../../../odbc/reference/develop-app/statement-handles.md) 和 [连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
