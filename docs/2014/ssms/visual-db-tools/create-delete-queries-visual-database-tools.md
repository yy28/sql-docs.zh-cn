---
title: 创建删除查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- row removal [SQL Server], Delete query
- Delete query
- queries [SQL Server], types
- removing rows
- removing data
- data deletions [SQL Server]
- deleting rows
- deleting data
ms.assetid: 0db3af43-1ec4-48c8-b769-2bb9c76d3434
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1103e1715c01cfc868c59af17ee0f95fa7cedff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62661681"
---
# <a name="create-delete-queries-visual-database-tools"></a>创建删除查询 (Visual Database Tools)
  您可以通过使用“删除”查询来删除表中的所有行。  
  
> [!NOTE]  
>  删除表中的所有行会清除表中的数据，但不会删除表本身。 若要从数据库中删除表，请在对象资源管理器中右键单击该表，再单击“删除”  。  
  
 在创建“删除”查询时，“条件”窗格将发生相应变化以反映可用于删除行的选项。 因为不在“删除”查询中显示数据，所以将移除“输出”、“排序方式”和“排序顺序”列。 此外，因为无法指定要删除的单个列，所以在代表表或表值对象的矩形中，将移除列名旁边的复选框。  
  
 如果查询和视图设计器不能删除一个或多个行，则将不会删除任何一个行，并且您将收到一条消息，指出哪个（些）行包含不能从数据库中删除的信息。  
  
> [!CAUTION]  
>  无法撤消执行“删除”查询的操作。 作为预防措施，请在执行“删除”查询之前备份数据。  
  
### <a name="to-create-a-delete-query"></a>创建“删除”查询  
  
1.  将要从中删除行的表添加到“关系图”窗格中。  
  
2.  在“查询设计器”  菜单中，指向“更改类型”  ，再单击“删除”  。 **注意** 如果启动“删除”查询时，在“关系图”窗格中显示有多个表，则查询和视图设计器将显示[“删除表”对话框](visual-database-tools.md)，以提示你选择要从中删除行的表名。  
  
 在执行“删除”查询时，不会在 [“结果”窗格](results-pane-visual-database-tools.md)中报告任何结果。 但是，会显示一条消息，指示已删除的行数。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Database Tools &#40;支持的查询类型&#41;](supported-query-types-visual-database-tools.md)   
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
