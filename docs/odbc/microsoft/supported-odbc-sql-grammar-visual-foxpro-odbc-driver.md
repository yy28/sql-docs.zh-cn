---
title: 支持的 ODBC SQL 语法（可视化福克斯 Pro ODBC 驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f72548d0708a63f887f7d6da4d4f5988500f0eef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304080"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>支持的 ODBC SQL 语法（Visual FoxPro ODBC 驱动程序）
微软可视化福克斯Pro ODBC驱动程序支持以下内容：  
  
-   ODBC 最小 SQL 语法中的所有 SQL 语句和子句  
  
-   来自 ODBC 核心 SQL 语法的附加 SQL 语句  
  
 下表列出了驱动程序支持的项，由 ODBC SQL 语法级别列出。  
  
|级别|元素|Item|  
|-----------|--------------|----------|  
|最小值|数据定义语言 (DDL)|CREATE TABLE 和 DROP TABLE|  
||数据操作语言 （DML）|选择、插入、更新和删除|  
||表达式|简单（如 A>B+C）|  
||数据类型|查尔、瓦尔查尔或长瓦尔查尔|  
  
 除了支持的 ODBC SQL 语法外，Visual FoxPro ODBC 驱动程序还支持完整的本机 Visual FoxPro 语言语法，用于以下 Visual FoxPro 命令：  
  
 [更改表](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [删除](../../odbc/microsoft/delete-sql-command.md)  
  
 [删除标记](../../odbc/microsoft/delete-tag-command.md)  
  
 [掉落表](../../odbc/microsoft/drop-table-command.md)  
  
 [指数](../../odbc/microsoft/index-command.md)  
  
 [插入](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [更新](../../odbc/microsoft/update-sql-command.md)
