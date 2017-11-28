---
title: "目录位置 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4b219fe2f008c6e7f0e289211665a1dcf6f1bd1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="catalog-position"></a>目录位置
中的位置的目录名称标识符以及它与标识符的其余部分分隔的方式从数据源到数据源而异。 例如，Xbase 数据源中的目录名称目录，并且，在 Microsoft® Windows®，分隔的表名称 （这是文件名称） 从反斜杠 (\\)。 下图演示了这种情况。  
  
 ![目录位置： Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 数据源，该目录的数据库，由句点 （.） 分隔的架构和表名称。  
  
 ![目录位置： SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 数据源，目录将也是数据库，但后面的表名称和分开的架构和表的名称，由 at 符号 (@)。  
  
 ![目录位置： Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 若要确定目录分隔符和目录名称的位置，应用程序调用**SQLGetInfo**使用 SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 选项。 可互操作的应用程序应该构建根据这些值的标识符。  
  
 当包含多个部分标识符引起来，应用程序必须小心地将其单独 quote 每个部分和加引号分隔标识符的字符。 例如，以下语句以选择所有行和列的 Xbase 表行情目录 (\XBASE\SALES\CORP) 和表 (Parts.dbf) 名称，但不是的目录分隔符 (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 以下语句以选择所有行和列的 Oracle 表行情目录 (Sales)、 架构 （企业） 和表 （部分） 名称，但不是目录 (@) 或架构 （.） 分隔符：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 有关标识符引起来的信息，请参阅下一部分中，[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
