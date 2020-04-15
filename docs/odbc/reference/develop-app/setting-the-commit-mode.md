---
title: 设置提交模式 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299817"
---
# <a name="setting-the-commit-mode"></a>设置提交模式
应用程序使用SQL_ATTR_AUTOCOMMIT连接属性指定事务模式。 默认情况下，ODBC 事务处于自动提交模式（除非不支持**SQLSetConnectAttr**和**SQLSetConnectOption，** 这不太可能）。 从手动提交模式切换到自动提交模式会自动提交连接上的任何未结事务。
