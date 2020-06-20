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
ms.openlocfilehash: 5ab6d134177c7861c3a8f92cf767c71c0b56e233
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929108"
---
# <a name="set-source-control-options"></a>设置源代码管理选项
  在利用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中内置的源代码管理功能之前，应针对您工作中所处的各种环境对源代码管理选项进行配置。  
  
 您可以通过使用 "**选项**" 对话框配置一个或多个源代码管理角色来配置源代码管理选项。 组成角色的内容包括：对使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 时所采用设置的常规说明，以及与该设置关联的源代码管理选项。  
  
 例如，如果您是独立的数据库开发人员，则在将文件签入后使其继续保持签出状态，通常不会产生与其他用户的冲突。 因此，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 定义了“独立开发人员”角色。 对于此角色， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 会自动选择 "**签入时使项保持签出状态**" 选项。  
  
 因为可以定义和自定义角色，因此您不必在每次从一个设置移动到另一个设置时全部重新配置源代码管理选项，即可采用不同的开发设置进行工作。  
  
### <a name="to-set-source-control-options"></a>设置源代码管理选项  
  
1.  在“工具”  菜单上，单击“选项” 。  
  
2.  在 "**选项**" 对话框中，展开 "**源代码管理**"，然后单击 "**插件选择**" 页。  
  
     **当前源代码管理插件**  
     从此列表中选择要使用的源代码管理。 必须在此计算机上安装源代码管理产品客户端，才能在该列表中显示源代码管理产品。 如果计算机上没有安装源代码管理客户端，则唯一可用的选项是“无”。 如果您安装了 Microsoft Source Safe，则会显示以下插件：  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe(Internet)  
  
3.  为要使用的每个源代码管理角色设置登录凭据。 只有当安装了源代码管理插件时，此页才可用。  
  
     **角色描述**  
     选择这些角色之一，将自动选择相应的源代码管理选项。  
  
    |角色|说明|  
    |----------|-----------------|  
    |**Visual SourceSafe**|指定您要使用 Visual SourceSafe 用户最常使用的设置 [!INCLUDE[msCoName](../includes/msconame-md.md)] 。|  
    |**独立开发人员**|指定您是在独立工作。|  
    |**自定义**|指定您已为特定角色修改了设置。|  
  
     **执行后台状态更新**  
     在项的状态改变时，自动更新解决方案资源管理器中源代码管理信号图标。 如果在执行占用大量服务器资源的操作时（尤其是在从源代码管理中打开解决方案或项目时）遇到延迟，则清除此复选框可能会改进性能。  
  
     **登录 ID**  
     指定要用来登录源代码管理提供程序的用户名。 如果源代码管理提供程序支持该名称，则会在**登录**对话框中自动填充此名称，以到达源代码管理服务器。 若要激活此选项，请通过使用源代码管理提供程序的管理员程序来禁用用户自动登录，再重新启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
     **高级**  
     显示用于向源代码管理添加项的其他选项。 这些选项因源代码管理提供程序的不同而有所差异。 源代码管理程序提供了有关这些选项的帮助。  
  
4.  选择 "**环境**" 页。  
  
5.  在 "**源代码管理环境设置**" 框中，选择要设置源代码管理选项的角色。  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将自动为您选定的角色选择默认的源代码管理选项。 如果清除了任何默认选项，则 "**源代码管理环境设置**" 框将显示 "**自定义**" 选项，以指示你已自定义了最初选择的角色。  
  
     **源代码管理环境设置**  
     指定要使用的角色。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 定义了以下角色。  
  
    |角色|说明|  
    |----------|-----------------|  
    |**Visual SourceSafe**|指定您要使用 Visual SourceSafe 用户最常使用的设置 [!INCLUDE[msCoName](../includes/msconame-md.md)] 。|  
    |**独立开发人员**|指定您是在独立工作。|  
    |**自定义**|指定您已为特定角色修改了设置。|  
  
     选择这些角色之一，将自动选择相应的源代码管理选项。  
  
     **签入时使项保持签出状态**  
     指定在签入项以更新源代码管理存储区时，这些项将对您保持签出状态。 如果要为特定签入更改此选项，请单击 "**签入**" 对话框中的 "**选项**" 箭头，然后清除 "**保持签出状态**" 复选框。  
  
     **签入的项**  
     显示一个选项列表，该列表指定在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 您尝试编辑未签出的项时应如何工作。下表描述了可用的选项。  
  
     **保存**  
  
    |操作|说明|  
    |------------|-----------------|  
    |**提示签出**|显示 "**签出**" 对话框。|  
    |**自动签出**|签出项而不显示 "**签出**" 对话框。 这是默认选项。|  
    |**另存为**|另存为新文件。|  
  
     **正在编辑**  
  
    |操作|说明|  
    |------------|-----------------|  
    |**提示签出**|显示 "**签出**" 对话框。|  
    |**提示以独占方式签出**|显示 "**签出**" 对话框。|  
    |**自动签出**|签出项而不显示 "**签出**" 对话框。 这是默认选项。|  
    |**不执行任何操作**|不签出文件。|  
  
     **允许编辑签入的项**  
     指定可以在内存中编辑签入的项。 如果选中此复选框，则在您尝试编辑签入的项时，"**签出**" 对话框中将显示一个 "**编辑**" 按钮。 单击此按钮后，即可编辑该项。 如果尝试保存该项，则必须签出它或者将其保存到其他位置。  
  
     **重置**  
     将源代码管理确认对话框重置为其默认设置。 例如，如果在 "源代码管理" 对话框中选中了 "**不再显示此对话框**" 复选框，则选择 "**重置**" 选项会反转该操作。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理基础知识](../../2014/database-engine/source-control-basics.md)   
 [更改源代码管理连接](../../2014/database-engine/change-source-control-connections.md)   
 [从源代码管理中排除文件](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
