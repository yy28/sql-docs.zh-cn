---
title: "保存关系图中所选的表 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: saving tables
ms.assetid: 86943b49-48f3-432c-8021-928c13edfbcf
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13e47d349680589c14f2804629c1417872f49265
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="save-selected-tables-on-a-diagram-visual-database-tools"></a>保存关系图中所选的表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 如果不希望保存在数据库关系图中所做的全部更改，则可以保存特定表或一组表。  
  
### <a name="to-save-selected-tables"></a>保存所选的表  
  
1.  在数据库关系图中，选择要保存的表。  
  
2.  在“文件”菜单中，选择“保存选择”。  
  
3.  保存所做的选择时，“保存”对话框将显示数据库中会被更新的表列表。  
  
    如果希望在继续操作前将表列表以文本文件形式保存到项目目录中，请选择“保存文本文件”。  
  
4.  在“保存”对话框中，确认表列表，再选择“是”保存这些表。  
  
    > [!NOTE]  
    > 表的列表除了包含所选的表之外，可能还包含其他表。 例如，如果更改了某列的数据类型，而该列参与了与另一个表的关系，那么这两个表都将包括在此列表中。  
  
## <a name="see-also"></a>另请参阅  
[使用数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
