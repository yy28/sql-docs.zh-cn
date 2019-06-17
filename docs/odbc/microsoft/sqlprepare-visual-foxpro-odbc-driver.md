---
title: SQLPrepare （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3ef083829b1ce322f2cede53f853c80683f01cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636666"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 通过规划如何优化并执行语句，准备 SQL 语句。 通过执行编译 SQL 语句[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 如果表、 视图或字段名称包含空格，将名称括在返回引号 （'） 标记。 例如，如果你的数据库包含名为我的表和字段 My Field 的表，则将标识符的每个元素，如下所示：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 有关详细信息，请参阅[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)中*ODBC 程序员参考*。
