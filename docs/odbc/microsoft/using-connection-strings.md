---
title: 使用连接字符串 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77bc54f857e04f31ccb982ca40b3ed6334664870
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848766"
---
# <a name="using-connection-strings"></a>使用连接字符串
连接字符串可用于连接到 Visual FoxPro 数据源。  
  
 例如，若要连接到 TasTrade 数据源和排他的当前设置与数据源关联的重写，将使用字符串：  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 有关属性关键字和可以在连接字符串中包含的值的列表，请参阅[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。  
  
 有关连接字符串语法的完整说明，请参阅[SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md)中*ODBC 程序员参考*。
