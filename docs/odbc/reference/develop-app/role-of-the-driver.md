---
title: 驱动程序的角色 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2687e1a68789566fd7b660a8241d65ff4714a933
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633565"
---
# <a name="role-of-the-driver"></a>驱动程序的角色
驱动程序检查所有错误和警告不会检查由驱动程序管理器，它将生成的状态记录进行排序。 (ODBC 2。*x*驱动程序不排序状态记录。)这包括在数据截断、 数据转换、 语法和某些状态转换的错误和警告。 错误和警告部分选中由驱动程序管理器中，可能还会检查驱动程序。 例如，尽管驱动程序管理器检查是否的值*操作*中**SQLSetPos**是合法的该驱动程序必须检查是否支持。  
  
 该驱动程序还映射*本机错误*— 也就是说，返回的数据源的错误 — SQLSTATEs 到。 例如，驱动程序可能会映射的多个不同的非法 SQL 语法 SQLSTATE 42000 （语法错误或访问冲突） 的本机错误。 状态记录的 SQL_DIAG_NATIVE 字段中，驱动程序返回本机错误号。 驱动程序文档应显示错误和警告映射的方式从数据源到中的自变量**SQLGetDiagRec**并**SQLGetDiagField**。
