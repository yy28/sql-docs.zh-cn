---
title: 备份数据库对话框 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 64e8b814cab69ca66127f28b55062232e45a60fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027341"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>“备份数据库”对话框（Analysis Services - 多维数据）
  可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的“备份数据库”对话框，使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 备份文件 (.abf) 格式将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库备份到备份文件中。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行备份命令的用户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
 **若要显示备份数据库对话框**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的“数据库”文件夹或“对象资源管理器”中的数据库，然后单击“备份”。  
  
## <a name="options"></a>“常规”  
 **脚本**  
 创建备份脚本，该脚本基于在对话框中选定的选项。 还原脚本是用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 编写的。  
  
 默认情况下，单击 **“脚本”** 图标会将备份脚本发送到新的查询窗口。  
  
 单击 **“脚本”** 箭头将显示一个菜单，您可以使用此菜单选择将备份脚本发送到的位置：  
  
-   发送到新查询窗口（默认值）。  
  
-   发送到文件。  
  
-   发送到剪贴板。  
  
-   发送到作业。  
  
 **“数据库”**  
 显示当前所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的名称。  
  
 **“备份文件”**  
 键入要使用的备份文件的完整路径和文件名。  
  
 **“浏览”**  
 单击可显示“文件另存为”对话框，并选择要使用的备份文件的路径和文件名。 有关“文件另存为”对话框的详细信息，请参阅[“文件另存为”对话框（Analysis Services - 多维数据）](save-file-as-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **允许覆盖文件**  
 选择此选项可覆盖现有备份文件或远程备份文件（如果存在）。  
  
> [!NOTE]  
>  如果未选择此选项，并且“备份文件”中指定的备份文件或“远程备份文件”中指定的远程备份文件存在，则会出现错误。  
  
 **应用压缩**  
 选择此选项可压缩备份文件和远程备份文件（如果指定）的内容。  
  
 **加密备份文件**  
 选择此选项可使用“密码”中所提供密码加密备份文件。  
  
 **密码**  
 键入加密备份文件和远程备份文件（如果指定）时所使用的密码。  
  
> [!NOTE]  
>  只有在选择“加密备份文件”时，才会启用此选项。  
  
 **确认密码**  
 键入在“密码”中所输入的密码，以确认备份文件和远程备份文件（如果指定）的密码。  
  
> [!NOTE]  
>  只有在选择“加密备份文件”时，才会启用此选项。  
  
 **备份远程分区**  
 选择此选项可将远程分区的位置信息和数据包含在备份文件中。  
  
> [!NOTE]  
>  只有当前所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库使用远程分区时，才会启用此选项。  
  
 **远程分区备份位置**  
 显示与所选数据库关联的远程分区的位置，以及用于备份远程分区的数据和元数据的远程备份文件。 可用的列包括：  
  
|“列”|Description|  
|------------|-----------------|  
|**Server**|显示管理远程分区的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。|  
|**“数据库”**|显示包含远程分区的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。|  
|**分区列表**|显示 **“数据库”** 中显示的数据库所包含的远程分区列表。|  
|**远程备份文件**|键入要使用的远程备份文件的完整路径和文件名，或单击省略号按钮 (**...**) 以显示“文件另存为”对话框，再选择要使用的远程备份文件的路径和文件名。 有关“文件另存为”对话框的详细信息，请参阅[“文件另存为”对话框（Analysis Services - 多维数据）](save-file-as-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [备份和还原 Analysis Services 数据库](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  