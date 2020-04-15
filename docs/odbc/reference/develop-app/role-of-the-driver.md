---
title: 驱动程序的角色 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304278"
---
# <a name="role-of-the-driver"></a>驱动程序的角色
驱动程序检查驱动程序管理器未检查的所有错误和警告，并命令它生成的状态记录。 （ODBC 2。*x*驱动程序不订购状态记录。这包括数据截断、数据转换、语法和某些状态转换中的错误和警告。 驱动程序还可能检查驱动程序管理器部分检查的错误和警告。 例如，尽管驱动程序管理器检查**SQLSetPos**中*的操作*值是否合法，但驱动程序必须检查它是否受支持。  
  
 该驱动程序还将*本机错误*（即数据源返回的错误）映射到 SQLSTAT。 例如，驱动程序可能会将非法 SQL 语法的许多不同的本机错误映射到 SQLSTATE 42000（语法错误或访问冲突）。 驱动程序返回状态记录SQL_DIAG_NATIVE字段中的本机错误编号。 驱动程序文档应显示如何从数据源映射到**SQLGetDiagRec**和**SQLGetDiagField**中的参数。
