---
title: 对行进行排序
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: d7d7409f6f52c7fa178eb276f6878d22854d0157
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999324"
---
# <a name="sort-rows-visual-database-tools"></a>对行进行排序 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以对查询结果中的行进行排序。 也就是说，可以对特定的列或一组列进行命名，该列或这些列的值决定结果集中行的顺序。  
  
> [!NOTE]  
> 排序顺序在一定程度上由列的排序规则顺序来决定。 可以在 [“排序规则”对话框](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)中更改排序规则顺序。  
  
下面是几种可以用来对查询结果进行排序的方法：  
  
-   **可按升序或降序来排列行** 默认情况下，SQL 使用排序依据列按升序排列行。 例如，若要依据价格按升序来排列书籍名称，只需按 price 列对行进行排序即可。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
    ```  
  
    另一方面，若要排列书籍名称，使较贵的书排在前面，可以显式指定最贵的排在第一位的顺序。 也就是说，指定应按 price 列的降序值来排列结果行。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **可按多个列进行排序** 例如，可以创建每个作者占一行、先按省市自治区再按市县排序的结果集。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
    ```  
  
-   **可按未显示在结果集中的列进行排序** 例如，可以创建这样的结果集：最贵的书排在第一位，尽管该书的价格没有显示在结果集中。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **可按派生列进行排序** 例如，可以创建每个书籍名称占一行的结果集，并将单本版税最高的书排在第一位。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
    ```  
  
    （用于计算每本书单本所赚版税的公式突出显示。）  
  
    若要计算派生列，可以使用 SQL 语法（如上例所示），或者使用返回标量值的用户定义函数。 有关用户定义函数的详细信息，请参阅 SQL Server 文档。  
  
-   **可对分组的行进行排序** 例如，可以创建这样的结果集：每行描述一个市县以及该市县中的作者数，并使包含作者多的市县排在前面。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
    ```  
  
    请注意，该查询将 `state` 用作次要排序列。 因此，如果两个州的作者数相同，则这两个州将按字母顺序显示。  
  
-   **可使用国际数据进行排序** 也就是说，可以使用与该列的默认约定不同的排序约定对列进行排序。 例如，可以编写一个查询，检索 Jaime Patiño 编写的所有书籍名称。 若要按字母顺序显示书籍名称，请对 title 列使用 Spanish 排序顺序。 生成的 SQL 结果可能类似以下形式：  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>另请参阅  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
