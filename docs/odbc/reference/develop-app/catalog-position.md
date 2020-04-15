---
title: 目录位置 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0305d978dc4ecd21892a0be3916fa5072b7be95a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303378"
---
# <a name="catalog-position"></a>目录位置
目录名称在标识符中的位置以及它与标识符的其余部分的分离方式因数据源而异。 例如，在 Xbase 数据源中，目录名称是目录，在 Microsoft 中® Windows®，由反斜杠 （）\\与表名（文件名）分隔。 下图演示了此条件。  
  
 ![目录位置：Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 数据源中，目录是数据库，与架构和表名分隔了一个句点 （.）。  
  
 ![目录位置：SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 数据源中，目录也是数据库，但遵循表名称，并由 at a 符号 （*） 与架构和表名称分开。  
  
 ![目录位置：Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 要确定目录分隔符和目录名称的位置，应用程序使用SQL_CATALOG_NAME_SEPARATOR和SQL_CATALOG_LOCATION选项调用**SQLGetInfo。** 可互操作的应用程序应根据这些值构造标识符。  
  
 在引用包含多个部件的标识符时，应用程序必须小心单独报价每个部件，而不是引用分隔标识符的字符。 例如，以下语句用于选择 Xbase 表的所有行和列，引用目录 （_XBASE_SALES_CORP） 和表 （parts.dbf） 名称，但不包括目录分隔符 （\\）：  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 以下用于选择 Oracle 表的所有行和列的语句引用目录（销售）、架构（公司）和表（部件）名称，但引用目录 （+） 或架构 （.） 分隔符：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 有关报价标识符的信息，请参阅下一节["引用标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)"。
