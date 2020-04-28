---
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
ms.openlocfilehash: 952ace7d17e8bb5b4c824761b02e5c8a0895f519
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303938"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函数
**度**  
 引入的版本： ODBC 1.0，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 中，已使用 ODBC_REMOVE_DEFAULT_DSN 的*fRequest*参数调用[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)的**SQLRemoveDefaultDataSource**函数。 如果 ODBC 2.x 安装程序调用了此函数，则*odbc 安装程序*将映射到以下**SQLConfigDataSource**调用：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
