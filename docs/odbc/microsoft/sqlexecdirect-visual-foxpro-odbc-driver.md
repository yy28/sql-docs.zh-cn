---
title: SQLExecDirect （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 808d7890c18839c0e9059cdc3181a4579eb2ec4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313312"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 执行一个新[可准备对象的 SQL 语句](../../odbc/microsoft/visual-foxpro-terminology.md)。 Visual FoxPro ODBC 驱动程序使用参数标记变量的当前值，如果在语句中存在任何参数。  
  
 若要创建批处理命令以提交一次的多个 SQL 语句，请使用分号 （;） 分隔批处理中的每个 SQL 语句。  
  
 如果表、 视图或字段名称包含空格，将名称括在返回引号标记。 例如，如果你的数据库包含名为我的表和字段 My Field 的表，则将标识符的每个元素，如下所示：  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 有关详细信息，请参阅[SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md)中*ODBC 程序员参考*。
