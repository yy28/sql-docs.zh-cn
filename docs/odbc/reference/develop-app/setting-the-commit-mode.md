---
title: 将提交模式设置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efc999a3644a9146e7195f0bbbb07d130172d30d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445929"
---
# <a name="setting-the-commit-mode"></a>设置提交模式
应用程序使用 SQL_ATTR_AUTOCOMMIT 连接属性指定的事务模式。 默认情况下，ODBC 事务处于自动提交模式 (除非**SQLSetConnectAttr**并**SQLSetConnectOption**不受支持，这是不太可能)。 从手动提交模式切换到自动提交模式自动提交在连接上任何打开的事务。
