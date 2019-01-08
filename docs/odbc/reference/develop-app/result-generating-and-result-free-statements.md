---
title: 结果生成和无结果的语句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f357576e9e7510ae581b41a50976a34981f35109
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517346"
---
# <a name="result-generating-and-result-free-statements"></a>结果生成和无结果语句
SQL 语句可以松散分为以下五种类别：  
  
-   **结果集生成语句**这些是生成的结果集的 SQL 语句。 例如，**选择**语句。  
  
-   **行计数生成语句**这些是生成受影响的行计数的 SQL 语句。 例如，**更新**或**删除**语句。  
  
-   **数据定义语言 (DDL) 语句**这些是修改数据库结构的 SQL 语句。 例如， **CREATE TABLE**或**DROP INDEX**。  
  
-   **上下文更改语句**这些是更改数据库的上下文的 SQL 语句。 例如，**使用**并**设置**SQL Server 中的语句。  
  
-   **管理语句**这些是用于管理目的在数据库中的 SQL 语句。 例如， **GRANT**并**撤消**。  
  
 前两个类别中的 SQL 语句统称为*结果生成语句*。 后一种的三个类别中的 SQL 语句统称为*语句无结果*。 ODBC 定义的批处理包含仅生成结果的语句的语义。 这些语义差异很大，因此数据源特定于。 例如，SQL Server 驱动程序不支持将对象拖动然后引用或重新创建同一批中的同一对象。 因此，术语*批处理*本手册中使用时将只向一批结果生成语句。
