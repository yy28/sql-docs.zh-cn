---
title: 从 SQL 到 C：GUID | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a2ed3cffcb196cb09841df3b54fbfab53e22477
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056871"
---
# <a name="sql-to-c-guid"></a>从 SQL 到 C：GUID
GUID ODBC SQL 数据类型的标识符是：  
  
 SQL_GUID  
  
 下表显示 ODBC C 数据类型可能会转换为 GUID SQL 数据。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度|Data|36|不适用|  
||*BufferLength* < 37|未定义|未定义|22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度|Data|36|不适用|  
||*BufferLength* < 37|未定义|未定义|22003|  
|SQL_C_BINARY|数据的字节长度\< =  *BufferLength*|Data|以字节为单位的数据的长度|不适用|  
||数据的字节长度 > *BufferLength*|未定义|未定义|22003|  
|SQL_C_GUID|无 [a]|Data|16[b]|不适用|  
  
 [a] 的值*BufferLength*忽略此转换。 驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。
