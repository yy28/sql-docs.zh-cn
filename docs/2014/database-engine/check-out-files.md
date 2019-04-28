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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786742"
---
# <a name="check-out-files"></a>签出文件
  除非已经将 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 环境配置为允许编辑已签入的文件，否则，必须先签出该文件后才可以进行修改。 签出文件时，该文件版本的副本将复制到本地磁盘，并删除文件的只读属性。  
  
 可以独占或以共享模式签出文件。 如果以独占模式签出文件，则其他任何用户均不能签出该文件，直到您将该文件签入。 当以共享模式签出文件时，其他用户可以签出并修改该文件，当您签入文件时，可能需要将您已经签出的版本与其他用户创建的版本进行合并。  
  
 使用**签出**命令签出源代码管理的项目和文件。 如果您使用此命令签出解决方案或项目，还应结帐解决方案或项目中的所有文件。但是，签出单个源代码文件不会导致签出的项目或其所属的解决方案。  
  
> [!NOTE]  
>  如果[!INCLUDE[msCoName](../includes/msconame-md.md)]为你的项目的 Visual SourceSafe 数据库配置为允许多次签出，并且你想要签出文件以独占方式，您必须清除**允许多次签出**选项中**高级签出选项**之前签出文件的对话框。 必须重新启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，该设置才能生效。  
  
### <a name="to-check-out-a-file"></a>若要签出文件  
  
1.  在解决方案资源管理器中，选择项目或文件。  
  
2.  上**文件**菜单，依次指向**源代码管理**，然后单击**签出以进行编辑**。  
  
3.  如果**签出以进行编辑**对话框中，选择的项，并单击**签出**。如果已配置[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]环境不希望显示**签出**对话框中，选择解决方案资源管理器可能具有任何子级中的项都将立即签出。  
  
     **退房**  
     签出所有选定项。  
  
     **“列”**  
     标识要显示的列及其显示顺序。  
  
     **注释**  
     指定与该签出操作关联的注释。  
  
     **签出项时不显示签出对话框的**  
     在签出操作过程中取消该对话框。  
  
     **平面视图**  
     将签出的项在其源代码管理连接下显示为平面列表。  
  
     **编辑**  
     修改某个项，而不签出。**编辑**按钮将显示仅在具有[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]配置为支持编辑签入的文件。  
  
     **名称**  
     显示可签出的项的名称。 选定的项旁边还会显示复选框。 如果不希望签出特定的项，请清除其复选框。  
  
     **选项**  
     单击按钮右侧的箭头时，显示源代码管理插件特定的签出选项。  
  
     **Sort**  
     对显示的列进行排序。  
  
     **树视图**  
     显示所签出项的文件夹和文件层次结构。  
  
## <a name="see-also"></a>请参阅  
 [编辑签入的文件](../../2014/database-engine/edit-checked-in-files.md)   
 [自动签出文件编辑时](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [撤消签出](../../2014/database-engine/undo-checkouts.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  
