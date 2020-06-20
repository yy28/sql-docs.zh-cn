---
title: 选项（查询执行-SQL Server-常规页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
author: rothja
ms.author: jroth
ms.openlocfilehash: 97fe66f317db25ab36f3e55cf2396f1252f66571
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930176"
---
# <a name="options-query-execution-sql-server-general-page"></a>选项（"查询执行-SQL Server-常规" 页）
  使用此页可指定用于运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询的选项。 对这些选项所做的更改仅应用于新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询。 若要更改当前查询的选项，请在“查询”**** 菜单上单击“查询选项”****，或在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询窗口中单击右键，再选择“查询选项”****。  
  
## <a name="options"></a>选项  
 **SET ROWCOUNT**  
 默认值为 0，指示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在收到所有结果之前将一直等待结果。 如果希望 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在获取指定数目的行后暂停查询，请提供一个大于 0 的值。 若要关闭此选项（以便返回所有的行），请将 SET ROWCOUNT 指定为 0。  
  
 **SET TEXTSIZE**  
 默认值为 2,147,483,647 字节，表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将提供长达 `text` 和 `ntext` 数据字段上限的完整数据字段。 提供较小的数值，可以在存在大量值时限制结果数量。 超出指定数量的列将被截断。  
  
 **执行超时值**  
 在 **“新建连接”** 对话框中设置默认值。 使用此数字调整框可以设置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在取消查询之前等待的时间（秒）。 值0表示无限期等待或无超时。对于新安装，此值为0。  
  
 **批分隔符**  
 键入用来将 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句分隔为批的词。 默认值为 GO。  
  
 **默认情况下，在 SQLCMD 模式下打开新查询**  
 选中此复选框可在 SQLCMD 模式下打开新查询。 有关 SQLCMD 模式的详细信息，请参阅[使用查询编辑器编辑 SQLCMD 脚本](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)。  
  
 选择此选项时，请记住下列限制：  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] 查询编辑器中的 IntelliSense 处于关闭状态。  
  
-   由于查询编辑器不能从命令行运行，因此您不能传入命令行参数（如变量）。  
  
-   由于查询编辑器无法响应操作系统提示，因此您一定要记住不要运行交互式语句。  
  
 **重置为默认值**  
 单击此项可将此页上的所有值重置为原始默认值。  
  
## <a name="see-also"></a>另请参阅  
 [sqlcmd 实用工具](../tools/sqlcmd-utility.md)  
  
  
