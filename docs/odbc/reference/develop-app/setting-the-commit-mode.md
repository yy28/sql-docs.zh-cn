---
description: 设置提交模式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a71d6f97f4683f9177c940be7d6ca1cc4a27c01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494621"
---
# <a name="setting-the-commit-mode"></a>设置提交模式
应用程序指定具有 SQL_ATTR_AUTOCOMMIT 连接属性的事务模式。 默认情况下，ODBC 事务处于自动提交模式 (除非不支持 **SQLSetConnectAttr** 和 **SQLSetConnectOption** ，这不太可能) 。 从手动提交模式切换到自动提交模式会自动提交连接上的任何打开的事务。
