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
ms.openlocfilehash: be36bd8efc059c1a4f9b5ddf2cdd7faf32cf7dd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107452"
---
# <a name="sql-type-identifiers"></a>SQL 类型标识符
每个数据源都定义了其自己的 SQL 数据类型。 ODBC 定义类型标识符，并描述可能映射到每个类型标识符的 SQL 数据类型的一般特征。 它是特定于驱动程序的，基础数据源中的每个数据类型如何映射到 ODBC 的 SQL 类型标识符。  
  
 例如，SQL_CHAR 是具有固定长度的字符列的类型标识符，通常介于1到254个字符之间。 这些特性与许多 SQL 数据源中的 CHAR 数据类型相对应。 因此，当应用程序发现某列的类型标识符 SQL_CHAR 时，它可以假定它可能处理 CHAR 列。 但是，它仍应检查列的字节长度，前提是它在1到254个字符之间;例如，非 SQL 数据源的驱动程序可能将500字符的固定长度字符列映射到 SQL_CHAR 或 SQL_LONGVARCHAR，因为两者都不完全匹配。  
  
 ODBC 定义各种 SQL 类型标识符。 但是，驱动程序不需要使用所有这些标识符。 相反，它只使用需要公开基础数据源所支持的 SQL 数据类型的标识符。 如果基础数据源支持不与任何类型标识符对应的 SQL 数据类型，则驱动程序可以定义其他类型标识符。 有关详细信息，请参阅[驱动程序特定的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有关 SQL 类型标识符的完整说明，请参阅附录 D：数据类型中的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)。
