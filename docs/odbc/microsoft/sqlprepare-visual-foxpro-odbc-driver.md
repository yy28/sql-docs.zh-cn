---
title: SQL准备（可视化福克斯Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14c9358d04e539eb2c77a00e195e8216cd0f5496
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301553"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 通过规划如何优化和执行该语句来准备 SQL 语句。 SQL 语句编译供[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)执行。  
  
 如果表、视图或字段名称包含空格，请将名称包含在后引号 （'） 标记中。 例如，如果数据库包含名为"我的表"的表和字段"我的字段"，请按照如下方式包含标识符的每个元素：  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 有关详细信息，请参阅*ODBC 程序员参考中的* [SQLPrepare。](../../odbc/reference/syntax/sqlprepare-function.md)
