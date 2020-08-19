---
description: SQL-92 符合性
title: SQL-92 相容性 |Microsoft Docs
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
ms.openlocfilehash: 7d978b236c45d442732cd3602c3fbbb6d16dfd8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483430"
---
# <a name="sql-92-compliance"></a>SQL-92 符合性
ODBC 桌面数据库驱动程序和基础 Microsoft Jet 引擎与 SQL-92 兼容。 它们支持 SQL-92 中定义的许多功能。 SQL-92 不支持驱动程序中支持的某些功能。 有关详细信息，请参阅 *Microsoft Jet 数据库引擎程序员指南*。 下面是这两者之间的主要区别：  
  
-   桌面数据库驱动程序使用的 SQL 支持的表达式比 92 SQL 指定的更强大。  
  
-   不同的规则适用于 BETWEEN 谓词。  
  
-   桌面数据库驱动程序和 ANSI SQL 使用的 SQL 支持不同的关键字。  
  
 Microsoft Jet SQL 不支持以下 SQL-92 功能：  
  
-   安全语句，如 GRANT 和 LOCK。  
  
-   与聚合函数引用截然不同。  
  
 以下功能是不由 SQL-92 指定的桌面数据库驱动程序使用的 SQL 中的增强功能：  
  
-   为交叉表查询提供支持的 TRANSFORM 语句。  
  
-    (**StDev** 和 **VarP**) 的其他聚合函数。  
  
> [!NOTE]  
>  桌面数据库驱动程序支持% (%) 和 _ (下划线) 的标准 ANSI 语法，而不是 (星号) 和？ （问号）。
