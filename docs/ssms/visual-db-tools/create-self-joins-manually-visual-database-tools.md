---
title: 手动创建自联接 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ad4abd99364ec906cb61a37b8e7f47c7095e2081
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090053"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>手动创建自联接 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
即使表在数据库中没有自反关系，您也可将它与自身联接。 例如，可使用自联接查找生活在同一市县的作者对。  
  
与任何联接一样，自联接至少需要两个表。 不同之处在于，您不是向查询中添加第二个表，而是添加同一个表的第二个实例。 这样，可将表的第一个实例中的列与第二个实例中的同一列相比较，以便对列中的值相互进行比较。 [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 为表的第二个实例分配一个别名。  
  
例如，若要创建自联接来查找居住在 Berkeley 的所有作者对，则可将表的第一个实例中的 `city` 列与第二个实例中的 `city` 列相比较。 生成的查询结果可能类似以下形式：  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
创建自联接通常需要多个联接条件。 若要了解其中的原因，请考虑上述查询的结果：  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
第一行没有用，它只是指示 Cheryl Carson 和 Cheryl Carson 生活在同一市县。 第二行也没有用。 若要消除这些无用数据，可添加另一个条件，仅保留其中的两个作者姓名是指不同作者的结果行。 生成的查询结果可能类似以下形式：  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
结果集就精简为：  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
但是这两个结果行是冗余的。 第一行说 Carson 与 Bennet 生活在同一市县，第二行说 Bennet 与 Carson 生活在同一市县。 若要消除这一冗余，可将第二个联接条件从“不等于”更改为“小于”。 生成的查询结果可能类似以下形式：  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
结果集类似以下形式：  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>手动创建自联接  
  
1.  将要使用的表或表值对象添加到 [“关系图”窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  再次添加同一个表，以便“关系图”窗格中显示同一个表或表值对象两次。  
  
    查询和视图设计器将通过为表名添加一个顺序号来为第二个实例分配别名。 此外，查询和视图设计器会在“关系图”窗格内表或表值对象的两个实例之间创建一条联接线。  
  
3.  右键单击联接线，再从快捷菜单中选择“属性”。  
  
4.  在“属性”窗口中，单击“联接条件和类型”，再单击该属性右侧的省略号 (…)。  
  
5.  在[“联接”对话框](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)中，根据需要更改两个主键间的比较运算符。 例如，可将运算符更改为小于 (<)。  
  
6.  通过拖动表或表值对象的第一个实例中的主联接列的名称，并将其放置到第二个实例的相应列上，即可创建附加联接条件（例如，authors.zip = authors1.zip）。  
  
7.  为查询指定其他选项，如输出列、搜索条件和排序顺序等。  
  
## <a name="see-also"></a>另请参阅  
[自动创建自联接 (Visual Database Tools)](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
