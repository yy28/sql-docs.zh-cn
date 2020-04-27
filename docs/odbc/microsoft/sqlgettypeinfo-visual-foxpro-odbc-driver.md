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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23db0350f0f7271f85e2bc5c6a9e6c8767443a85
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "81299517"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别1  
  
 返回有关数据源支持的数据类型的信息。 驱动程序返回 SQL 结果集中的信息。 下表列出了 ODBC 数据类型以及相应的可视 FoxPro 数据类型。  
  
|ODBC 类型|视觉 FoxPro 类型|  
|---------------|------------------------|  
|SQL_BIGINT|不支持。 没有64位的视觉 FoxPro 类型。|  
|SQL_BIT|逻辑|  
|SQL_CHAR|字符|  
|SQL_DATE|日期|  
|SQL_DECIMAL|数字|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|备注（二进制）|  
|SQL_LONGVARCHAR|备忘录|  
|SQL_NUMERIC|Numeric *、Currency、Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|不支持。 没有 Visual FoxPro*时间*类型。|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|备注（二进制） *，常规|  
|SQL_VARCHAR|字符|  
  
 * 默认类型  
  
 有关 Visual FoxPro 数据类型的详细信息，请参阅[CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)。 有关此函数的详细信息，请参阅*ODBC 程序员参考*中的[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 。
