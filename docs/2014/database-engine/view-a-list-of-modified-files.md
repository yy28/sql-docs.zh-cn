---
title: 查看更改过的文件的列表 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VisualStudio.SourceControl.CheckinWindow
helpviewer_keywords:
- listing modified files
- modified files list [SQL Server]
- checking in files
ms.assetid: 1b053719-8500-4300-a169-fffca5801dd0
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: affad7b7830088a955794f4825a68e72f12fca96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028180"
---
# <a name="view-a-list-of-modified-files"></a>查看已修改的文件列表
  你可以使用**挂起签入**窗口以显示在所有时间在当前解决方案中，签出文件的列表和签入这些文件与单个按钮单击。  
  
### <a name="to-view-a-list-of-modified-files"></a>若要查看已修改文件的列表  
  
1.  上**视图**菜单上，单击**挂起签入**。  
  
2.  若要签入所选的文件时，请单击**签入**。 或者，你可以将停靠**挂起签入**窗口的右侧[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]环境，以便在完成时，你可以检查在文件中使用。  
  
     **登记**  
     签入解决方案。  
  
     **注释**  
     将纯文本注释与挂起的签入相关联。 对于项目的每一个版本，都会创建一个与之关联的注释，该注释存储在源代码管理数据库中。  
  
     **选项**  
     指定当你单击时，源代码管理应采取的操作**签入**按钮。  
  
    -   **保持所有签出**  
  
         指定应将所做的更改写入源代码管理提供程序，但是这些文件应保持签出状态。  
  
     **Sort**  
     指定“项”列表中所显示的列的排序顺序。  
  
     **“列”**  
     显示可添加到窗口“项”列表中的列的列表。  
  
     **树视图**  
     显示要签入的解决方案或项目的文件夹和文件层次结构。  
  
     **平面视图**  
     要签入的文件显示为其源控件连接下的平面列表。  
  
     **对版本进行比较**  
     打开 Visual SourceSafe**差异选项**对话框中，这将所选的文件中任何其他所选文件到你的开发环境项目比较，并显示你的差异，如果有的话。  
  
     **撤消签出**  
     反转中选定的所有项目的签出**挂起签入**窗口。  
  
     **名称**  
     显示可签入的项的列表。 这些项旁边所显示的复选框将处于选中状态。 如果您不希望签入特定项，请清除其旁边的复选框。  
  
## <a name="see-also"></a>请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  