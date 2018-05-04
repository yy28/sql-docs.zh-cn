---
title: SELECT 语句限制 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e27e435fea1aeb864eb20ac478a72860394b8f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="select-statement-limitations"></a>SELECT 语句的限制
聚合函数列不能混合使用 SELECT 语句中的非聚合列。  
  
 具有 GROUP BY 子句的 SELECT 语句的选择列表只能有 GROUP BY 子句中的表达式或 set 函数。  
  
 不支持包含 GROUP BY 子句的 SELECT 语句中的星号 （若要选择所有列） 的使用。 必须指定要选择的列的名称。  
  
 不支持的垂直条 SELECT 语句中使用。 如果你需要引用包含竖线的数据值，请在 SELECT 语句中使用参数。  
  
 当在 SELECT 语句中使用列别名，"as"word 必须优先别名。 例如，"为 SELECT col1 从 b。" 而不是"为"，该语句将返回错误。  
  
 如果 SELECT 语句中输入不正确的列名称，则会返回 SQLSTATE 07001 错误，"参数错误数，"，而不是 SQLSTATE S0022 错误，"列找不到。"  
  
 当使用 Microsoft Excel 驱动程序时，如果列中插入一个空字符串时，将空字符串转换为 NULL;使用空字符串的 WHERE 子句中执行的搜索 SELECT 语句将对该列不会成功。
