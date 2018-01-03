---
title: "使用结果列表搜索文档 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searches [SQL Server Management Studio], result lists
- result list searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], multiple files
- Query Editor [SQL Server Management Studio], search multiple files
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f6159d723ec52adf4117a5ab571570b6c1ec1166
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="search-documents-using-results-lists"></a>使用结果列表搜索文档
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]使用“查找和替换”对话框，可以搜索和替换项目、解决方案或文件系统文件夹中的所有文件中的文本（即使这些文件未在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开）。 使用 **“查找和替换”** 对话框执行的搜索返回的匹配项将显示在“查找结果 1”和“查找结果 2”窗口中。这样，您可以查看包含匹配项的行中的完全匹配文本。  
  
### <a name="to-search-in-multiple-files"></a>在多个文件中搜索  
  
1.  在 **“编辑”** 菜单上，指向 **“查找和替换”** ，再单击 **“在文件中查找”**。  
  
2.  在 **“查找内容”** 文本框中，输入要搜索的文本。  
  
3.  在 **“查找范围”** 列表中，单击 **“所有打开的文档”**、 **“当前项目”**、 **“整个解决方案”**，或者键入目录路径。  
  
4.  在 **“文件类型”** 列表中，选择一个列出的文件扩展名组，或输入要搜索的文件类型的扩展名（由分号分隔）。 使用 \*.\* 可以搜索在“查找范围”下拉列表中列出的目录中的所有文件。  
  
5.  选择其余搜索选项以提高搜索的准确性。  
  
6.  单击 **“查找”** 以开始执行搜索。  
  
 在默认情况下，搜索匹配项将显示在“查找结果 1”窗口中。 可以通过双击“查找结果 1”窗口中的每个条目浏览搜索匹配项。 若要在新窗口中查看搜索结果，请选择 **“在查找 2 中显示”**。  
  
#### <a name="to-replace-across-multiple-files-or-folders"></a>在多个文件或文件夹中替换  
  
1.  在 **“编辑”** 菜单上，指向 **“查找和替换”** ，再单击 **“在文件中替换”**。  
  
2.  在 **“查找内容”** 文本框中，输入要搜索的文本。  
  
3.  在 **“替换为”** 框中，输入用来替换搜索文本的文本。  
  
4.  在 **“查找范围”** 列表中，单击 **“所有打开的文档”**、 **“当前项目”**、 **“整个解决方案”**，或者键入目录路径。  
  
5.  单击 **“替换”** 以使用 **“替换为”** 框中的文本替换当前的搜索匹配项。 可以通过单击 **“查找下一个”** 跳过单个匹配项，或通过单击 **“跳过文件”**跳过整个文件。  
  
     \- 或 -  
  
     选择 **“全部替换”** 以使用 **“替换为”** 框中的文本替换所有匹配项。 若要在其他时间撤消某些替换，请选择 **“在全部替换后使已修改文件保持打开状态”** 。  
  
    > [!NOTE]  
    >  如果选择**“全部替换”** ，则系统将替换所有搜索匹配项，包括已使用 **“跳过文件”** 或 **“查找下一个”**跳过的那些搜索匹配项。 只能针对在替换操作完成后仍保持打开状态的文件中进行的替换使用 **“撤消”** 操作。  
  
 默认情况下，替换信息将显示在“查找结果 1”窗口中。 可以通过双击“查找结果 1”窗口中的各个条目来浏览替换项。  
  
## <a name="see-also"></a>另请参阅  
 [搜索和替换](../../relational-databases/scripting/search-and-replace.md)   
 [交互式搜索文档](../../relational-databases/scripting/search-documents-interactively.md)   
 [使用通配符搜索文本](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用正则表达式搜索文本](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
