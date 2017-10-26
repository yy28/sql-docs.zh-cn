---
title: "提交和回滚行为 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7bf7e756c77ceef96502fdacc078b4780f01ce86
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="commit-and-rollback-behavior"></a>提交和回滚行为
在服务器 Dbms 之间常见行为是关闭游标，然后提交或回滚一个语句时放弃已准备的语句。 桌面数据库很有可能，以保持游标处于打开状态并使已准备的语句。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明和[游标和准备语句上生效的事务](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).

