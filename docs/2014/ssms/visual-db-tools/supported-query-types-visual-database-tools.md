---
title: 支持的查询类型 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 543c70df2cda31251eb193f1acf04ab46ec8cddf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065847"
---
# <a name="supported-query-types-visual-database-tools"></a>支持的查询类型 (Visual Database Tools)
  可以在[查询和视图设计器](visual-database-tools.md)的“关系图”窗格和“条件”窗格（图形化窗格）中创建以下类型的查询：  
  
-   **“选择”查询** 从一个或多个表或视图中检索数据。 此类型的查询将创建一个 SQL SELECT 语句。  
  
-   **插入结果** 通过将现有行作为新行从一个表复制到另一个表或同一个表中，从而创建新行。 此类型的查询将创建一个 SQL INSERT INTO...SELECT 语句。  
  
-   **插入值** 创建新行并将值插入指定列。 此类型的查询将创建一个 SQL INSERT INTO...VALUES 语句。  
  
-   **“更新”查询** 更改表中一个或多个现有行中单个列的值。 此类型的查询将创建一个 SQL UPDATE...SET 语句。  
  
-   **“删除”查询** 从表中移除一行或多行。 此类型的查询将创建一个 SQL DELETE 语句。  
  
    > [!NOTE]  
    >  “删除”查询会从表中移除整行。 如果想删除单个数据列中的值，请使用“更新”查询。  
  
-   **“生成表”查询** 创建新表，并通过将查询结果复制到该表在表中创建行。 此类型的查询将创建一个 SQL SELECT...INTO 语句。  
  
 除了可以使用图形化窗格创建的查询之外，还可以向 SQL 窗格中输入任何 SQL 语句，例如“联合”查询。  
  
 在使用 SQL 语句创建无法在图形化窗格中显示的查询时，查询和视图设计器会将这些图形化窗格显示为灰色，以表示它们不再反映正在创建的查询。 不过，变成灰色的窗格仍然是活动的，而且在许多情况下，仍可以在这些窗格中对查询进行修改。 如果所做的更改产生的查询可以在图形化窗格中显示，则这些窗格将不再显示为灰色。  
  
## <a name="see-also"></a>请参阅  
 [设计查询和视图操作指南主题&#40;可视化数据库工具&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [查询类型 (Visual Database Tools)](types-of-queries-visual-database-tools.md)  
  
  
