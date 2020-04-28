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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298667"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 执行新的[可准备对象 SQL 语句](../../odbc/microsoft/visual-foxpro-terminology.md)。 如果语句中存在任何参数，则 Visual FoxPro ODBC 驱动程序使用参数标记变量的当前值。  
  
 若要创建一个批处理命令以便一次提交多个 SQL 语句，请使用分号（;)分隔批处理中的每个 SQL 语句。  
  
 如果表、视图或字段的名称包含空格，则用引号将名称括起来。 例如，如果您的数据库包含名为 "我的表" 和 "我的字段" 字段的表，则将标识符的每个元素括起来，如下所示：  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 。
