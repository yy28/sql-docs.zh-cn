---
title: SQL删除默认数据源函数 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303938"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函数
**一致性**  
 版本介绍： ODBC 1.0， 已弃用  
  
 **摘要**  
 在 ODBC 3.0 中 **，SQLRemoveDefaultDataSource**函数已被对[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)的调用替换为 ODBC_REMOVE_DEFAULT_DSN的*fRequest*参数。 如果 ODBC 2 *.x*安装程序调用此功能，ODBC 安装程序将将其映射到以下**SQLConfigDataSource**调用：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
