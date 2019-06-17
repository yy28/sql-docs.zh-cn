---
title: 查看已修改的文件的列表 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckinWindow
helpviewer_keywords:
- listing modified files
- modified files list [SQL Server]
- checking in files
ms.assetid: 1b053719-8500-4300-a169-fffca5801dd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35062e6dfa339d0cd37f3905dc801f0f47becba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773423"
---
# <a name="view-a-list-of-modified-files"></a>查看已修改的文件列表
  可以使用**挂起的签入**窗口随时显示时间在当前解决方案中，签出文件的列表和签入这些文件一次按钮单击。  
  
### <a name="to-view-a-list-of-modified-files"></a>若要查看的已修改的文件列表  
  
1.  上**视图**菜单上，单击**挂起的签入**。  
  
2.  若要检查所选文件中，单击**签入**。 或者，可以停靠**挂起的签入**窗口的右侧[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]环境，以便您可以签入文件时已完成工作。  
  
     **Check In**  
     签入解决方案。  
  
     **注释**  
     将纯文本注释与挂起的签入相关联。 对于项目的每一个版本，都会创建一个与之关联的注释，该注释存储在源代码管理数据库中。  
  
     **选项**  
     指定当您单击时，应执行源代码管理操作**签入**按钮。  
  
    -   **保持所有签出**  
  
         指定应将所做的更改写入源代码管理提供程序，但是这些文件应保持签出状态。  
  
     **Sort**  
     指定“项”列表中所显示的列的排序顺序。  
  
     **“列”**  
     显示可添加到窗口“项”列表中的列的列表。  
  
     **树视图**  
     显示要签入的解决方案或项目的文件夹和文件层次结构。  
  
     **平面视图**  
     正在签入的文件显示为其源代码管理连接下的平面列表。  
  
     **比较版本**  
     打开 Visual SourceSafe**差异选项**对话框中，该比较所选的任何其他文件在开发环境项目中所选的文件，并显示不同的内容，如果有的话。  
  
     **撤消签出**  
     反转对选择中的所有项的签出**挂起的签入**窗口。  
  
     **名称**  
     显示可签入的项的列表。 这些项旁边所显示的复选框将处于选中状态。 如果您不希望签入特定项，请清除其旁边的复选框。  
  
## <a name="see-also"></a>请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  
