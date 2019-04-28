---
title: 选项 (文本编辑器-所有语言的选项卡页) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: bd715d6b-f873-41d4-aa10-57b7098b61cc
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a49db54b71f3b7daf0a7a10cc1b4073f1b651fc5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844188"
---
# <a name="options-text-editor---all-languages--tabs-page"></a>选项（“文本编辑器”-“所有语言”-“选项卡”页）
  使用此对话框可以设置 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的所有五个编辑器的跳格行为。 若要显示这些选项，请在 **“工具”** 菜单上单击 **“选项”** 。 选择“文本编辑器”文件夹，展开“所有语言”文件夹，再单击“制表符”。  
  
## <a name="tabbing-options-by-editor"></a>编辑器的跳格选项  
 您必须使用 **“所有语言”** 对话框来设置 DMX、MDX 和 SQL Server Compact 编辑器的选项。 此处设置的选项也适用于纯文本、Transact-SQL 和 XML 编辑器，但您可以通过展开这些语言的子文件夹并选择相应的选项页面来为这些编辑器单独设置选项。 某些语言只能支持部分跳格选项。  
  
> [!CAUTION]  
>  如果你使用此对话框设置了选项，但希望在纯文本、Transact-SQL 或 XML 编辑器中使用不同设置，则必须在“所有语言”对话框中应用选项之后为这些编辑器设置选项。  
  
 如果为特定编辑器选择了不同设置，则将显示“各种文本格式的缩进(或制表符)设置相互冲突”消息。 例如，如果为“纯文本”选择了“块缩进”选项，而为“XML”选择了“无”，那么将会显示此提示信息。  
  
## <a name="indenting"></a>缩进  
 **无**  
 选择此选项后，则按 Enter 键时所创建的新行不会缩进。 光标置于新行的第一列。  
  
 **Block**  
 如果选择此选项，则按 Enter 时所创建新行的自动缩进距离与上一行的缩进距离相同。  
  
 **Smart**  
 选择此选项后，则按 Enter 键时所创建的新行会根据上下文调整位置。  
  
## <a name="tabs"></a>制表符  
 **制表符大小**  
 设置制表位之间的距离（以空格为单位）。 默认为四个空格。  
  
 **缩进大小**  
 设置自动缩进的大小（以空格为单位）。 默认为四个空格。 可能会插入制表符、空格字符，或同时插入这二者，以填充为指定大小。  
  
 **插入空格**  
 选择此选项后，缩进操作仅插入空格字符，而不会插入制表符。 如果“缩进大小”设置为 5，则在按 Tab 键或单击 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 主窗口工具栏上的“增加缩进”按钮时会插入五个空格。  
  
 **保留制表符**  
 选择此选项后，缩进操作会插入尽可能多的制表符。 每个制表符都会填充 **“制表符大小”** 中指定的空格数。 如果 **“缩进大小”** 不是 **“制表符大小”** 的偶数倍，则会添加空格字符补齐。  
  
  
