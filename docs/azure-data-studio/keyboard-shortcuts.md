---
title: 创建和自定义 Azure Data Studio 中的键盘快捷键 |Microsoft Docs
description: 了解如何创建和自定义 Azure Data Studio 中的键盘快捷键。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3452e2e19d237f8ba5135c723e9971c0932ba61c
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356468"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>中的键盘快捷键 [!INCLUDE[name-sos](../includes/name-sos.md)]

本文提供了快速查看、 编辑和创建键盘快捷方式中的步骤[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

因为[!INCLUDE[name-sos](../includes/name-sos-short.md)]从 Visual Studio Code 中，高级自定义，有关详细信息使用不同的键盘布局等继承其键绑定功能，处于[Visual Studio Code 的键绑定](https://code.visualstudio.com/docs/getstarted/keybindings)一文。 某些键绑定功能可能不可用 (例如，在不支持键映射扩展[!INCLUDE[name-sos](../includes/name-sos-short.md)])。


## <a name="open-the-keyboard-shortcuts-editor"></a>打开键盘快捷键编辑器

若要查看所有当前定义的键盘快捷方式：

打开**键盘快捷方式**从编辑器**文件**菜单：**文件** > **首选项** >  **键盘快捷方式**(**[!INCLUDE[name-sos](../includes/name-sos-short.md)]** > **首选项** > **键盘快捷方式**Mac 上)。

除了显示当前键绑定**键盘快捷方式**编辑器列出了可用的命令不具有定义的键盘快捷方式。 **键盘快捷方式**编辑器，您可以轻松地更改、 删除、 重置，并定义新的键绑定。  


## <a name="edit-existing-keyboard-shortcuts"></a>编辑现有的键盘快捷方式

若要更改现有的键盘快捷方式的键绑定：

1. 找到你想要通过使用搜索框或滚动浏览列表更改键盘快捷方式。
   > [!TIP]
   > 搜索由参数、 命令、 通过源等内容，返回所有相关的键盘快捷方式。

1. 右键单击所需的条目并选择**更改键绑定**

   ![编辑键盘快捷方式](media/keyboard-shortcuts/change-keybinding.png)

1. 按所需的组合键的键，然后按**Enter**将其保存。 

   ![保存键盘快捷方式](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>创建新的键盘快捷方式

若要创建新的键盘快捷方式：

1. 右击某个命令，没有任何键绑定，并选择**添加的键绑定**。

   ![创建键盘快捷方式](media/keyboard-shortcuts/add-keybinding.png)

1. 按所需的组合键的键，然后按**Enter**将其保存。


