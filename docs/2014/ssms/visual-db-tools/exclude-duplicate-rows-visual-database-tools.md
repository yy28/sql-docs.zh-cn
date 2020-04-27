---
title: 排除重复行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63ec11b8575017ffbb3a1b1468ef3150a20326e2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63028345"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>排除重复行 (Visual Database Tools)
  如果希望在结果集中看到的值都是唯一的，则可指定要从结果集中排除重复项。  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>从结果集中排除重复行  
  
1.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“属性”  。  
  
2.  在“属性”窗口，单击“DISTINCT 值”  ，再将其值设置为“是”  。  
  
     查询和视图设计器将在 SQL 语句中显示列的列表之前插入关键字 DISTINCT。  
  
    > [!NOTE]  
    >  如果使用 DISTINCT 关键字，则可能无法在结果窗格中修改结果集。  
  
## <a name="see-also"></a>另请参阅  
 [指定 Visual Database Tools &#40;搜索条件&#41;](visual-database-tools.md)   
 [对查询结果进行排序和分组 (Visual Database Tools)](sort-and-group-query-results-visual-database-tools.md)  
  
  
