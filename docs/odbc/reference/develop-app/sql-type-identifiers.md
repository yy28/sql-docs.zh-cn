---
title: SQL 类型标识符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1763ee0cd8c5bc2017160de44b9c047781649eba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150023"
---
# <a name="sql-type-identifiers"></a>SQL 类型标识符
每个数据源定义其自己的 SQL 数据类型。 ODBC 定义类型的标识符和描述可能映射到每个类型标识符的 SQL 数据类型的一般特征。 它是驱动程序特定于如何在基础数据源中的每种数据类型映射到的 ODBC SQL 类型标识符。  
  
 例如，SQL_CHAR 是具有固定长度，通常介于 1 到 254 个字符之间的字符列的类型标识符。 这些特性对应于在多个 SQL 数据源中找到的 CHAR 数据类型。 因此，当应用程序发现某一列的类型标识符是 SQL_CHAR，它会假定它可能在处理对 CHAR 列。 但是，它应并仍检查假设它前面的列的字节长度为 1 到 254 个字符的字符;因为既不是为非 SQL 数据源，例如，驱动程序可能会将 500 个字符的固定长度的字符列映射到 SQL_CHAR 或 SQL_LONGVARCHAR，完全匹配。  
  
 ODBC 定义各种类型的 SQL 标识符。 但是，该驱动程序不需要使用所有这些标识符。 相反，它使用基础数据源仅需要公开支持的 SQL 数据类型的标识符。 如果基础数据源支持到 SQL 数据类型的任何类型标识符相对应，该驱动程序可以定义其他类型标识符。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 SQL 类型标识符的完整说明，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)中附录 d:数据类型。
