---
title: 创建表语句限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a83acb061cf8192dff1c6adede349f49a0b0bbdb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280868"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 语句限制
使用 Microsoft Access、Microsoft Excel 或 Paradox 驱动程序，并且未指定文本或二进制列的长度（或指定为 0）时，列长度将设置为 255。  
  
 使用 dBASE 驱动程序且未指定文本或二进制列的长度（或指定为 0）时，列长度将设置为 254。  
  
 最多支持 255 列。  
  
 当在 MicrosoftExcel 5.0、7.0 或 97 数据源上使用 Microsoft Excel 驱动程序时，无法创建与以前删除的工作表同名的工作表。 当 Microsoft Excel 驱动程序用于访问版本 5.0、7.0 或 97 工作表时，DROP TABLE 语句将清除工作表，但不会删除工作表名称。  
  
 使用 Paradox 驱动程序时，在表上定义索引后无法添加列。 如果 CREATE TABLE 语句的参数列表的第一列创建索引，则第二列不能包含在参数列表中。
