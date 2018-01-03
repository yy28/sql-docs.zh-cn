---
title: "调用 SQLCloseCursor |Microsoft 文档"
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
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c3870a36138fd55a2e404d38e28db327990ba1b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="calling-sqlclosecursor"></a>调用 SQLCloseCursor
因为**SQLCloseCursor**几乎相同**SQLFreeStmt**与 SQL_CLOSE，驱动程序管理器未映射此函数。 替换函数映射，以便现有 ODBC 2*.x*应用程序可以轻松地将移动到 ODBC 3。*x*通过使用新的函数。 此类移动，使此类应用程序，若要开始使用新的 ODBC 3 容易。*x*内模块化方式的条件代码的功能。 **SQLCloseCursor**不表示任何新功能。 应用程序不能通过将移动到的任何优势**SQLCloseCursor**从**SQLFreeStmt**与 SQL_CLOSE。
