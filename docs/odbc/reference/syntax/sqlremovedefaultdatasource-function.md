---
description: SQLRemoveDefaultDataSource 函数
title: SQLRemoveDefaultDataSource 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0010e59cc4dfad2d54b8b1c4e59e83ea72fcd3ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487085"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函数
**度**  
 引入的版本： ODBC 1.0，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 中，已使用 ODBC_REMOVE_DEFAULT_DSN 的*fRequest*参数调用[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)的**SQLRemoveDefaultDataSource**函数。 如果 ODBC 2.x 安装程序调用了此函数，则*odbc 安装程序* 将映射到以下 **SQLConfigDataSource** 调用：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
