---
title: "驱动程序的角色 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2fe0d0545bcc787275bda3ba2154088f23eeda20
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="role-of-the-driver"></a>该驱动程序的角色
该驱动程序检查所有错误和警告不会检查由驱动程序管理器，并对它所生成的状态记录进行排序。 (一个 ODBC 2。*x*驱动程序不排序状态记录。)这包括数据截断、 数据转换、 语法和某些状态转换中的错误和警告。 错误和警告部分选中的驱动程序管理器，还可以检查驱动程序。 例如，尽管的驱动程序管理器检查是否的值*操作*中**SQLSetPos**是合法的该驱动程序必须检查是否支持。  
  
 该驱动程序还会将映射*本机错误*— 也就是说，返回的数据源的错误-到 SQLSTATEs。 例如，驱动程序可能会映射大量不同的本机错误非法 SQL 语法到 SQLSTATE 42000 （语法错误或访问冲突）。 该驱动程序返回的状态记录 SQL_DIAG_NATIVE 字段中的本机错误号。 驱动程序文档应显示如何错误和警告映射从数据源到自变量在**SQLGetDiagRec**和**SQLGetDiagField**。

