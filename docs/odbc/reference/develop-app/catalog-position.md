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
ms.openlocfilehash: 3d7c320521a9948c7968f4f7f5d42fd715f6c03d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062679"
---
# <a name="catalog-position"></a>目录位置
目录名称在标识符中的位置，以及如何将其与标识符的其余部分分隔开来不同于数据源。 例如，在 Xbase 数据源中，目录名称是目录，在 Microsoft® Windows®中，用反斜杠（\\）分隔的表名称（这是一个文件名）。 下图演示了这种情况。  
  
 ![目录位置：Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 的数据源中，目录是一个数据库，并以句点（.）分隔。  
  
 ![目录位置：SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 数据源中，目录也是数据库，但后面是表名称，并以 at 符号（@）分隔到架构和表名称。  
  
 ![目录位置：Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 若要确定目录分隔符和目录名称的位置，应用程序需要使用 SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 选项调用**SQLGetInfo** 。 可互操作的应用程序应根据这些值构造标识符。  
  
 在将包含多个部分的标识符引用时，应用程序必须小心地单独引用每个部件，而不是将标识符分隔的字符括起来。 例如，下面的语句选择 Xbase 表中的所有行和列，并将目录（\XBASE\SALES\CORP）和表（Parts）名称（而不是目录分隔符（\\））括起来：  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 以下语句用于选择 Oracle 表的所有行和列的引号（销售）、架构（公司）和表（部件）名称，但不包括目录（@）或架构（.）分隔符：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 有关引用标识符的信息，请参阅下一节[带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。
