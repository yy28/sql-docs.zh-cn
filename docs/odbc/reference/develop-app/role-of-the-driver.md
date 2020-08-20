---
description: 驱动程序的角色
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: afd8f058b12b30140bb193ded7a23e8daf365865
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465643"
---
# <a name="role-of-the-driver"></a>驱动程序的角色
驱动程序将检查驱动程序管理器不检查的所有错误和警告以及它生成的订单状态记录。  (ODBC 2。*x* 驱动程序不会对状态记录进行排序。 ) 这包括数据截断、数据转换、语法和某些状态转换中的错误和警告。 驱动程序还可能检查驱动程序管理器部分检查的错误和警告。 例如，尽管驱动程序管理器检查**SQLSetPos**中的*操作*的值是否合法，驱动程序必须检查它是否受支持。  
  
 驱动程序还会映射 *本机错误* ，即数据源返回的错误-SQLSTATEs。 例如，对于 SQLSTATE 42000 (语法错误或访问冲突) ，驱动程序可能会将多个不同的本机错误映射为非法的 SQL 语法。 驱动程序返回状态记录的 "SQL_DIAG_NATIVE" 字段中的本机错误号。 驱动程序文档应显示如何将数据源中的错误和警告映射到 **SQLGetDiagRec** 和 **SQLGetDiagField**中的参数。
