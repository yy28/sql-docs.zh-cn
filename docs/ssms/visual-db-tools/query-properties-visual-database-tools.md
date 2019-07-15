---
title: 查询属性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 44be7c64358828c7e5c043a8b5180a22c0515987
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67687478"
---
# <a name="query-properties-visual-database-tools"></a>查询属性 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
当您在查询和视图设计器中打开查询时，将在“属性”窗口中显示以下属性。 除非另行说明，否则这些属性都可以在“属性”窗口中编辑。  
  
> [!NOTE]  
> 本主题中的属性按类别排序，而不是按字母顺序排序。  
  
## <a name="options"></a>选项  
**标识类别**  
展开此项可显示“名称”  属性。  
  
**名称**  
显示当前查询的名称。 无法在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中更改。  
  
**Database Name**  
显示所选表的数据源的名称。  
  
**服务器名称**  
显示用于数据源的服务器的名称。  
  
**查询设计器类别**  
展开此项可显示剩余的属性。  
  
**目的表**  
指定要向其中插入数据的表的名称。 如果正在创建“插入”查询或“生成表”查询，则会显示此列表。 对于“插入”查询，请从列表中选择表名。  
  
对于“生成表”查询，请键入新表的名称。 若要在另一个数据源中创建目的表，请指定完全限定的表名，包括目标数据源名称、所有者（如有需要）以及表名。  
  
> [!NOTE]  
> 查询设计器不检查该名称是否已在使用中，也不检查您是否具有创建表的权限。  
  
**DISTINCT 值**  
指定查询将在结果集中筛选出重复值。 当只使用表中的部分列并且这些列可能包含重复值时，或者当联接两个或更多表的过程会在结果集中产生重复行时，此选项非常有用。 选择该选项等效于向 SQL 窗格内的语句中插入 DISTINCT 一词。  
  
**GROUP BY 扩展**  
指定对于基于聚合查询的查询，附加选项可用。 （仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。）  
  
**输出所有列**  
指定当前查询中所有表的全部列都将包含在结果集中。 选择此选项等效于在 SQL 语句的 SELECT 关键字后指定星号 (*) 代替单个列名。  
  
**查询参数列表**  
显示查询参数。 若要编辑这些参数，请单击相应属性，再单击该属性右侧的省略号 (…)  。 （仅适用于一般性的 OLE DB。）  
  
**SQL 注释**  
显示 SQL 语句的说明。 若要查看或编辑完整的说明，请单击相应的说明，再单击属性右侧的省略号 (…)  。 您的注释可以包含查询使用者和使用时间等信息。 （仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本的数据库。）  
  
**Top 规范类别**  
展开此项可显示“Top”  、“百分比”  、“表达式”  和“With Ties”  属性的属性。  
  
**(最前面)**  
指定查询将包括 TOP 子句，该子句只返回结果集中的前 n  行或前百分之 n  行。 默认情况下，查询将在结果集中返回前 10 行。  
  
使用此框可更改返回的行数或指定不同的百分比值。 （仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或更高版本。）  
  
**表达式**  
指定查询将返回的行数或行数百分比。 如果将“百分比”  设置为“是”，此数字表示查询将返回的行数百分比；如果将“百分比”  设置为“否”，则此数字表示要返回的行数。 （仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本。）  
  
**百分比**  
指定查询将只返回结果集中的前百分之 n  的行。 （仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本。）  
  
**With Ties**  
指定视图将包括 WITH TIES 子句。 如果视图包含 ORDER BY 子句和基于百分比的 TOP 子句，WITH TIES 将非常有用。 如果设置了该选项，并且百分比截止位置在一组行的中间，且这些行在 ORDER BY 子句中具有相同的值，则视图将会扩展，以包含所有这样的行。 （仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本。）  
  
## <a name="see-also"></a>另请参阅  
[使用参数进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
