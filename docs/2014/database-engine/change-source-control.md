---
title: 更改源代码管理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- IDD_SCC_CONNECTION_DIALOG
helpviewer_keywords:
- Change Source Control dialog box
ms.assetid: e6a5d83c-5809-4c56-907a-73d0c7ccdd7a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 939e3befd0cbec87dbba7046761637c4b7655e22
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62812730"
---
# <a name="change-source-control"></a>更改源代码管理
  创建和管理特定的连接和绑定（用于将本地保存的解决方案或项目链接到源代码管理数据库文件夹）。  
  
## <a name="dialog-box-access"></a>对话框访问  
 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，请在解决方案资源管理器中选择一项。 在 "**文件**" 菜单上，单击 "**源代码管理**"，然后**更改源代码管理**。  
  
> [!NOTE]  
>  也可以右键单击解决方案资源管理器中的项来访问此对话框。  
  
## <a name="options"></a>选项  
 **绑定**  
 使所选项与指定的源代码管理服务器位置相关联。 例如，您可以使用此按钮绑定到上一次已知的源代码管理服务器文件夹和数据库。 如果找不到最近使用的服务器文件夹或数据库，则将提示您指定另一个。  
  
 **浏览**  
 导航到指定项的新源代码管理服务器位置。  
  
 **“列”**  
 标识要显示的列以及显示它们的顺序。  
  
 **“连接”**  
 在选定项和源代码管理服务器之间创建连接。  
  
 **联机**  
 显示选定解决方案或项目的连接状态。  
  
 **取消**  
 断开计算机上解决方案或项目的本地副本与数据库中其主副本的连接。 在断开计算机与源代码管理服务器的连接之前（例如在便携式计算机上脱机工作时），使用此命令。  
  
 **确定**  
 接受在对话框中进行的更改。  
  
 **提供程序**  
 显示您的源代码管理插件的名称。  
  
 **全部**  
 刷新在此对话框中列出的所有项目的连接信息。  
  
 **服务器绑定**  
 指示项绑定到源代码管理服务器。  
  
 **服务器名称**  
 显示将相应解决方案或项目绑定到的源代码管理服务器的名称。  
  
 **解决方案/项目**  
 显示当前选择中的每个解决方案和项目的名称。  
  
 **进行**  
 对显示的列的顺序进行排序。  
  
 **状态**  
 标识项的绑定和连接状态。 可能的选项包括：  
  
|**选项**|**说明**|  
|----------------|---------------------|  
|有效|项已正确绑定并连接到它所属的服务器文件夹。|  
|无效|项没有正确绑定到它所属的文件夹或者与该文件夹断开了连接。 对于此项，请使用 "**添加到源代码管理**" 命令而不是 "**绑定**"。|  
|Unknown|尚未确定源代码管理下项的状态。|  
|不受控制|该项尚未置于源代码管理下。|  
  
 **首先**  
 显示 "**源代码管理**" 对话框，允许您从源代码管理中删除所选项，并从其现有文件夹中永久取消项关联。  
  
## <a name="see-also"></a>另请参阅  
 [解决方案资源管理器源代码管理](../../2014/database-engine/solution-explorer-source-control.md)  
  
  
