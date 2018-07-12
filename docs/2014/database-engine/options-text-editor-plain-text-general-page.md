---
title: 选项 （文本编辑器的纯文本-常规页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.General
ms.assetid: 53bfa594-ba36-4c9c-8dd5-4c2dcce7d2dc
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b66c8286d3ae062307175e689f222f33ea3be6a0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150988"
---
# <a name="options-text-editor---plain-text---general-page"></a>选项（“文本编辑器”-“纯文本”-“常规”页）
  使用此对话框可以更改文本编辑器的常规编辑行为，该编辑器用于编辑未与特定开发语言关联的文档。 若要显示这些设置，请在 **“工具”** 菜单上单击 **“选项”** ，依次展开 **“文本编辑器”** 和 **“纯文本”** ，然后单击 **“常规”**。  
  
## <a name="setting-options-in-multiple-locations"></a>在多个位置设置选项  
 纯文本编辑器的选项也可在 **“所有语言”** 和“常规”对话框中设置。 如果使用 **“所有语言”** 对话框来设置其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 编辑器（例如 DMX 或 MDX 编辑器）的其他选项，则必须使用此对话框重置纯文本编辑器选项。  
  
## <a name="statement-completion"></a>语句结束  
 **自动列出成员**  
 纯文本编辑器不支持此功能。  
  
 **隐藏高级成员**  
 纯文本编辑器不支持此功能。  
  
 **参数信息**  
 纯文本编辑器不支持此功能。  
  
## <a name="settings"></a>“设置”  
 **启用虚空格**  
 在每行文本的结尾处插入空格。 如果选中此复选框，则注释在文本旁的位置将保持不变。  
  
 **自动换行**  
 将行水平延伸到编辑器可见区域之外的所有部分在下一行中显示。 选中此复选框将启用 **“显示可视的自动换行标志符号”** 选项。  
  
 **显示可视的自动换行标志符号**  
 在长行换行的位置显示返回箭头指示符。 如果不希望显示这些指示符，请清除此复选框。  
  
> [!NOTE]  
>  这些提示箭头不会添加到代码中，也不会打印出来。 它们仅供参考。  
  
 **未选择任何内容时对空行应用剪切或复制命令**  
 设置将插入点放在空行中，不选择任何内容，再单击 **“复制”** 或 **“剪切”** 时的编辑器行为。  
  
 如果选中此复选框，将复制或剪切空白行。 如果随后单击 **“粘贴”**，将插入一个新空白行。  
  
 如果此复选框处于未选中状态，则不复制或剪切任何内容。 如果随后单击 **“粘贴”**，将粘贴最近一次复制的内容。 如果尚未复制任何内容，则不会粘贴任何内容。  
  
 如果不是空白行，则此设置对 **“复制”** 或 **“剪切”** 无效。 如果没有选定任何内容，将复制或剪切整个行。 如果随后单击 **“粘贴”**，将粘贴整个行的文本及其行终止符。  
  
## <a name="display"></a>显示位置  
 **行号**  
 在每行文本的旁边显示行号。  
  
> [!NOTE]  
>  这些行号不会添加到文本中，也不会打印出来。 它们仅供参考。  
  
 **启用单击 URL 定位**  
 当光标移至编辑器的 URL 上方时，将光标变为手形指针。 您可以单击 URL 以在 Web 浏览器中显示所指示的页。  
  
 **导航栏**  
 此复选框不可用。  
  
  
