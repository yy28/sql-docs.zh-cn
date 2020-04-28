---
title: 结果生成和结果免费语句 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300087"
---
# <a name="result-generating-and-result-free-statements"></a>结果生成和无结果语句
SQL 语句可以松散分为以下五类：  
  
-   **结果集生成语句**这些是生成结果集的 SQL 语句。 例如， **SELECT**语句。  
  
-   **行计数-生成语句**这些是生成受影响行的计数的 SQL 语句。 例如， **UPDATE**或**DELETE**语句。  
  
-   **数据定义语言（DDL）语句**这些是修改数据库结构的 SQL 语句。 例如， **CREATE TABLE**或**DROP INDEX**。  
  
-   **上下文变化的语句**这些是更改数据库上下文的 SQL 语句。 例如，中的**USE**和**SET**语句 SQL Server。  
  
-   **管理语句**它们是在数据库中用于管理的 SQL 语句。 例如， **GRANT**和**REVOKE**。  
  
 前两个类别中的 SQL 语句统称为*结果生成语句*。 后三个类别中的 SQL 语句统称为 "*无结果" 语句*。 ODBC 定义仅包含结果生成语句的批处理的语义。 这些语义差别很大，因此是特定于数据源的。 例如，SQL Server 驱动程序不支持删除对象，然后在同一批中引用或重新创建相同的对象。 因此，在本手册中使用的 "*批处理*" 一词只引用结果生成语句的批处理。
