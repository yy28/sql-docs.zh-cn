---
title: 折叠行组 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 20c267524869cd530a2a63a29abc9d149eb5b10c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123531"
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>折叠行组 (Visual Database Tools)
  您可以创建这样的一个查询结果，其中每个结果行都与来自原始数据的一整组行相对应。 在拆叠行时应谨记以下几点：  
  
-   **可以消除重复行** 有些查询可以创建显示多个相同行的结果集。 例如，可以创建这样的结果集：每行都包含作者所在市县的市县名和省市自治区名，但如果一个市县包含多个作者，则将会生成多个相同的行。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
     由上述查询生成的结果集不是很有用。 如果一个市县包含四个作者，则结果集将包括四个相同的行。 由于结果集不包括除 city 和 state 以外的任何其他列，因此无法区别这些相同的行。 避免这类重复行的一种方法是包含能可用于区分行的其他列。 例如，如果包含作者名，则每行将不相同（假设任一市县中不存在两个同名的作者）。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
  
    ```  
  
     当然，上述查询只是消除了表象，但并未真正解决问题。 也就是说，结果集不再含重复行，但该结果集已不再是关于市县的结果集。 若要消除原始结果集中的重复行，使每行仍描述一个市县，则可以创建只返回唯一行的查询。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
  
    ```  
  
     有关消除重复的详细信息，请参阅[排除重复行 (Visual Database Tools)](visual-database-tools.md)。  
  
-   **可计算多组行** 也就是说，可以汇总多组行中的信息。 例如，可以创建这样的结果集：每行包含作者所在市县的市县名和省市自治区名，以及该市县包含的作者数。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
  
    ```  
  
     有关计算多组行的详细信息，请参阅[汇总查询结果 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)和[对查询结果进行排序和分组 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)  
  
-   **可以使用选择条件包括多组行** 例如，可以创建这样的结果集：每行包含几个作者所在市县的市县名和省市自治区名，以及该市县包含的作者数。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
  
    ```  
  
     有关将选择条件用于多组行的详细信息，请参阅[为组指定条件 (Visual Database Tools)](specify-conditions-for-groups-visual-database-tools.md) 和[在同一查询中使用 HAVING 和 WHERE 子句 (Visual Database Tools)](use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)。  
  
## <a name="see-also"></a>请参阅  
 [指定搜索条件&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  