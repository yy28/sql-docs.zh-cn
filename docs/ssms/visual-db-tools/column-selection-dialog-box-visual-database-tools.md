---
title: "“列选择”对话框 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.columnselection
- vdtsql.chm:65548
ms.assetid: 479bae2c-fee0-4215-b424-1ab779a7e5ca
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ec9eb8b6cee6f16dc54f6d16a43d1f94f16a8e11
ms.contentlocale: zh-cn
ms.lasthandoff: 08/18/2017

---
# <a name="column-selection-dialog-box-visual-database-tools"></a>“列选择”对话框 (Visual Database Tools)
使用此对话框可以在数据库关系图中更改表的“自定义”视图。 “自定义”视图仅显示由用户标识的列属性。  
  
右键单击一个表并从快捷菜单中选择“修改自定义视图”后，将显示此对话框。  
  
## <a name="options"></a>选项  
**可用列**  
列出所选数据库表中的全部现有列。 在此列出的列取决于数据库表的属性和数据库的类型。 突出显示所需的列，再使用箭头按钮，可以将这些列移入“选定的列”框。  
  
**选定的列**  
显示当前为“自定义”视图定义的列属性。 使用箭头按钮可以将列属性添加到“选定的列”列表中或从该列表中移除列属性。  
  
**箭头控件**  
使用向上和向下箭头按钮可以在“选定的列”列表中上下移动突出显示的列。  
  
使用 > 箭头和 >> 箭头可以向自定义视图中添加一个或所有属性。  
  
使用 < 箭头和 << 箭头可以从自定义视图中删除一个或所有属性。  
  
**按默认值另存**  
用此对话框中所选的列替换默认的“自定义”视图。 如果未选择此项，则该对话框中所选的列只应用于数据库关系图中选定的表。  
  
**确定**  
保存“自定义”视图。  
  
**取消**  
取消对“自定义”视图的修改。  
  
## <a name="see-also"></a>另请参阅  
[使用数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[自定义关系图中显示的信息量 (Visual Database Tools)](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)  
  

