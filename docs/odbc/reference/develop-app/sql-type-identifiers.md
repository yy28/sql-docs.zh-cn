---
title: SQL 类型标识符 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95bf46844e9ed91aac1ec6cb93a298995f0901d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299767"
---
# <a name="sql-type-identifiers"></a>SQL 类型标识符
每个数据源定义其自己的 SQL 数据类型。 ODBC 定义类型标识符，并描述可能映射到每个类型标识符的 SQL 数据类型的一般特征。 它是特定于驱动程序的基础数据源中每个数据类型映射到 ODBC 的 SQL 类型标识符的。  
  
 例如，SQL_CHAR 是具有固定长度（通常介于 1 到 254 个字符）的字符列的类型标识符。 这些特征对应于许多 SQL 数据源中的 CHAR 数据类型。 因此，当应用程序发现列的类型标识符SQL_CHAR时，它可以假定它可能正在处理 CHAR 列。 但是，在假定列介于 1 到 254 个字符之间之前，它仍应检查列的字节长度;例如，非 SQL 数据源的驱动程序可能会将 500 个字符的固定长度字符列映射到SQL_CHAR或SQL_LONGVARCHAR，因为两者都不是完全匹配的。  
  
 ODBC 定义了多种 SQL 类型标识符。 但是，驱动程序不需要使用所有这些标识符。 相反，它只使用它需要的标识符来公开基础数据源支持的 SQL 数据类型。 如果基础数据源支持没有类型标识符对应的 SQL 数据类型，则驱动程序可以定义其他类型标识符。 有关详细信息，请参阅[特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有关 SQL 类型标识符的完整说明，请参阅附录 D 中的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)：数据类型。
