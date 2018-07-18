---
title: 选项 （查询结果-SQL Server 的结果到网格页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 23e5634a67ff6daec4f6b0852905d8596b885c60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37318897"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>选项 （查询结果-SQL Server 的结果到网格页）
  使用此页可以指定以网格格式显示查询结果集的选项。 对这些选项所做的更改只应用于新的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询。 若要更改当前查询的选项，请在“查询”菜单上单击“查询选项”，或在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询窗口中单击右键，再选择“查询选项”。 在 **“查询选项”** 对话框的左窗格中，在 **“结果”** 下，单击 **“网格”**。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **在结果集中包括查询**  
 作为查询输出的一部分返回查询文本。  
  
 **复制或保存结果时包括列标题**  
 在将结果复制到剪贴板或保存到文件时若要包括列标题，请选中此复选框。 如果希望保存或复制的结果数据只有数据而没有列标题，请清除此复选框。  
  
 **执行后放弃结果**  
 禁止在查看窗格中显示查询结果。 结果将在执行查询之后立即放弃。 指定此选项可帮助节省内存。  
  
 **在单独的选项卡中显示结果**  
 选中此复选框可在新选项卡中显示结果集，而不是在查询文档窗口的底部显示。  
  
 **执行查询后切换到结果选项卡**  
 单击此项可在执行查询时，将屏幕焦点自动设置到结果窗格。  
  
 **检索的最大字符数**  
 **非 XML 数据**：  
  
 输入一个介于 1 到 65535 之间的数字以指定每个单元中显示的最大字符数。  
  
> [!NOTE]  
>  指定大量字符可能会导致结果集中显示的数据截断。 每个单元中显示的最大字符数取决于字号。 在返回较大的结果集时，如果此框中的值太大，可能会导致 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 运行时内存不足，从而影响系统性能。  
  
 **XML 数据**：  
  
 选择 **1 MB**、 **2 MB**或 **5 MB**。 选择 **“无限制”** 将检索所有字符。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
