---
title: SQLExecDirect（可视化福克斯Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298667"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 执行新的[可预准备 SQL 语句](../../odbc/microsoft/visual-foxpro-terminology.md)。 如果语句中存在任何参数，Visual FoxPro ODBC 驱动程序将使用参数标记变量的当前值。  
  
 要创建批处理命令以一次提交多个 SQL 语句，请使用分号（;)分隔批处理中的每个 SQL 语句。  
  
 如果表、视图或字段名称包含空格，请将名称包含在回引号中。 例如，如果数据库包含名为"我的表"的表和字段"我的字段"，请按照如下方式包含标识符的每个元素：  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLExecDirect。](../../odbc/reference/syntax/sqlexecdirect-function.md)
