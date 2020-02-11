---
title: 将脚本迁移到 VSTA |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cb44a7b635e24c0c2e3266c1cca98a9c4f6a347c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093988"
---
# <a name="migrate-scripts-to-vsta"></a>将脚本迁移到 VSTA
  将包升级[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]会将任何脚本任务或脚本组件中的脚本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]迁移到 Tools for Applications （VSTA）。 VSTA 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用的脚本环境。 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中，的脚本编写[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]环境[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]适用于应用程序（VSA）。  
  
 如果脚本任务或脚本组件中的脚本引用接口，您在升级包之前可能必须修改这些引用。 否则，将无法升级包或者将无法验证脚本，具体取决于所使用的升级方法。 若要修改这些引用，请将对 IDTS*xxx*90 接口的引用替换为对相应的 IDTS*xxx*100 接口的引用。  
  
 有关如何迁移脚本和升级包的详细信息，请参阅[upgrade Integration Services 软件包](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
## <a name="understanding-migration-failures"></a>了解迁移失败  
 在迁移脚本时，脚本可能会由于以下原因之一而失败：  
  
-   VSA 脚本的入口点已重命名。  
  
     入口点在 VSTA 项目中的 `ScriptMain` 类中指定一种方法，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 运行时会将该方法作为脚本任务代码的入口点来调用。 
  `ScriptMain` 类是由脚本模板生成的默认类。  
  
-   在 VSA 脚本中，没有入口点或者有多个入口点。  
  
-   无法添加程序集引用。  
  
-   已经将 `ScriptMain` 类修改为从 `ScriptObjectModelSSIS` 类以外的其他类中继承。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]不支持多重继承。  
  
 不能将使用[!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)]的 VSA 脚本转换为使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]的 VSTA 脚本。 但是，你可以创建一个使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]的新的 VSTA 脚本。 有关详细信息，请参阅[脚本任务的编码和调试](../../integration-services/control-flow/script-task.md)和[脚本组件的编码和调试](../../integration-services/data-flow/transformations/script-component.md)。  
  
## <a name="see-also"></a>另请参阅  
 [用脚本扩展包](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  
