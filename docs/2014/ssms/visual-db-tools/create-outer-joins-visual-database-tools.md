---
title: 创建外部联接 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd5c9a9cb2e40c7b0a235ff848c1f9a0025773a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63184307"
---
# <a name="create-outer-joins-visual-database-tools"></a>创建外部联接 (Visual Database Tools)
  默认情况下， [查询和视图设计器](visual-database-tools.md) 在表之间创建内部联接。 内部联接消除了与其他表中的行不匹配的行。 但是，外部联接可以从 FROM 子句中提到的至少一个表或视图中返回所有行，只要这些行符合任何 WHERE 或 HAVING 搜索条件。 若要在结果集中包含在联接表无匹配项的数据行，可以创建外部联接。  
  
 在创建外部联接时，表在 SQL 语句中出现的顺序（反映在 SQL 窗格中）非常重要。 添加的第一个表成为“左”表，而第二个表成为“右”表。 （表在 [“关系图”窗格](diagram-pane-visual-database-tools.md) 中实际出现的顺序并不重要。）当指定左外部联接或右外部联接时，引用的顺序是将这些表添加到查询中的顺序，以及它们在 [SQL 窗格](sql-pane-visual-database-tools.md)中的 SQL 语句中出现的顺序。  
  
### <a name="to-create-an-outer-join"></a>创建外部联接  
  
1.  自动或手动创建外部联接。 有关详细信息，请参阅[自动联接表 (Visual Database Tools)](join-tables-automatically-visual-database-tools.md) 或[手动联接表 (Visual Database Tools)](join-tables-manually-visual-database-tools.md)。  
  
2.  在 "关系图" 窗格中选择联接线，然后在 "**查询设计器**" 菜单中，选择 "**从 Tablename 中\<选择所有行">**，并选择包含要包含其额外行的表的命令。  
  
    -   选择第一个表可以创建左外部联接。  
  
    -   选择第二个表可以创建右外部联接。  
  
    -   选择两个表可以创建完全外部联接。  
  
 在指定外部联接时，查询和视图设计器将修改联接线以指示外部联接。  
  
 此外，查询和视图设计器将修改 SQL 窗格中的 SQL 语句，以反映联接类型的变化，如以下语句所示：  
  
```  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
```  
  
 因为外部联接包含不匹配的行，所以可使用它查找与外键约束冲突的行。 为此，可以创建一个外部联接，然后添加搜索条件以查找最右侧表的主键列为空的行。 例如，下面的外部联接可以查找在 `employee` 表中无相应行的 `jobs` 表中的行：  
  
```  
SELECT employee.emp_id, employee.job_id  
FROM employee LEFT OUTER JOIN jobs   
   ON employee.job_id = jobs.job_id  
WHERE (jobs.job_id IS NULL)  
```  
  
## <a name="see-also"></a>另请参阅  
 [利用联接查询 &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)   
 [“联接”对话框 (Visual Database Tools)](join-dialog-box-visual-database-tools.md)  
  
  
