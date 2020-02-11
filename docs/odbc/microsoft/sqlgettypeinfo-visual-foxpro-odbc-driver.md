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
ms.openlocfilehash: f29be5e03a6cc9c1c91809db2b8ec7c686e90f11
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898629"
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
|SQL_CHAR|Character|  
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
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
|SQL_VARCHAR|Character|  
  
 * 默认类型  
  
 有关 Visual FoxPro 数据类型的详细信息，请参阅[CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)。 有关此函数的详细信息，请参阅*ODBC 程序员参考*中的[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 。
