---
title: 备份选项 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c2d6f719e6b37560e515558175cc3389072bc69
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="backup-options"></a>备份选项
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可通过多种方式备份 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，但都要求您具有服务器管理员和数据库管理员的权限。 您可以在 **中打开** “备份” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框，选择适当的选项配置，然后从该对话框本身运行备份。 或者，您可以使用文件中已指定的设置创建脚本；然后，可保存该脚本，根据需要定期运行。  
  
## <a name="backup-and-synchronize"></a>备份与同步  
 如果数据库位于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的远程实例中，可以使用同步功能将数据库备份到本地实例。 数据库的开发内部版本可以用这种方式移到生产环境。 您还可以使用基于文件的常规备份和还原功能将开发内部版本移到生产环境，但同步功能还可提供其他功能。 例如，对于开发计算机和生产计算机，您可以使用不同的安全设置；使用同步功能即可维护这些设置，并同步除角色之外的所有对象。 而且，对于源计算机和目标计算机不同的那些对象，同步功能还可以对其执行增量更新。 而使用备份/还原功能则无法实现这种增量备份。 有关详细信息，请参阅 [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)。  
  
> [!IMPORTANT]  
>  Analysis Services 服务帐户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的管理员角色，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
## <a name="see-also"></a>另请参阅  
 [备份数据库对话框 & #40;Analysis Services-多维数据 & #41;](http://msdn.microsoft.com/library/7811ce7d-6c37-4189-bfa6-ef36fb4932db)   
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Backup 元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [备份、 还原和同步数据库 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
