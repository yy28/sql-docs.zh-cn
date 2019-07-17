---
title: 支持 ODBC SQL 语法 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 535f2feaf17d2060c1c65e7aba17951bb3339a5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080057"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>支持的 ODBC SQL 语法（Visual FoxPro ODBC 驱动程序）
Microsoft Visual FoxPro ODBC 驱动程序支持以下功能：  
  
-   所有 SQL 语句和子句中的 ODBC 最小 SQL 语法  
  
-   其他 SQL 语句从 ODBC 核心 SQL 语法  
  
 下表列出了支持的驱动程序，通过 ODBC SQL 语法级别的项。  
  
|级别|元素|项|  
|-----------|--------------|----------|  
|最低要求|数据定义语言 (DDL)|CREATE TABLE 和 DROP TABLE|  
||数据操作语言 (DML)|选择、 插入、 更新和删除|  
||表达式|简单 (例如 A > B + C)|  
||数据类型|CHAR、 VARCHAR、 或 LONG VARCHAR|  
  
 除了支持 ODBC SQL 语法，Visual FoxPro ODBC 驱动程序支持以下 Visual FoxPro 命令的完整的本机 Visual FoxPro 语言语法：  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [删除标记](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
