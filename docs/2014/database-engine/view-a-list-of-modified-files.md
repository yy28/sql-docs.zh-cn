---
title: 查看已修改文件的列表 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "62773423"
---
# <a name="view-a-list-of-modified-files"></a>查看已修改的文件列表
  您可以使用 "**挂起签入**" 窗口显示当前解决方案中的已签出文件的列表，并通过单击一次按钮签入这些文件。  
  
### <a name="to-view-a-list-of-modified-files"></a>查看已修改文件的列表  
  
1.  在 "**视图**" 菜单上，单击 "**挂起签入**"。  
  
2.  若要签入选定的文件，请单击 "**签入**"。 或者，您可以将**挂起的签入**窗口停靠在[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]环境的右侧，以便您可以在完成工作时签入文件。  
  
     **登记**  
     签入解决方案。  
  
     **备注**  
     将纯文本注释与挂起的签入相关联。 对于项目的每一个版本，都会创建一个与之关联的注释，该注释存储在源代码管理数据库中。  
  
     **选项**  
     指定在单击 "**签入**" 按钮时源控件应执行的操作。  
  
    -   **保持所有签出**  
  
         指定应将所做的更改写入源代码管理提供程序，但是这些文件应保持签出状态。  
  
     **进行**  
     指定“项”列表中所显示的列的排序顺序。  
  
     **“列”**  
     显示可添加到窗口“项”列表中的列的列表。  
  
     **树视图**  
     显示要签入的解决方案或项目的文件夹和文件层次结构。  
  
     **平面视图**  
     在其源代码管理连接下显示要签入的文件。  
  
     **版本比较**  
     打开 "Visual SourceSafe**差异选项**" 对话框，该对话框将您的开发环境项目中的选定文件与任何其他所选文件进行比较，并显示差异（如果有）。  
  
     **撤消签出**  
     反转 "**挂起签入**" 窗口中选定的所有项的签出。  
  
     **名称**  
     显示可签入的项的列表。 这些项旁边所显示的复选框将处于选中状态。 如果您不希望签入特定项，请清除其旁边的复选框。  
  
## <a name="see-also"></a>另请参阅  
 [管理签入](../../2014/database-engine/manage-checkins.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  
