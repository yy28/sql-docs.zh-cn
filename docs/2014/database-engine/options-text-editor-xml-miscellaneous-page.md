---
title: 选项 （文本编辑器-XML-杂项页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 1a9509f0-c663-4b31-b396-7f5dc4371651
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 70689ff767661409dce982d7bb294d0b620838e2
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328427"
---
# <a name="options-text-editor---xml---miscellaneous-page"></a>选项（“文本编辑器”-“XML”-“杂项”页）

使用“选项”对话框，可以更改 XML 编辑器的自动完成设置和架构设置。 若要使用这些设置，请在“工具”菜单上单击“选项”，展开“文本编辑器”文件夹，单击“XML”，再单击“杂项”。  
  
## <a name="auto-insert"></a>自动插入  
 **关闭标记**  
 文本编辑器在创建 XML 元素时将添加关闭标记。 如果选择了元素开始标记，该编辑器将插入匹配的关闭标记，包括匹配的命名空间前缀。 默认情况下，此复选框为选中状态。  
  
 **属性引号**  
 创建 XML 属性时，编辑器将插入 `="``"` 字符并将插入号 (**^** ) 置于引号内。 默认情况下，此复选框为选中状态。  
  
 **Namespace 声明**  
 文本编辑器将在需要的位置自动插入命名空间声明。 默认情况下，此复选框为选中状态。  
  
 **其他标记 （注释，CDATA）**  
 注释、CDATA、DOCTYPE、处理指令和其他标记是自动完成的。 默认情况下，此复选框为选中状态。  
  
## <a name="network"></a>网络  
 **自动下载 Dtd 和架构**  
 架构和文档类型定义 (DTD) 是从 HTTP 位置上自动下载的。 此功能使用了启用自动代理服务器检测功能的 System.Net。 默认情况下，此复选框为选中状态。  
  
## <a name="outlining"></a>大纲显示  
 **打开文件时进入大纲模式**  
 打开文件时，将启用大纲显示功能。 默认情况下，此复选框为选中状态。  
  
## <a name="caching"></a>Caching  
 **架构**  
 指定架构缓存的位置。 单击“浏览(...)”按钮在新窗口中打开当前的架构缓存。 默认位置是 *\<Management Studio 安装目录 >* \Xml\Schemas。  
