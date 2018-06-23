---
title: 删除联接 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 75ee172ba9dcdb5761e7dd1eefe5722441c9983a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026446"
---
# <a name="remove-joins-visual-database-tools"></a>删除联接 (Visual Database Tools)
  如果您不希望表通过内部联接或外部联接进行联接，则可移除它们之间的联接。 例如，希望删除 [查询和视图设计器](visual-database-tools.md) 在两个表之间自动创建的联接。  
  
> [!NOTE]  
>  从查询中移除联接不会更改数据库中的基础关系。  
  
 如果两个联接表都是查询的一部分，而且您移除了它们之间的所有联接条件，那么生成的查询结果将变为这两个表的积，即变为 CROSS JOIN。  
  
### <a name="to-remove-a-join"></a>移除联接  
  
-   在“ [关系图](diagram-pane-visual-database-tools.md)”窗格中，选择要删除的联接的联接线，再按 Delete 键。 您可一次选择并删除多个联接线。  
  
 查询和视图设计器将删除联接线并相应地更改 [SQL 窗格](sql-pane-visual-database-tools.md)中的语句。  
  
## <a name="see-also"></a>请参阅  
 [自动联接表&#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md)   
 [手动联接表&#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md)   
 [使用联接进行查询 (Visual Database Tools)](query-with-joins-visual-database-tools.md)  
  
  