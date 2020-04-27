---
title: 选项（文本编辑器-Transact-sql-IntelliSense） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Advanced
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.Advanced
dev_langs:
- TSQL
ms.assetid: 1855d916-5bf9-4d94-b0fb-9f9bb05ff950
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: fd2cf2be2102aeed1c853ce1b9a198c2b196d26a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089822"
---
# <a name="options-text-editor-transact-sql-intellisense"></a>选项（文本编辑器-Transact-sql-IntelliSense）
  您可以使用 **“选项”** 对话框更改 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查询编辑器的 IntelliSense 设置。 若要显示这些设置，请在“工具”**** 菜单上单击“选项”****，依次展开“文本编辑器”**** 文件夹和“Transact-SQL”**** 文件夹，然后单击“高级”****。  
  
## <a name="transact-sql-intellisense-settings"></a>Transact-SQL IntelliSense 设置  
 指定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 查询编辑器的 IntelliSense 选项。  
  
### <a name="enable-intellisense"></a>启用 IntelliSense  
 启用 IntelliSense 功能。 如果未选中此复选框，具体的 IntelliSense 选项不可用。 默认情况下，此复选框处于选中状态。  
  
 **用下划线标出错误**  
 在查询窗口中标识 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句中的语法和语义错误。 所有错误和警告将以红色显示。 只有已为其实现 IntelliSense 的 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句才支持错误和警告。 默认情况下，此复选框处于选中状态。  
  
 **大纲语句**  
 打开文件时启用大纲显示功能。 这将创建可折叠的 [!INCLUDE[tsql](../includes/tsql-md.md)] 代码块。 默认情况下，此复选框处于选中状态。  
  
 **最大脚本大小**  
 指定脚本的大小，达到此大小时将禁用 IntelliSense 功能。 如果脚本超过指定大小，则发出一条警告消息。 该编辑器窗口的所有 IntelliSense 功能（颜色编码功能除外）将被禁用。 在删除了足够多的文本以将脚本大小降低到限制范围内时，IntelliSense 将重新启用。 对大型脚本启用 IntelliSense 会降低速度较慢的计算机的性能。 允许的大小为 100 KB、500 KB、1 MB、2 MB 和无限制。 默认值为 1 MB。  
  
 **内置函数名称的大小写**  
 指定完成列表中内置 [!INCLUDE[tsql](../includes/tsql-md.md)] 函数的名称采用大写形式（例如 DATEADD）还是小写形式（例如 dateadd）。 请选择最符合您使用的 [!INCLUDE[tsql](../includes/tsql-md.md)] 编码约定的选项。  
  
## <a name="see-also"></a>另请参阅  
 [IntelliSense &#40;SQL Server Management Studio 疑难解答&#41;](../relational-databases/scripting/troubleshooting-intellisense.md)  
  
  
