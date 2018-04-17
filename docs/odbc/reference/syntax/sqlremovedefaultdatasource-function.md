---
title: SQLRemoveDefaultDataSource 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5b3a37cf0b0f42567d4a787b9c090f8298f74ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函数
**一致性**  
 版本引入了： ODBC 1.0，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 中， **SQLRemoveDefaultDataSource**对的调用替换为函数[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)与*fRequest* ODBC_REMOVE_DEFAULT_DSN 自变量。 如果 ODBC 2*.x*安装程序会调用此函数，ODBC 安装程序会将其映射到以下**SQLConfigDataSource**调用：  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
