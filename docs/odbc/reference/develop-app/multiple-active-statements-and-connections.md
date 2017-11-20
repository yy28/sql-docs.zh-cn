---
title: "多个活动语句和连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97976df0d7f0a237abd2e67ed71202ba4d518f3b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="multiple-active-statements-and-connections"></a>多个活动语句和连接
某些驱动程序和 Dbms 限制语句和一次可以处于活动状态的连接的数。 这些数字可以是最小可为一个。 有关详细信息，请参阅中的 SQL_MAX_CONCURRENT_ACTIVITIES 和 SQL_MAX_DRIVER_CONNECTIONS 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明，和[语句处理](../../../odbc/reference/develop-app/statement-handles.md)和[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。

