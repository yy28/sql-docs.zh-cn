---
title: 还原数据库对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Restore.f1
ms.assetid: a3990d47-55e2-424e-8eac-87edc937e806
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ced766942b0bba6c84985315907708d40565f763
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330417"
---
# <a name="restore-database-dialog-box-analysis-services---multidimensional-data"></a>“还原数据库”对话框（Analysis Services - 多维数据）
  可使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的“还原数据库”对话框，以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 备份文件 (.abf) 格式从备份文件中还原 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
 **若要显示还原数据库对话框**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的“数据库”文件夹或“对象资源管理器”中的数据库，然后单击“还原”。  
  
 **“还原数据库”** 对话框包含以下页。  
  
## <a name="pages"></a>页  
 **常规**  
 使用此页可以选择要还原的数据库、从中还原数据库的备份文件以及还原数据库时使用的常规选项和密码。 有关该页的详细信息，请参阅[常规（“还原数据库”对话框）（Analysis Services - 多维数据）](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **分区**  
 使用此页可以将本地分区还原到指定的位置，以及从远程备份文件还原远程分区。 有关该页的详细信息，请参阅[分区（“还原数据库”对话框）（Analysis Services - 多维数据）](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [备份和还原 Analysis Services 数据库](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
