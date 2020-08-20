---
description: SQLPrepare（Visual FoxPro ODBC 驱动程序）
title: SQLPrepare (Visual FoxPro ODBC 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8dfda2e04711681144e4a5cd21e445570e30a1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500150"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 通过计划如何优化和执行语句来准备 SQL 语句。 为执行 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)编译 SQL 语句。  
  
 如果表、视图或字段的名称包含空格，请将名称放在后引号中 (") 标记。 例如，如果您的数据库包含名为 "我的表" 和 "我的字段" 字段的表，则将标识符的每个元素括起来，如下所示：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) 。
