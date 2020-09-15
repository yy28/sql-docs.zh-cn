---
description: “联接”对话框 (Visual Database Tools)
title: “联接”对话框
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.ppg.joinline
- vdtsql.chm:69638
ms.assetid: 0d9516bb-4ad3-4fcf-bb77-93474dea698f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 385e2a9cafa9323772068ed91872e8add00b3257
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423131"
---
# <a name="join-dialog-box-visual-database-tools"></a>“联接”对话框 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
使用此对话框可以指定用于对表进行联接的选项。 若要访问此对话框，请在“设计”**** 窗格中选择联接线。 然后，在“属性”窗口中单击“联接条件和类型”，再单击属性右侧显示的省略号 (…)************。  
  
默认情况下，相关表使用内部联接进行联接，内部联接可基于联接列中包含匹配信息的行创建结果集。 通过在“联接”**** 对话框中设置选项，可以指定基于不同运算符的联接，还可以指定外部联接。  
  
有关联接表的详细信息，请参阅[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)。  
  
## <a name="options"></a>选项  
  
|**条款**|**定义**|  
|------------|------------------|  
|**表**|联接中涉及的表或表值对象的名称。 不能在此处更改表名（此信息仅作为信息显示）。|  
|**列**|用于联接表的列的名称。 运算符列表中的运算符指定了这些列中数据之间的关系。 不能在此处更改列名（此信息仅作为信息显示）。|  
|**“运算符”**|指定用于使联接列相关的运算符。 若要指定等号 (=) 以外的运算符，请从列表中进行选择。 关闭该属性页后，您选择的运算符将显示在联接线的菱形图中，如下所示：<br /><br />![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools 图标")|  
|**所有行 <table1>**|指定即使右表中没有相应的匹配行，左表中的所有行也都显示在输出中。 右表中不包含匹配数据的列显示为空。 选择此选项等效于在 SQL 语句中指定 LEFT OUTER JOIN。|  
|**所有行 <table2>**|指定即使左表中没有相应的匹配行，右表中的所有行也都显示在输出中。 左表中不包含匹配数据的列显示为空。 选择此选项等效于在 SQL 语句中指定 RIGHT OUTER JOIN。|  
  
同时选择“<table1> 中的所有行”**** 和“<table2> 中的所有行”**** 等效于在 SQL 语句中指定 FULL OUTER JOIN。  
  
当选择创建外部联接的选项时，联接线中的菱形图会随之改变，以指示联接是左外部联接、右外部联接还是完全外部联接。  
  
> [!NOTE]  
> 文中的“左”和“右”并不一定与表在“关系图”窗格中的位置相对应。 “左”指的是其名称显示在 SQL 语句中 JOIN 关键字左侧的表，而“右”指的是其名称显示在 JOIN 关键字右侧的表。 在“关系图”**** 窗格中移动表时不会更改表原有的“左”或“右”顺序。  
  
## <a name="see-also"></a>另请参阅  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
