---
title: 分区 （还原数据库对话框） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.partitions.f1
ms.assetid: 1ad4dde5-4651-4069-875c-7ab73cd8b4f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef5ec59980d267a8ead0f69aedb12c6eca5508dc
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639864"
---
# <a name="partitions-restore-database-dialog-box-analysis-services---multidimensional-data"></a>分区（“还原数据库”对话框）（Analysis Services - 多维数据）
  可以使用 **中的** “还原数据库” **对话框上的** “分区” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 页，指定还原本地分区的位置、是否还原远程分区以及在还原远程分区时使用的远程备份文件。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
 **若要显示还原数据库对话框中的分区页**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的“数据库”文件夹或**对象资源管理器**中的数据库，单击“还原”，然后在“选择页”下单击“分区”。  
  
## <a name="options"></a>选项  
 **脚本**  
 创建还原脚本，该脚本基于在对话框中选定的选项。 还原脚本是用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 编写的。  
  
 默认情况下，单击 **“脚本”** 图标会将还原脚本发送到新的查询窗口。  
  
 单击 **“脚本”** 箭头将显示一个菜单，您可以使用此菜单选择将还原脚本发送到的位置：  
  
-   发送到新查询窗口（默认值）。  
  
-   发送到文件。  
  
-   发送到剪贴板。  
  
-   发送到作业。  
  
 **将还原到原始位置**  
 选择此选项可以将备份文件中包含的本地分区还原到其原位置。  
  
 **选择不同的位置**  
 选择此选项可以指定要还原本地分区的其他位置。  
  
> [!NOTE]  
>  只有在多维数据集中为本地分区指定了默认位置之外的位置时，才可以更改本地分区的还原文件夹。  
  
 下面的网格（选择此选项后启用）用于指定每个本地分区的还原文件夹：  
  
|“列”|Description|  
|------------|-----------------|  
|**Cube**|显示包含本地分区的多维数据集的名称。|  
|**度量值组**|显示包含本地分区的度量值组的名称。|  
|**分区**|显示本地分区的名称。|  
|**大小(MB)**|显示本地分区的大小 (MB)。|  
|**原始文件夹**|显示存储本地分区的原始文件夹的名称。|  
|**还原文件夹**|键入本地分区的还原文件夹的名称，或单击省略号按钮 (**...**) 以显示“查找远程文件夹”对话框，再选择要使用的文件夹的路径。 有关“查找远程文件夹”对话框的详细信息，请参阅[“查找远程文件夹”对话框（Analysis Services - 多维数据）](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)。|  
  
 **还原远程分区**  
 选择此选项可以还原在远程备份文件中存储的远程分区。  
  
> [!NOTE]  
>  只有备份文件中包含对远程分区的引用时，才会启用此选项。  
  
 下面的网格（选择此选项后启用）用于指定每个本地分区的还原文件夹：  
  
|“列”|Description|  
|------------|-----------------|  
|**Server**|显示管理远程分区的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的名称。|  
|**数据源**|显示备份文件中数据源的名称，该数据源代表包含远程分区的数据库。|  
|**备份文件**|键入要使用的远程备份文件的完整路径和文件名，或单击省略号按钮 (**...**) 以显示“定位数据库文件”对话框，再选择要使用的远程备份文件的路径和文件名。 有关“定位数据库文件”对话框的详细信息，请参阅[“定位数据库文件”对话框（Analysis Services - 多维数据）](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)。|  
|**...**|单击此按钮可以显示“远程分区 - 高级设置”对话框，以便修改用于还原远程分区的高级选项，例如数据源的连接字符串。 有关“远程分区 - 高级设置”对话框的详细信息，请参阅[对话框（Analysis Services - 多维数据）](remote-partitions-advanced-settings-dialog-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>请参阅  
 [“还原数据库”对话框（Analysis Services - 多维数据）](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [常规&#40;还原数据库对话框&#41; &#40;Analysis Services-多维数据&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [备份和还原 Analysis Services 数据库](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
