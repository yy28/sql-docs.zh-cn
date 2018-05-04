---
title: SQL 类型标识符 |Microsoft 文档
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
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98c78940a3e01943da03b92f5791dc8f146b14c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-type-identifiers"></a>SQL 类型标识符
每个数据源定义其自己的 SQL 数据类型。 ODBC 定义类型标识符，并描述了可能映射到每个类型标识符的 SQL 数据类型的一般特征。 它是驱动程序特定的基础数据源中的每个数据类型映射到 ODBC SQL 类型标识符的方式。  
  
 例如，SQL_CHAR 是具有固定的长度，通常介于 1 到 254 个字符之间的字符列的类型标识符。 这些特性对应于在多个 SQL 数据源中找到的 CHAR 数据类型。 因此，当应用程序发现时为列的类型标识符是 SQL_CHAR，它可以假定可能处理 CHAR 列。 但是，它应仍检查的字节长度的前面假设它的列之间 1 到 254 个字符;因为都不为非 SQL 数据源，例如，驱动程序可能将 500 个字符的固定长度字符列映射到 SQL_CHAR 或 SQL_LONGVARCHAR、 完全匹配。  
  
 ODBC 定义各种类型的 SQL 标识符。 但是，该驱动程序不需要使用所有这些标识符。 相反，它使用基础数据源仅这些它需要公开支持的 SQL 数据类型的标识符。 如果基础数据源支持到 SQL 数据类型的任何类型标识符对应，该驱动程序可以定义其他类型标识符。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 SQL 类型标识符的完整说明，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中。
