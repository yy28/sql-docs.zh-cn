---
title: 还原选项 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], restoring
- restoring databases [Analysis Services]
ms.assetid: 75c73802-f321-4671-afc7-54505d62c013
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a754ac9650c94511e8576a8a05e0b81fb38138a3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073089"
---
# <a name="restore-options"></a>还原选项
  可通过多种方式还原 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，但都要求您具有服务器计算机和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的管理员权限。 若要还原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，可在 **中打开** “还原数据库” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框，选择相应的选项配置，再从该对话框运行还原。 也可以使用文件中已指定的设置创建一个脚本，然后，可保存该脚本，并按需要的频率运行。 这样一来，就可使用 XMLA 来完成还原，如下所述。  
  
## <a name="restoring-databases-using-xmla"></a>使用 XMLA 还原数据库  
 使用 XMLA Restore 命令，可基于 .abf 文件运行还原，从而实现还原过程的自动化。 Restore 命令具有许多属性，可设置这些属性以指定安全性定义、应存储远程分区的位置以及 OLAP (ROLAP) 关系对象的重定位。 有关详细信息，请参阅 [Restore 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户必须具有以下角色之一： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员，或对要还原的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
## <a name="see-also"></a>请参阅  
 [“还原数据库”对话框（Analysis Services - 多维数据）](../restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [备份和还原 Analysis Services 数据库](backup-and-restore-of-analysis-services-databases.md)   
 [Restore 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [备份、还原和同步数据库 (XMLA)](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
