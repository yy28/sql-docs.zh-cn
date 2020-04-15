---
title: SQL 到 C： GUID |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0f247bc4cb411d535050d7c78e0ea42cc144b0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296457"
---
# <a name="sql-to-c-guid"></a>从 SQL 到 C：GUID
GUID ODBC SQL 数据类型的标识符是：  
  
 SQL_GUID  
  
 下表显示了可转换为 GUID SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*缓冲区长度*>字符字节长度|数据|36|不适用|  
||*缓冲区长度*< 37|Undefined|Undefined|22003|  
|SQL_C_WCHAR|*缓冲区长度*>字符长度|数据|36|不适用|  
||*缓冲区长度*< 37|Undefined|Undefined|22003|  
|SQL_C_BINARY|数据\<= *缓冲区长度*的字节长度|数据|以字节为单位的数据长度|不适用|  
||>*缓冲区长度*的数据字节长度|Undefined|Undefined|22003|  
|SQL_C_GUID|无[a]|数据|16[b]|不适用|  
  
 [a] 此转换将忽略*缓冲区长度*的值。 驱动程序假定 **目标价值Ptr*的大小是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。
