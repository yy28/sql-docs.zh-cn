---
title: 设置源代码管理选项 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Source_Control.Visual_SourceSafe
- VS.ToolsOptionsPages.Source_Control.General
- VS.ToolsOptionsPages.Source_Control.Environment
helpviewer_keywords:
- source controls [SQL Server Management Studio], options
ms.assetid: b2c6ca00-46f0-4f86-b067-07bae779c147
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a654932689785d96aaff049551faf19494c311a
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589891"
---
# <a name="set-source-control-options"></a>设置源代码管理选项
  在利用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中内置的源代码管理功能之前，应针对您工作中所处的各种环境对源代码管理选项进行配置。  
  
 使用配置源代码管理选项**选项**对话框可以配置一个或多个源代码管理角色。 组成角色的内容包括：对使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 时所采用设置的常规说明，以及与该设置关联的源代码管理选项。  
  
 例如，如果您是独立的数据库开发人员，则在将文件签入后使其继续保持签出状态，通常不会产生与其他用户的冲突。 因此，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 定义了“独立开发人员”角色。 对于此角色，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]会自动选择**保留签入时签出项**选项。  
  
 因为可以定义和自定义角色，因此您不必在每次从一个设置移动到另一个设置时全部重新配置源代码管理选项，即可采用不同的开发设置进行工作。  
  
### <a name="to-set-source-control-options"></a>若要设置源代码管理选项  
  
1.  在“工具”  菜单上，单击“选项” 。  
  
2.  在中**选项**对话框框中，展开**源代码管理**，然后单击**插件选择**页。  
  
     **当前源代码管理插件**  
     从此列表中选择要使用的源代码管理。 必须在此计算机上安装源代码管理产品客户端，才能在该列表中显示源代码管理产品。 如果计算机上没有安装源代码管理客户端，则唯一可用的选项是“无”。 如果您安装了 Microsoft Source Safe，则会显示以下插件：  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe(Internet)  
  
3.  为要使用的每个源代码管理角色设置登录凭据。 只有当安装了源代码管理插件时，此页才可用。  
  
     **角色描述**  
     选择这些角色之一，将自动选择相应的源代码管理选项。  
  
    |角色|Description|  
    |----------|-----------------|  
    |**Visual SourceSafe**|指定你想要使用最常使用的设置[!INCLUDE[msCoName](../includes/msconame-md.md)]Visual SourceSafe 用户。|  
    |**独立开发人员**|指定您是在独立工作。|  
    |**自定义**|指定您已为特定角色修改了设置。|  
  
     **执行后台状态更新**  
     在项的状态改变时，自动更新解决方案资源管理器中源代码管理信号图标。 如果在执行占用大量服务器资源的操作时（尤其是在从源代码管理中打开解决方案或项目时）遇到延迟，则清除此复选框可能会改进性能。  
  
     **登录 ID**  
     指定要用来登录源代码管理提供程序的用户名。 如果受源代码管理提供程序，此名称，将填写中自动**登录名**对话框来访问你的源代码管理服务器。 若要激活此选项，请通过使用源代码管理提供程序的管理员程序来禁用用户自动登录，再重新启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
     **高级**  
     显示用于向源代码管理添加项的其他选项。 这些选项因源代码管理提供程序的不同而有所差异。 源代码管理程序提供了有关这些选项的帮助。  
  
4.  选择**环境**页。  
  
5.  在中**源代码管理环境设置**框中，选择你想要设置源代码管理选项的角色。  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将自动为您选定的角色选择默认的源代码管理选项。 如果您清除了任何默认选项**源代码管理环境设置**框将显示**自定义**选项以指示你已自定义最初选择的角色。  
  
     **源代码管理环境设置**  
     指定要使用的角色。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 定义了以下角色。  
  
    |角色|Description|  
    |----------|-----------------|  
    |**Visual SourceSafe**|指定你想要使用最常使用的设置[!INCLUDE[msCoName](../includes/msconame-md.md)]Visual SourceSafe 用户。|  
    |**独立开发人员**|指定您是在独立工作。|  
    |**自定义**|指定您已为特定角色修改了设置。|  
  
     选择这些角色之一，将自动选择相应的源代码管理选项。  
  
     **保留签入时签出项**  
     指定在签入项以更新源代码管理存储区时，这些项将对您保持签出状态。 如果你想要为特定签入更改此选项，请单击**选项**中的箭头**签入**对话框中，，然后清除**保持签出**复选框。  
  
     **签入的项**  
     显示一个选项列表，用于指定在您尝试编辑未签出项时，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将采取何种操作。下表列出了可用的选项。  
  
     **正在保存**  
  
    |操作|Description|  
    |------------|-----------------|  
    |**提示签出**|显示**签出**对话框。|  
    |**自动签出**|签出项而不会显示**签出**对话框。 这是默认选项。|  
    |**将另存为**|另存为新文件。|  
  
     **编辑**  
  
    |操作|Description|  
    |------------|-----------------|  
    |**提示签出**|显示**签出**对话框。|  
    |**以独占方式签出的提示**|显示**签出**对话框。|  
    |**自动签出**|签出项而不会显示**签出**对话框。 这是默认选项。|  
    |**不执行任何操作**|不签出文件。|  
  
     **允许编辑签入的项**  
     指定可以在内存中编辑签入的项。 如果选择此复选框，**编辑**按钮将出现在**签出**对话框中，当您尝试编辑签入的项。 单击此按钮后，即可编辑该项。 如果尝试保存该项，则必须签出它或者将其保存到其他位置。  
  
     **重置**  
     将源代码管理确认对话框重置为其默认设置。 例如，如果所选**不再显示此对话框**复选框，在源代码管理对话框中，选择**重置**选项将撤消该操作。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理基础知识](../../2014/database-engine/source-control-basics.md)   
 [更改源代码管理连接](../../2014/database-engine/change-source-control-connections.md)   
 [从源代码管理中排除文件](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
