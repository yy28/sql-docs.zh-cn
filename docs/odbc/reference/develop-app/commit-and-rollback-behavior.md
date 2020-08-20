---
description: 提交和回滚行为
title: 提交和回滚行为 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 309d28dfb2c97fc8f3d8631edc3f0f7b9db85508
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494665"
---
# <a name="commit-and-rollback-behavior"></a>提交和回滚行为
服务器 Dbms 中的常见行为是在提交或回滚语句时关闭游标并放弃已准备的语句。 桌面数据库更有可能保持游标打开并保持预定义的语句。 有关详细信息，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项，以及 [事务对游标和预定义语句的影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。
