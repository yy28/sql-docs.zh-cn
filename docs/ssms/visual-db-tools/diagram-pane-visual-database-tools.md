---
title: “关系图”窗格
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 9ba8a064256541ffc756ef37fe01f1205e6bc243
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251901"
---
# <a name="diagram-pane-visual-database-tools"></a>关系图窗格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
“关系图”窗格以图形形式显示了您通过数据连接选择的表或表值对象。 同时也会显示它们之间的联接关系。  
  
在“关系图”窗格中可以进行如下操作：  
  
-   添加或移除表和表值对象并指定要输出的数据列。  
  
-   创建或修改表和表值对象之间的联接。  
  
当您在“关系图”窗格中进行更改时，“条件”窗格和 SQL 窗格会自动更新以反映所做的更改。 例如，如果在“关系图”窗格内的表或表值对象窗口中选择某个要输出的列，查询和视图设计器会将该数据列添加到“条件”窗格中以及 SQL 窗格内的 SQL 语句中。  
  
每个表或表值对象在“关系图”窗格中均作为单独的窗口出现。 每个矩形的标题栏中的图标表示该矩形所代表的对象类型，如下表所示：  
  
## <a name="options"></a>选项  
**表**  
列出可以添加到“关系图”窗格中的表。 若要添加某个表，请选择该表，再单击“添加”  。 若要同时添加多个表，请选中这些表，再单击“添加”  。  
  
**视图**  
列出可以添加到“关系图”窗格中的视图。 若要添加某个视图，请选择该视图，再单击“添加”  。 若要同时添加多个视图，请选中这些视图，再单击“添加”  。  
  
**函数**  
列出可以添加到“关系图”窗格中的用户定义的函数。 若要添加某个函数，请选择该函数，再单击“添加”  。 若要同时添加多个函数，请选中这些函数，再单击“添加”  。  
  
**本地表**  
列出由查询创建的表而不是数据库中的表。  
  
**同义词**  
列出可以添加到“关系图”窗格中的同义词。 若要添加某个同义词，请选择该同义词，再单击“添加”  。 若要同时添加多个同义词，请选中这些同义词，再单击“添加”  。  
  
|图标|对象类型|  
|--------|---------------|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi1.gif "Visual Database Tools 图标")|表|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi2.gif "Visual Database Tools 图标")|查询或视图|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi3.gif "Visual Database Tools 图标")|被链接表|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dvudficon.gif "Visual Database Tools 图标")|用户定义函数|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi5.gif "Visual Database Tools 图标")|链接视图|  
  
每个矩形显示表或表值对象的数据列。 显示于列名旁边的复选框和符号指示如何在查询中使用列。 工具提示显示列的数据类型和大小等信息。  
  
下表列出了各个表或表值对象的矩形中所使用的复选框和符号：  
  
|复选框或符号|说明|  
|-----------------------|---------------|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi7.gif "Visual Database Tools 图标")<br /><br />![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi8.gif "Visual Database Tools 图标")<br /><br />![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbi9.gif "Visual Database Tools 图标")<br /><br />![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbia.gif "Visual Database Tools 图标")|指定某个数据列是否出现在查询结果集内（“选择”查询），或者是否用于“更新”、“插入源”、“生成表”或“插入到”查询中。 选择要添加到结果中的列。 如果选择“(所有列)”  ，则所有数据列都将出现在输出中。<br /><br />与复选框一起使用的图标会根据要创建的查询类型而更改。 在创建“删除”查询时，不能选择单个列。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbib.gif "Visual Database Tools 图标")<br /><br />![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbic.gif "Visual Database Tools 图标")|表示数据列用于对查询结果进行排序（是 ORDER BY 子句的一部分）。 如果排序顺序为升序，则图标显示为 A-Z；如果排序顺序为降序，则图标显示为 Z-A。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbid.gif "Visual Database Tools 图标")|表示数据列用于在聚合查询中创建分组结果集（是 GROUP BY 子句的一部分）。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbie.gif "Visual Database Tools 图标")|表示数据列包含在查询的搜索条件中（是 WHERE 或 HAVING 子句的一部分）。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbif.gif "Visual Database Tools 图标")|表示数据列的内容将进行汇总以便输出（包含在 SUM、AVG 或其他聚合函数中）。|  
  
> [!NOTE]  
> 如果您对表或表值对象没有足够的访问权限，或者数据库驱动程序无法返回其有关信息，则查询和视图设计器将不显示该表或表值对象的数据列。 在这种情况下，查询和视图设计器将只显示表或表结构对象的标题栏。  
  
## <a name="joined-tables-on-the-diagram-pane"></a>“关系图”窗格上联接的表  
如果查询涉及联接，在联接所涉及的数据列之间将显示一条联接线。 如果没有显示联接的数据列（例如，表或表值对象窗口已最小化或者此联接涉及表达式），则查询和视图设计器会将联接线放在表示表或表值对象的矩形的标题栏中。 查询和视图设计器为每个联接条件显示一条联接线。  
  
联接线中间的图标形状指示表或表结构对象的联接方式。 如果联接子句使用等于 (=) 以外的运算符，则该运算符将显示在联接线图标中。 下表列出可在联接线中显示的图标：  
  
|联接线图标|说明|  
|------------------|---------------|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbih.gif "Visual Database Tools 图标")|内部联接（使用等号创建）。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools 图标")|基于“大于”运算符的内部联接。 （在联接线图标中显示的运算符反映了在联接中使用的运算符。）|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbij.gif "Visual Database Tools 图标")|外部联接，其中包括左侧表示的表中的所有行，即使它们在相关表中没有匹配行。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbik.gif "Visual Database Tools 图标")|外部联接，其中包括右侧表示的表中的所有行，即使它们在相关表中没有匹配行。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbil.gif "Visual Database Tools 图标")|完全外部联接，其中含有两个表中的所有行，即使它们在相关表中没有匹配行。|  
  
联接线末端的图标表示联接的类型。 下表列出联接的类型以及可在联接线末端显示的图标：  
  
|联接线末端的图标|说明|  
|-----------------------------|---------------|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbim.gif "Visual Database Tools 图标")|一对一联接|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbin.gif "Visual Database Tools 图标")|一对多联接|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbio.gif "Visual Database Tools 图标")|查询和视图设计器无法确定联接类型|  
  
## <a name="see-also"></a>另请参阅  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[“条件”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
