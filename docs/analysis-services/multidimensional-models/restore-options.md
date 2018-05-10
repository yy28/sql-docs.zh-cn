---
title: 还原选项 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3e70b5e15937b8f2c035339a7d1facfa7908ac08
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="restore-options"></a>还原选项
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可通过多种方式还原 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，但都要求您具有服务器计算机和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的管理员权限。 若要还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，可在 **中打开** “还原数据库” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框，选择相应的选项配置，再从该对话框运行还原。 也可以使用文件中已指定的设置创建一个脚本，然后，可保存该脚本，并按需要的频率运行。 这样一来，就可使用 XMLA 来完成还原，如下所述。  
  
## <a name="restoring-databases-using-xmla"></a>使用 XMLA 还原数据库  
 使用 XMLA Restore 命令，可基于 .abf 文件运行还原，从而实现还原过程的自动化。 Restore 命令具有许多属性，可设置这些属性以指定安全性定义、应存储远程分区的位置以及 OLAP (ROLAP) 关系对象的重定位。 有关详细信息，请参阅 [Restore 元素 (XMLA)](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
## <a name="see-also"></a>另请参阅  
 [“还原数据库”对话框（Analysis Services - 多维数据）](http://msdn.microsoft.com/library/a3990d47-55e2-424e-8eac-87edc937e806)   
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [还原元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [备份、 还原和同步数据库 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
