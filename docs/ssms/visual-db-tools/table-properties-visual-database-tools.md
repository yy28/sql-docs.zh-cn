---
title: 表属性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5534fdf65543e651b52373629c81010d75cab449
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098132"
---
# <a name="table-properties-visual-database-tools"></a>表属性 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果您在表设计器中右键单击，再选择“属性”，则会在“属性”窗口中显示这些属性。 除非另行说明，否则在选定表后可以在“属性”窗口中编辑这些属性。  
  
> [!NOTE]  
> 如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。  
  
## <a name="show-table-properties-in-table-designer"></a>在表设计器中显示表属性  
  
> [!NOTE]  
> 本主题中的属性按类别排序，而不是按字母顺序排序。  
  
**标识类别**  
展开此项可显示“名称”  、“说明”  和“架构”  的属性。  
  
**名称**  
显示表的名称。 若要编辑名称，请在文本框中键入相应的内容。  
  
> [!CAUTION]  
> 如果现有查询、视图、用户定义函数、存储过程或程序引用该表，则对名称的修改将使这些对象无效。  
  
**数据库名称**  
显示所选表的数据源的名称。  
  
**Description**  
显示所选表的说明。 若要查看或编辑完整的说明，请单击相应的说明，再单击属性右侧的省略号 (…)  。  
  
**架构**  
显示此表所属的架构的名称。 （仅适用于 Microsoft SQL Server。）  
  
**服务器名称**  
显示用于数据源的服务器的名称。  
  
**表设计器类别**  
展开此项可显示“标识列”  、“可编制索引”  和“是复制的”  的属性。  
  
**标识列**  
显示用作表的标识列的列。 若要更改标识列，请从下拉列表中进行选择。 该列表中只显示数值数据类型的列。  
  
**可编制索引**  
显示该表是否可以索引。 如果表不可索引，则可能是因为您不是该表的所有者或因为该表包含具有 text、ntext 或 image 数据类型的列。  
  
**是复制的**  
显示是否在另一个位置复制了该表。  
  
**常规数据空间规范类别**  
展开此项可显示“（数据空间类型）”  、“文件组或分区方案名称”  和“分区列列表”  的属性。  
  
**(数据空间类型)**  
显示是使用文件组还是使用分区方案存储此表。  
  
**文件组或分区方案名称**  
显示文件组或分区方案的名称。  
  
**分区列列表**  
通过此项可访问“分区列列表”  对话框。  
  
**行 GUID 列**  
显示由 Microsoft SQL Server 用作表的 ROWGUID 列的列。 若要更改 ROWGUID 列，请从下拉列表中进行选择。 （仅适用于 SQL Server 7.0 或更高版本。）  
  
**Text/Image 文件组**  
提供一个下拉列表，您可以从中为具有 text 或 image 数据类型的列选择文件组。 如果该表是使用分区方案存储的，则将此字段保留为空。  
  
## <a name="see-also"></a>另请参阅  
[设计表 (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
