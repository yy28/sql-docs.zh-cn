---
title: "为 c: GUID 的 SQL |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d60ca76d44f443c564bd354535833ab6c7b407f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-guid"></a>为 c: GUID 的 SQL
GUID ODBC SQL 数据类型的标识符是：  
  
 SQL_GUID  
  
 下表显示 ODBC C 数据类型 GUID SQL 数据可能转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度|data|36|不适用|  
||*BufferLength* < 37|未定义|未定义|22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度|data|36|不适用|  
||*BufferLength* < 37|未定义|未定义|22003|  
|SQL_C_BINARY|数据的字节长度\< =  *BufferLength*|data|以字节为单位的数据的长度|不适用|  
||数据的字节长度 > *BufferLength*|未定义|未定义|22003|  
|SQL_C_GUID|无 [a]|data|16 [b]|不适用|  
  
 [a] 的值*BufferLength*忽略此转换。 该驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是对应的 C 数据类型的大小。

