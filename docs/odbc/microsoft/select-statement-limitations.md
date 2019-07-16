---
title: SELECT 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cde0158e72d1e24c112c8e7955f0d6b317bd729
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987859"
---
# <a name="select-statement-limitations"></a>SELECT 语句限制
SELECT 语句中的非聚合列不能在聚合函数列。  
  
 中有 GROUP BY 子句的 SELECT 语句的选择列表只能有 GROUP BY 子句中的表达式或 set 函数。  
  
 不支持使用包含 GROUP BY 子句的 SELECT 语句中的星号 （若要选择所有列）。 必须指定要选择的列的名称。  
  
 不支持的垂直条 SELECT 语句中使用。 如果您需要引用包含一个垂直条数据值，请在 SELECT 语句中使用参数。  
  
 当在 SELECT 语句中使用列别名，"为"word 前面必须有别名。 例如，"SELECT col1 作为从 b。" 而无需"为"，该语句将返回错误。  
  
 如果 SELECT 语句中输入了不正确的列名称，则将返回一个 SQLSTATE 07001 错误，"错误数的参数，"，而不是 SQLSTATE S0022 错误"列找不到。"  
  
 使用 Microsoft Excel 驱动程序时，如果为空字符串插入到的列，则为空字符串转换为 NULL;使用空字符串的 WHERE 子句中执行的搜索选择语句将不会在该列上成功。
