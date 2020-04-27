---
title: 签入文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckInDialog
helpviewer_keywords:
- checking in files
ms.assetid: 0657a387-8411-4406-bef9-d262a5bfa269
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5debb7c80e7365e67d8661709b09b16f5d25b7b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62812581"
---
# <a name="check-in-files"></a>签入文件
  若要将已修改的源代码管理文件用于其他用户，必须将这些文件签入到源代码管理中。 签入文件时，所签入的版本将写入源代码管理提供程序，并成为文件的最新版本。  
  
 您可以使用 "**签入**" 命令签入文件。 如果使用该命令签入解决方案或项目，将同时签入该解决方案或项目中的所有文件。 但是，签入单个源代码文件则不会将其所属的项目或解决方案一起签入。  
  
### <a name="to-check-in-a-file"></a>签入文件  
  
1.  在解决方案资源管理器中，右键单击要签入的文件，然后单击 "**签入**"。  
  
2.  如果出现 "**签入**" 对话框，请选择相应的选项，然后单击 **"确定"**。  
  
     **登记**  
     签入所有选定项。  
  
     **“列”**  
     标识要显示的列及其显示顺序。  
  
     **备注**  
     为签入操作添加相关注释。  
  
     **签入项时不显示“签入”对话框**  
     在签入操作过程中取消该对话框。  
  
     **平面视图**  
     将签入的文件在其源代码管理连接下显示为平面列表。  
  
     **名称**  
     显示要签入的项的名称。 所显示项旁边的复选框处于选中状态。 如果不希望签入特定的项，请清除其复选框。  
  
     **选项**  
     单击按钮右侧的箭头时，显示源代码管理插件特定的签入选项。  
  
     **进行**  
     对显示列进行排序。  
  
     **树视图**  
     显示所签入项的文件夹和文件层次结构。  
  
 如果已签入的文件不是以共享方式签出的文件的一部分，则 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 环境将立即签入该文件。 否则，它可能提示您将您的版本与其他用户创建的版本合并。  
  
## <a name="see-also"></a>另请参阅  
 [查看已修改文件的列表](../../2014/database-engine/view-a-list-of-modified-files.md)   
 [管理签入](../../2014/database-engine/manage-checkins.md)  
  
  
