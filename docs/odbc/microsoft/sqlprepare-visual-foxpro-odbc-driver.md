---
title: "SQLPrepare （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ef6287177be3b52b80e0a2439d7d0686da180da
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 核心级别  
  
 通过规划如何优化并执行语句准备 SQL 语句。 通过执行编译 SQL 语句[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 如果你的表、 视图或字段名称包含空格，将名称括在返回引号 （'） 标记。 例如，如果你的数据库包含名为我的表和字段 My Field 的表，将包含标识符的每个元素，如下所示：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 有关详细信息，请参阅[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)中*ODBC 程序员参考*。

