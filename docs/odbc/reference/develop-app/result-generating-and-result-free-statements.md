---
title: 结果生成和无结果语句 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc94aabd7982fba5879519573980db03b1857ef6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300087"
---
# <a name="result-generating-and-result-free-statements"></a>结果生成和无结果语句
SQL 语句可以大致分为以下五个类别：  
  
-   **结果集生成语句**这些是生成结果集的 SQL 语句。 例如 **，SELECT**语句。  
  
-   **行计数生成语句**这些是生成受影响行计数的 SQL 语句。 例如，**更新**或**删除**语句。  
  
-   **数据定义语言 （DDL） 语句**这些是修改数据库结构的 SQL 语句。 例如，**创建表**或**DROP 索引**。  
  
-   **上下文更改语句**这些是更改数据库上下文的 SQL 语句。 例如，SQL Server 中的**USE**和**SET**语句。  
  
-   **行政声明**这些是用于数据库中管理目的的 SQL 语句。 例如，**授予**和**撤销**。  
  
 前两个类别中的 SQL 语句统称为*生成结果语句*。 后三个类别中的 SQL 语句统称为*无结果语句*。 ODBC 定义只包含结果生成语句的批处理的语义。 这些语义差异很大，因此特定于数据源。 例如，SQL Server 驱动程序不支持删除对象，然后引用或在同一批处理中重新创建同一对象。 因此，本手册中使用的术语*批处理*仅指结果生成语句的批处理。
