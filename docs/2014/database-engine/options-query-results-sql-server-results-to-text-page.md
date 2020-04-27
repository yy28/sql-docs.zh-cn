---
title: 选项（查询结果-SQL Server-结果到文本页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToText
ms.assetid: 2ccbdf17-e14f-42f1-a836-ca999a3432c9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 43e35c5de15aeeab5351b4d262db846840e5f6a0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66090021"
---
# <a name="options-query-results-sql-server-results-to-text-page"></a>选项（查询结果-SQL Server-结果到文本页）
  使用此页可以指定以文本格式显示查询结果集的选项。 对这些选项所做的更改只应用于新的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询。 若要更改当前查询的选项，请在 "**查询**" 菜单上单击 "**查询选项**"，或在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查询窗口中单击右键，然后选择 "**查询选项**"。 在 **“查询选项”** 对话框中的 **“结果”** 下，单击 **“文本”**。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **输出格式**  
 默认情况下，将在通过用空格分隔结果而得到的列中显示输出。 您还可以使用逗号、制表符或空格来分隔列。 从此下拉列表中选择“自定义分隔符”****，可以在“自定义分隔符”**** 文本框中指定其他分隔字符。  
  
 **“自定义分隔符”**  
 自行指定用于分隔列的字符。 只有在“输出格式”**** 下拉列表框中单击“自定义分隔符”时，此文本框才可用。  
  
 **在结果集中包括列标题**  
 如果不希望每列都带有列标题，请清除此复选框。  
  
 **在结果集中包括查询**  
 在结果窗格中，若要在查询结果前面包括正在运行的查询文本，请选中此复选框。  
  
 **接收到结果时滚动**  
 选中此复选框将使得结果集的显示侧重于结尾处最近返回的记录。 清除此复选框，则使其侧重于接收到的前几行。  
  
 **右对齐数值**  
 选中此复选框可以将数值与列的右侧对齐。 这样，就可以更方便地查看具有固定小数位数的数值。  
  
 **在执行查询后放弃结果**  
 当查询结果在查询窗口的结果窗格中显示之后，若要放弃查询结果，请选中此复选框。  
  
 **在单独选项卡中显示结果**  
 选中此复选框可在新文档窗口中显示结果集，而不是在查询文档窗口的底部显示。  
  
 **执行查询后切换到“结果”选项卡**  
 若要自动将屏幕焦点设置到结果集，请选中此复选框。  
  
 **每列中显示的最大字符数**  
 此值默认为 256。 增大此值可显示更大的结果集，而不会将其截断。 最大值为 8,192。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
