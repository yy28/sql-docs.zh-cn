---
title: 使用连接字符串 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1e492423fec8f214890dfa7aa2f75c8a6ce19da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-connection-strings"></a>使用连接字符串
连接字符串可用于连接到 Visual FoxPro 数据源。  
  
 例如，若要连接到 TasTrade 数据源和与数据源关联独占的当前设置替代，将使用字符串：  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 属性关键字和可以包括连接字符串中的值的列表，请参阅[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。  
  
 有关连接字符串语法的完整说明，请参阅[SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md)中*ODBC 程序员参考*。
