---
title: SQLGetTypeInfo（可视化福克斯Pro ODBC驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299517"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：1 级  
  
 返回有关数据源支持的数据类型的信息。 驱动程序返回 SQL 结果集中的信息。 下表列出了 ODBC 数据类型和相应的 Visual FoxPro 数据类型。  
  
|ODBC 类型|可视化狐狸专业类型|  
|---------------|------------------------|  
|SQL_BIGINT|不支持。 没有 64 位可视化福克斯专业类型。|  
|SQL_BIT|逻辑|  
|SQL_CHAR|字符|  
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|备忘录（二进制）|  
|SQL_LONGVARCHAR|备忘录|  
|SQL_NUMERIC|数字*， 货币， 浮动|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|不支持。 没有可视化 FoxPro*时间*类型。|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|备忘录（二进制）*，一般|  
|SQL_VARCHAR|字符|  
  
 *默认类型  
  
 有关 Visual FoxPro 数据类型的详细信息，请参阅[创建表](../../odbc/microsoft/create-table-sql-command.md)。 有关此功能的详细信息，请参阅*ODBC 程序员参考*中的[SQLGetTypeInfo。](../../odbc/reference/syntax/sqlgettypeinfo-function.md)
