---
title: "排除重复行 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2379c4f9decc04f5967bbc4be7b34874495097d5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>排除重复行 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 如果希望在结果集中看到的值都是唯一的，则可指定要从结果集中排除重复项。  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>从结果集中排除重复行  
  
1.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“属性”。  
  
2.  在“属性”窗口，单击“DISTINCT 值”，再将其值设置为“是”。  
  
    查询和视图设计器将在 SQL 语句中显示列的列表之前插入关键字 DISTINCT。  
  
    > [!NOTE]  
    > 如果使用 DISTINCT 关键字，则可能无法在结果窗格中修改结果集。  
  
## <a name="see-also"></a>另请参阅  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
