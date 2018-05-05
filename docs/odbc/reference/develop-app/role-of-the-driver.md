---
title: 驱动程序的角色 |Microsoft 文档
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
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e0ef812cb4c397beeb5778c4e4764b7e79f5d0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="role-of-the-driver"></a>该驱动程序的角色
该驱动程序检查所有错误和警告不会检查由驱动程序管理器，并对它所生成的状态记录进行排序。 (一个 ODBC 2。*x*驱动程序不排序状态记录。)这包括数据截断、 数据转换、 语法和某些状态转换中的错误和警告。 错误和警告部分选中的驱动程序管理器，还可以检查驱动程序。 例如，尽管的驱动程序管理器检查是否的值*操作*中**SQLSetPos**是合法的该驱动程序必须检查是否支持。  
  
 该驱动程序还会将映射*本机错误*— 也就是说，返回的数据源的错误-到 SQLSTATEs。 例如，驱动程序可能会映射大量不同的本机错误非法 SQL 语法到 SQLSTATE 42000 （语法错误或访问冲突）。 该驱动程序返回的状态记录 SQL_DIAG_NATIVE 字段中的本机错误号。 驱动程序文档应显示如何错误和警告映射从数据源到自变量在**SQLGetDiagRec**和**SQLGetDiagField**。
