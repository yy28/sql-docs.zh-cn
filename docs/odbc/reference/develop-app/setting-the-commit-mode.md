---
title: 设置提交模式 |Microsoft Docs
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
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094226"
---
# <a name="setting-the-commit-mode"></a>设置提交模式
应用程序指定具有 SQL_ATTR_AUTOCOMMIT 连接属性的事务模式。 默认情况下，ODBC 事务处于自动提交模式（除非不支持**SQLSetConnectAttr**和**SQLSetConnectOption** ，这是不可能的）。 从手动提交模式切换到自动提交模式会自动提交连接上的任何打开的事务。
