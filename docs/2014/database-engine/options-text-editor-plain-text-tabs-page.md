---
title: 选项（"文本编辑器"-"纯文本"-"选项卡" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
ms.assetid: 07d82d10-bca9-4b37-abbb-58ef9bfb264b
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 0e060f1bccb544edd4e82c759b737e05c4bb980b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089863"
---
# <a name="options-text-editor---plain-text---tabs-page"></a>选项（“文本编辑器”-“纯文本”-“选项卡”页）
  使用此对话框可以更改文本编辑器的跳格行为，该编辑器用于编辑未与特定开发语言关联的文档。 若要显示这些设置，请在****“工具”菜单上单击****“选项”，展开****“文本编辑器”，展开****“纯文本”，再单击****“制表符”。  
  
## <a name="setting-options-in-multiple-locations"></a>在多个位置设置选项  
 纯文本编辑器的选项也可在 **“所有语言”** 和“常规”对话框中设置。 如果使用 **“所有语言”** 对话框来设置其他 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 编辑器（例如 DMX 或 MDX 编辑器）的其他选项，则必须使用此对话框重置纯文本编辑器选项。  
  
## <a name="indenting"></a>缩进  
 **无**  
 不缩进按 Enter 时创建的新行。 光标置于新行的第一列。  
  
 **模块**  
 缩进按 Enter 时创建的新行，缩进量与上一行的缩进量相同。  
  
 **智能**  
 纯文本编辑器不支持此格式类型。  
  
## <a name="tabs"></a>制表符  
 **制表符大小**  
 设置制表位之间的距离（空格）。 默认为四个空格。  
  
 **缩进大小**  
 设置自动缩进的大小（空格）。 默认为四个空格。 可能会插入制表符、空格字符，或同时插入这二者，以填充为指定大小。  
  
 **插入空格**  
 缩进时仅插入空格，而不插入制表符。 例如，如果****“缩进大小”设置为 5，则在按 TAB 键或 ****“格式”工具栏上的****“增加缩进”按钮时会插入五个空格。  
  
 **保留制表符**  
 在缩进时插入尽可能多的制表符。 每个制表符都会填充 **“制表符大小”** 中指定的空格数。 如果****“缩进大小”不是****“制表符大小”的偶数倍，则会添加空格补齐。  
  
  
