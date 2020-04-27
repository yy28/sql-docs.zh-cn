---
title: 签出文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- Visual Studio.SourceControl.CheckOutDialog
helpviewer_keywords:
- checking out files
ms.assetid: cc033727-51bb-4b58-a12b-8977ce61ff56
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bde4d7fa738bdc952abc936ea13caa7225887ad6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62786742"
---
# <a name="check-out-files"></a>签出文件
  除非已经将 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 环境配置为允许编辑已签入的文件，否则，必须先签出该文件后才可以进行修改。 签出文件时，该文件版本的副本将复制到本地磁盘，并删除文件的只读属性。  
  
 可以独占或以共享模式签出文件。 如果以独占模式签出文件，则其他任何用户均不能签出该文件，直到您将该文件签入。 当以共享模式签出文件时，其他用户可以签出并修改该文件，当您签入文件时，可能需要将您已经签出的版本与其他用户创建的版本进行合并。  
  
 使用 "**签出**" 命令签出源代码管理的项目和文件。 如果使用此命令签出解决方案或项目，则也将签出解决方案或项目中的所有文件。但是，签出单个源代码文件不会导致签出它所属的项目或解决方案。  
  
> [!NOTE]  
>  如果你[!INCLUDE[msCoName](../includes/msconame-md.md)]的项目的 Visual SourceSafe 数据库配置为允许多次签出，并且你想要以独占方式签出文件，则必须先清除 "**高级签出选项**" 对话框中的 "**允许多个签**出" 选项，然后才能签出该文件。 必须重新启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，该设置才能生效。  
  
### <a name="to-check-out-a-file"></a>签出文件  
  
1.  在解决方案资源管理器中，选择项目或文件。  
  
2.  在 "**文件**" 菜单上，指向 "**源代码管理**"，然后单击 "**签出以进行编辑**"。  
  
3.  如果显示 "**签出以进行编辑**" 对话框，请选择所需的项，然后单击 "**签出**"。如果已将[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]环境配置为不显示 "**签出**" 对话框，则会立即签出在解决方案资源管理器中选择的项以及它们可能具有的任何子项。  
  
     **退房**  
     签出所有选定项。  
  
     **“列”**  
     标识要显示的列及其显示顺序。  
  
     **备注**  
     指定与该签出操作关联的注释。  
  
     **签出项时不显示“签出”对话框**  
     在签出操作过程中取消该对话框。  
  
     **平面视图**  
     将签出的项在其源代码管理连接下显示为平面列表。  
  
     **编辑**  
     修改项但不将其签出。仅**Edit**当你已[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]将配置为支持编辑签入文件时，才会显示 "编辑" 按钮。  
  
     **名称**  
     显示可签出的项的名称。 选定的项旁边还会显示复选框。 如果不希望签出特定的项，请清除其复选框。  
  
     **选项**  
     单击按钮右侧的箭头时，显示源代码管理插件特定的签出选项。  
  
     **进行**  
     对显示的列进行排序。  
  
     **树视图**  
     显示所签出项的文件夹和文件层次结构。  
  
## <a name="see-also"></a>另请参阅  
 [编辑签入的文件](../../2014/database-engine/edit-checked-in-files.md)   
 [编辑时自动签出文件](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [撤消签出](../../2014/database-engine/undo-checkouts.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  
