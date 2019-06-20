---
title: SQLGetTypeInfo （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05cc6dc2647b5297b8d7176cd4bc70261b78cb71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181411"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：级别 1  
  
 返回有关所支持的数据源的数据类型的信息。 该驱动程序中的 SQL 结果集返回的信息。 下表列出了 ODBC 数据类型和相应的 Visual FoxPro 数据类型。  
  
|ODBC 类型|Visual FoxPro 类型|  
|---------------|------------------------|  
|SQL_BIGINT|不提供支持。 没有 64 位 Visual FoxPro 类型。|  
|SQL_BIT|逻辑函数|  
|SQL_CHAR|字符|  
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|双精度|  
|SQL_FLOAT|双精度|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|备注 （二进制）|  
|SQL_LONGVARCHAR|备忘录|  
|SQL_NUMERIC|数字 *，货币，Float|  
|SQL_REAL|双精度|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|不提供支持。 没有任何 Visual FoxPro*时间*类型。|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|备注 （二进制） *，常规|  
|SQL_VARCHAR|字符|  
  
 * 默认类型  
  
 有关 Visual FoxPro 数据类型的详细信息，请参阅[CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)。 有关此函数的详细信息，请参阅[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)中*ODBC 程序员参考*。
