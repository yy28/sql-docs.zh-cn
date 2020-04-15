---
title: SQL-92 合规性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ac0ae5873e545afb8fcac9dd003c984b1ed303a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300697"
---
# <a name="sql-92-compliance"></a>SQL-92 符合性
ODBC 桌面数据库驱动程序和基础的 Microsoft Jet 引擎不符合 SQL-92。 它们支持 SQL-92 中定义的许多功能。 SQL-92 不支持驱动程序中支持的某些功能。 有关详细信息，请参阅 Microsoft*喷气数据库引擎程序员指南*。 以下是两者之间的主要区别：  
  
-   桌面数据库驱动程序使用的 SQL 支持比 SQL-92 指定的表达式更强大的表达式。  
  
-   不同的规则适用于"之间"谓词。  
  
-   桌面数据库驱动程序和 ANSI SQL 使用的 SQL 支持不同的关键字。  
  
 微软 Jet SQL 不支持以下 SQL-92 功能：  
  
-   安全语句，如 GRANT 和 LOCK。  
  
-   带聚合函数引用的  
  
 以下功能是 SQL-92 未指定的桌面数据库驱动程序使用的 SQL 中的增强功能：  
  
-   提供对交叉表查询支持的 TRANSFORM 语句。  
  
-   其他聚合函数 （**StDev**和**VarP**）。  
  
> [!NOTE]  
>  桌面数据库驱动程序支持百分比（百分比）和 # （下划线）、而不是 * （星号）和 （问号）。
