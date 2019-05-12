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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea540d2ef6747bbe3bfc9ac55f04afe1d63349f7
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537234"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函数
**符合性**  
 版本引入了：ODBC 1.0，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 **SQLRemoveDefaultDataSource**的调用替换为函数[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)与*fRequest* ODBC_REMOVE_DEFAULT_DSN 参数。 如果 ODBC 2 *.x*安装程序会调用此函数，ODBC 安装程序会将其映射到以下**SQLConfigDataSource**调用：  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
