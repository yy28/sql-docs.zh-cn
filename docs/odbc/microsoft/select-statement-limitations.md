---
title: 选择语句限制 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300917"
---
# <a name="select-statement-limitations"></a>SELECT 语句限制
聚合函数列不能与 SELECT 语句中的非聚合列混合。  
  
 具有 GROUP BY 子句的 SELECT 语句的选择列表只能具有来自 GROUP BY 子句或集函数的表达式。  
  
 不支持在包含 GROUP BY 子句的 SELECT 语句中使用星号（以选择所有列）。 必须指定要选择的列的名称。  
  
 不支持在 SELECT 语句中使用垂直条。 如果需要引用包含垂直条的数据值，请使用 SELECT 语句中的参数。  
  
 在 SELECT 语句中使用列别名时，"as"一词必须位于别名之前。 例如，"SELECT col1 作为 a 从 b"。 如果没有"as"，语句将返回错误。  
  
 如果在 SELECT 语句中输入了不正确的列名称，则返回 SQLSTATE 07001 错误"错误参数数"，而不是 SQLSTATE S0022 错误"未找到列"。  
  
 使用 Microsoft Excel 驱动程序时，如果将空字符串插入到列中，则空字符串将转换为 NULL;如果将空字符串插入到列中，则将空字符串转换为 NULL。使用 WHERE 子句中的空字符串执行的搜索 SELECT 语句将不会在该列上成功。
