---
title: 在“结果”窗格中删除行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a82a7232559cd8761ae3af66a9accc0bc307552
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066176"
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>在“结果”窗格中删除行 (Visual Database Tools)
  如果希望删除数据库中的记录，请在“结果”窗格中删除相应的行。 如果希望删除所有行，则可以使用“删除”查询。 有关详细信息，请参阅 [创建“删除”查询 (Visual Database Tools)](visual-database-tools.md)。 如果只希望将行从“结果”窗格中移除，请更改查询的条件。 有关详细信息，请参阅 [指定搜索条件 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)。  
  
### <a name="to-delete-a-row-or-rows"></a>删除一行或多行  
  
1.  在“结果”窗格中选中要删除的行左侧的框。  
  
2.  按 Delete。  
  
3.  在要求确认的消息框中单击“是”  。  
  
> [!CAUTION]  
>  以这种方式删除的行将从数据库中永久移除并且不能恢复。  
  
> [!NOTE]  
>  如果所选行中有任意行无法从数据库中删除，则这些行都不会删除，并且系统将显示消息，指示无法删除哪些行。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Visual Database Tools 创建删除查询&#41;](visual-database-tools.md)   
 [指定搜索条件 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
