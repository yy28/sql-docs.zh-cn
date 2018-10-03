---
title: SQL-92 符合性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6d8d056c1658a924de4b108d3c0d025e8a58f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791485"
---
# <a name="sql-92-compliance"></a>SQL-92 符合性
ODBC 桌面数据库驱动程序和基础 Microsoft Jet 引擎不是 SQL-92 兼容。 它们支持已在 SQL-92 中定义的许多功能。 在 SQL-92 中不支持在驱动程序支持某些功能。 有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。 两者之间的主要差异如下：  
  
-   桌面数据库驱动程序使用 SQL 支持比指定的 SQL-92 更功能强大的表达式。  
  
-   不同的规则适用于 BETWEEN 谓词。  
  
-   使用桌面数据库驱动程序与在 ANSI SQL 的 SQL 支持不同的关键字。  
  
 Microsoft Jet SQL 不支持以下 SQL-92 功能：  
  
-   安全语句，例如授予和锁。  
  
-   DISTINCT 的聚合函数引用。  
  
 以下功能是使用未指定 SQL-92 的桌面数据库驱动程序的 SQL 中的增强功能：  
  
-   转换语句提供的交叉表查询支持。  
  
-   其他聚合函数 (**StDev**并**VarP**)。  
  
> [!NOTE]  
>  桌面数据库驱动程序支持标准的 ANSI 语法不支持 %（%） 和 _ （下划线） * （星号） 和？ （问号）。
