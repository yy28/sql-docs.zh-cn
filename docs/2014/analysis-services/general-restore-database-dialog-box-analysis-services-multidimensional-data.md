---
title: 常规 （还原数据库对话框） (Analysis Services-多维数据) |Microsoft 文档
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
- sql12.asvs.restoredbdialog.f1
ms.assetid: 319e7ef5-c9c7-4e50-8690-02a90aed006f
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4969ceb840f6c3d80b4d0854d582e695c109806b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126418"
---
# <a name="general-restore-database-dialog-box-analysis-services---multidimensional-data"></a>常规（“还原数据库”对话框）（Analysis Services - 多维数据）
  在 **中，可以使用** “还原数据库” **对话框的** “常规” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 页指定在还原 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库时使用的备份文件和常规设置。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
 **在还原数据库对话框中显示常规页**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的“数据库”文件夹，或“对象资源管理器”中的数据库，单击“还原”，然后在“选择页”下单击“常规”。  
  
## <a name="options"></a>“常规”  
 **脚本**  
 创建还原脚本，该脚本基于在对话框中选定的选项。 还原脚本是用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 脚本语言 (ASSL) 编写的。  
  
 默认情况下，单击 **“脚本”** 图标会将还原脚本发送到新的查询窗口。  
  
 单击 **“脚本”** 箭头将显示一个菜单，您可以使用此菜单选择将还原脚本发送到的位置：  
  
-   发送到新查询窗口（默认值）。  
  
-   发送到文件。  
  
-   发送到剪贴板。  
  
-   发送到作业。  
  
 **还原数据库**  
 选择要还原的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
 **从备份文件**  
 选择从中还原所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的备份文件。  
  
 **“浏览”**  
 单击可显示“定位数据库文件”对话框，并选择要使用的备份文件的路径和文件名。 有关“定位数据库文件”对话框的详细信息，请参阅[“定位数据库文件”对话框（Analysis Services - 多维数据）](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **允许覆盖数据库**  
 选择此选项允许 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 还原所选备份文件的内容来覆盖所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中的现有对象。  
  
 **包括安全信息**  
 选择此选项可以将备份文件中存储的所有安全信息复制到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
 如果选择此选项，则可以从通过选择此选项启用的下拉列表中选择安全信息。 可用选项包括：  
  
|选项|Description|  
|------------|-----------------|  
|**将所有复制**|还原备份文件中包含的数据库角色以及与这些角色关联的用户帐户。|  
|**跳过成员身份**|还原备份文件中包含的数据库角色，但不还原与这些角色关联的用户帐户。|  
  
 **密码**  
 如果对备份文件进行了加密，请键入用于加密备份文件的密码。  
  
## <a name="see-also"></a>请参阅  
 [还原数据库对话框&#40;Analysis Services-多维数据&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [分区&#40;还原数据库对话框&#41; &#40;Analysis Services-多维数据&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [备份和还原 Analysis Services 数据库](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  