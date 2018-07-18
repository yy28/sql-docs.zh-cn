---
title: 创建外部联接 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eaa656ab6775594477ed4d83470b1c2ebab642c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33047754"
---
# <a name="create-outer-joins-visual-database-tools"></a>创建外部联接 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
默认情况下， [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 在表之间创建内部联接。 内部联接消除了与其他表中的行不匹配的行。 但是，外部联接可以从 FROM 子句中提到的至少一个表或视图中返回所有行，只要这些行符合任何 WHERE 或 HAVING 搜索条件。 若要在结果集中包含在联接表无匹配项的数据行，可以创建外部联接。  
  
在创建外部联接时，表在 SQL 语句中出现的顺序（反映在 SQL 窗格中）非常重要。 添加的第一个表成为“左”表，而第二个表成为“右”表。 （表在[“关系图”窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)中实际出现的顺序并不重要。）当指定左外部联接或右外部联接时，引用的顺序是将这些表添加到查询中的顺序，以及它们在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中的 SQL 语句中出现的顺序。  
  
### <a name="to-create-an-outer-join"></a>创建外部联接  
  
1.  自动或手动创建外部联接。 有关详细信息，请参阅[自动联接表 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md) 或[手动联接表 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)。  
  
2.  在“关系图”窗格中选择联接线，然后在“查询设计器”菜单中选择“选择 <tablename> 中的全部行”，选择包含要包含其中更多行的表的命令。  
  
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
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[“联接”对话框 (Visual Database Tools)](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
