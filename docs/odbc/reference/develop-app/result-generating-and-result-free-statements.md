---
title: "结果生成和无结果的语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac7d08e9ca59738686baa079d87af8c158bca35a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="result-generating-and-result-free-statements"></a>结果生成和无结果的语句
SQL 语句可以松散分为以下五种类别：  
  
-   **结果集生成语句**这些是生成的结果集的 SQL 语句。 例如，**选择**语句。  
  
-   **行计数生成语句**这些是生成受影响的行的计数的 SQL 语句。 例如，**更新**或**删除**语句。  
  
-   **数据定义语言 (DDL) 语句**这些是修改数据库的结构的 SQL 语句。 例如， **CREATE TABLE**或**DROP INDEX**。  
  
-   **上下文更改语句**这些是更改数据库的上下文的 SQL 语句。 例如，**使用**和**设置**SQL Server 中的语句。  
  
-   **管理语句**这些是用于管理目的在数据库中的 SQL 语句。 例如，**授予**和**撤消**。  
  
 前两个类别中的 SQL 语句统称为*结果生成语句*。 后三个类别中的 SQL 语句统称为*无结果的语句*。 ODBC 定义包括仅生成结果的语句的批处理的语义。 这些语义有很大差异，因此数据源 – 特定。 例如，SQL Server 驱动程序不支持删除对象，然后引用或重新创建同一个批处理中的相同对象。 因此，术语*批处理*因为用此手册仅指批处理的结果生成的语句。
