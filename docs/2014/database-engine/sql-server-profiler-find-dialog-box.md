---
title: SQL Server Profiler-查找对话框 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.find.f1
helpviewer_keywords:
- Find dialog box
ms.assetid: dfaeec04-93d3-4214-9fc1-38b80179b36b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23bbfd748bcb649e5f7d103683d20413764a62a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842494"
---
# <a name="sql-server-profiler---find-dialog-box"></a>SQL Server Profiler -“查找”对话框
  使用 **“查找”** 对话框可以在跟踪中搜索特定字符或字词。 若要取消正在进行的搜索，请按 Esc。  
  
 若要在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]中打开此对话框，请在 **“编辑”** 菜单上，单击 **“查找”**。  
  
## <a name="options"></a>选项  
 **查找内容**  
 输入要搜索的文本。 该搜索匹配包含指定字符串的任何字符串。 例如，针对“Completed”的搜索匹配“SQL:BatchCompleted”。 不支持通配符（*、? 等）。  
  
 **在列中搜索**  
 单击要搜索的数据列，或者单击“\<所有列>”以搜索跟踪中的所有数据列。  
  
 **匹配大小写**  
 查找与“查找内容”框中的大小写完全匹配的文本。 清除此复选框将在跟踪中不区分文本字符的大小写形式查找匹配项。  
  
 **全字匹配**  
 将搜索结果限制为完整的字词。 清除 **“全字匹配”** 复选框可以搜索单词内的部分字符。  
  
 **查找下一个**  
 查找“查找内容”框中字符的下一个匹配项。  
  
 **查找上一个**  
 在跟踪中向后搜索，以查找“查找内容”框中字符的上一个匹配项。  
  
## <a name="see-also"></a>请参阅  
 [查找值或跟踪时数据列&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)   
 [创建跟踪 (SQL Server Profiler)](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [打开跟踪表 (SQL Server Profiler)](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [打开跟踪文件 (SQL Server Profiler)](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
