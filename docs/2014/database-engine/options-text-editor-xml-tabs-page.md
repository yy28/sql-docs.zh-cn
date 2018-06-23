---
title: 选项 （文本编辑器： XML:Tabs 页） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Tabs
ms.assetid: 13bf5f8c-aba3-4c05-b8bb-eb475797c9bd
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bb41fb44ad1f820623ab3db96b1bf6108fd580a0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016653"
---
# <a name="options-text-editorxmltabs-page"></a>选项 （文本编辑器： XML:Tabs 页）
  此对话框支持您更改 XML 编辑器（用于编辑 XML 文档）的跳格行为。 若要显示这些设置，请在 **“工具”** 菜单上单击 **“选项”** ，展开 **“文本编辑器”** 文件夹，展开 **XML** 子文件夹，再单击 **“制表符”**。  
  
## <a name="setting-options-in-multiple-locations"></a>在多个位置设置选项  
 XML 编辑器的选项也可在“所有语言”和“常规”对话框中设置。  如果使用 **“所有语言”** 对话框来设置其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 编辑器（例如 DMX 或 MDX 编辑器）的其他选项，则必须使用此对话框重置 XML 编辑器选项。  
  
## <a name="indenting"></a>缩进  
 **无**  
 选择此选项后，则按 Enter 键时所创建的新行不会缩进。 光标置于新行的第一列。  
  
 **块**  
 如果选择此选项，则按 Enter 时创建的新行的自动缩进距离与上一行的缩进距离相同。  
  
 **智能**  
 选择此选项后，则按 Enter 键时所创建的新行会根据上下文调整位置。 例如，在左大括号 ({) 后，包含的行将自动多缩进一个制表位。 对应的右大括号 (}) 将根据其左大括号重新对齐。  
  
## <a name="tabs"></a>制表符  
 **制表符大小**  
 设置制表位之间的距离（以空格为单位）。 默认为四个空格。  
  
 **缩进大小**  
 设置自动缩进的大小（以空格为单位）。 默认为四个空格。 可能会插入制表符、空格字符，或同时插入这二者，以填充为指定大小。  
  
 **插入空格**  
 选择此选项后，缩进操作仅插入空格字符，而不会插入制表符。 例如，如果 **“缩进大小”** 设置为 5，则每次按 Tab 键或单击 **主窗口工具栏上的** “增加缩进” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 按钮时会插入五个空格。  
  
 **保留制表符**  
 选择此选项后，缩进操作会插入尽可能多的制表符。 每个制表符都会填充 **“制表符大小”** 中指定的空格数。 如果 **“缩进大小”** 不是 **“制表符大小”** 的偶数倍，则会添加空格字符补齐。  
  
  