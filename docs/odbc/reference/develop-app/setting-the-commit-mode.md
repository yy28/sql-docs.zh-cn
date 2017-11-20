---
title: "将提交模式设置 |Microsoft 文档"
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
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d0c38d70b859b1fb986ebaa366a5396159a95da
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-commit-mode"></a>将提交模式设置
应用程序使用 SQL_ATTR_AUTOCOMMIT 连接属性指定的事务模式。 默认情况下，ODBC 事务处于自动提交模式 (除非**SQLSetConnectAttr**和**SQLSetConnectOption**不支持，这是不太可能)。 从手动提交模式切换到自动提交模式自动提交在连接上任何打开的事务。

