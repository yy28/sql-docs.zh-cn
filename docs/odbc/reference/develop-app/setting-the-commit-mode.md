---
title: 将提交模式设置 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6d56a85716d88658c6e365484136460f7cce04b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910532"
---
# <a name="setting-the-commit-mode"></a>将提交模式设置
应用程序使用 SQL_ATTR_AUTOCOMMIT 连接属性指定的事务模式。 默认情况下，ODBC 事务处于自动提交模式 (除非**SQLSetConnectAttr**和**SQLSetConnectOption**不支持，这是不太可能)。 从手动提交模式切换到自动提交模式自动提交在连接上任何打开的事务。
