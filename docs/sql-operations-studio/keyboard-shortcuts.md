---
title: 创建和自定义 SQL Operations Studio (preview) 中的键盘快捷键 |Microsoft 文档
description: 了解如何创建和自定义 SQL Operations Studio (preview) 中的键盘快捷方式。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a96204723bd56a63ec23841ede47b5844fbad313
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>中的键盘快捷键[!INCLUDE[name-sos](../includes/name-sos.md)]

本文提供了快速查看、 编辑和创建中的键盘快捷键的步骤[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

因为[!INCLUDE[name-sos](../includes/name-sos-short.md)]从 Visual Studio Code，详细信息高级自定义项，使用不同的键盘布局等继承其键绑定功能，处于[Visual Studio Code 的键绑定](https://code.visualstudio.com/docs/getstarted/keybindings)文章。 键绑定的某些功能可能不可用 (例如，在不支持键映射扩展[!INCLUDE[name-sos](../includes/name-sos-short.md)])。


## <a name="open-the-keyboard-shortcuts-editor"></a>打开键盘快捷键编辑器

若要查看所有当前定义的键盘快捷方式：

打开**键盘快捷方式**编辑器与**文件**菜单：**文件** > **首选项** >  **键盘快捷方式**(**[!INCLUDE[name-sos](../includes/name-sos-short.md)]** > **首选项** > **键盘快捷方式**Mac 上)。

除了显示当前键绑定**键盘快捷方式**编辑器列出可用命令没有定义的键盘快捷方式。 **键盘快捷方式**编辑器，可以轻松地更改、 删除、 重置，和定义新的键绑定。  


## <a name="edit-existing-keyboard-shortcuts"></a>编辑现有的键盘快捷方式

若要更改为现有的键盘快捷方式键绑定：

1. 找到你想要更改通过使用搜索框或列表中上下滚动的键盘快捷方式。
   > [!TIP]
   > 搜索由参数、 命令、 源、 等返回所有相关的键盘快捷方式。

1. 右键单击所需的条目，然后选择**更改键绑定**

   ![编辑键盘快捷方式](media/keyboard-shortcuts/change-keybinding.png)

1. 按所需的组合的密钥，然后按**Enter**将其保存。 

   ![保存键盘快捷方式](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>创建新的键盘快捷方式

若要创建新键盘快捷方式：

1. 右击某个命令，没有任何键绑定，然后选择**添加键绑定**。

   ![创建键盘快捷方式](media/keyboard-shortcuts/add-keybinding.png)

1. 按所需的组合的密钥，然后按**Enter**将其保存。


