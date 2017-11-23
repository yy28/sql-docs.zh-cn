---
title: "提交和回滚行为 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f8cecb32a5713f707a885f2004eef0fe13ae47a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="commit-and-rollback-behavior"></a>提交和回滚行为
在服务器 Dbms 之间常见行为是关闭游标，然后提交或回滚一个语句时放弃已准备的语句。 桌面数据库很有可能，以保持游标处于打开状态并使已准备的语句。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明和[游标和准备语句上生效的事务](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
