---
title: 排除重复行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd83e73a0a7b94f7963531baa167669850ef0b8c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43807613"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>排除重复行 (Visual Database Tools)
  如果希望在结果集中看到的值都是唯一的，则可指定要从结果集中排除重复项。  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>从结果集中排除重复行  
  
1.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“属性”。  
  
2.  在“属性”窗口，单击“DISTINCT 值”，再将其值设置为“是”。  
  
     查询和视图设计器将在 SQL 语句中显示列的列表之前插入关键字 DISTINCT。  
  
    > [!NOTE]  
    >  如果使用 DISTINCT 关键字，则可能无法在结果窗格中修改结果集。  
  
## <a name="see-also"></a>请参阅  
 [指定搜索条件&#40;可视化数据库工具&#41;](visual-database-tools.md)   
 [对查询结果进行排序和分组 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)  
  
  
