---
title: SQLRemoveDefaultDataSource 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 072f599ad63e7b624478e66030356367d944fd17
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函数
**一致性**  
 版本引入了： ODBC 1.0，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 中， **SQLRemoveDefaultDataSource**对的调用替换为函数[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)与*fRequest* ODBC_REMOVE_DEFAULT_DSN 自变量。 如果 ODBC 2 *.x*安装程序会调用此函数，ODBC 安装程序会将其映射到以下**SQLConfigDataSource**调用：  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
