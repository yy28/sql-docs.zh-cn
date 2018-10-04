---
title: 目录位置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22a9a9d50891a6101076af6378fb33543274b21b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606225"
---
# <a name="catalog-position"></a>目录位置
中的位置的目录名称标识符和分隔标识符的其余部分从方式从数据源到数据源而异。 例如，Xbase 数据源中的目录名称是一个目录，而且在 Microsoft® Windows®，从表名 （即文件名称） 由反斜杠分隔 (\\)。 下图演示了这种情况。  
  
 ![目录位置： Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 数据源中，目录是一个数据库和一个句点 （.） 分隔的架构和表名称。  
  
 ![目录位置： SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 数据源，目录将也是数据库，但后面的表名和分开的架构和表名称 at 符号 (@)。  
  
 ![目录位置： Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 若要确定目录分隔符和目录名称的位置，应用程序调用**SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 选项。 可互操作应用程序应构造根据这些值的标识符。  
  
 包含多个部分的标识符引起来，当应用程序必须小心单独引用每个部分，并加引号分隔标识符的字符。 例如，以下语句以选择的所有行和 Xbase 表的列加引号的目录 (\XBASE\SALES\CORP) 和表 (Parts.dbf) 名称，但不是目录分隔符 (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 要选择的所有行和列的 Oracle 表的以下语句引号 (Sales) 的目录、 架构 （企业） 和表 （部分） 名称，但不是在目录 (@) 或架构 （.） 分隔符：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 有关标识符引起来的信息，请参阅下一部分中，[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
