---
title: 执行 SQL 任务编辑器（"结果集" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 43921efab592e6642fcc5adaef8caa869a1b524f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966747"
---
# <a name="execute-sql-task-editor-result-set-page"></a>执行 SQL 任务编辑器（“结果集”页）
  可以使用 **“执行 SQL 任务编辑器”** 对话框的 **“结果集”** 页，将 SQL 语句的结果映射到新变量或现有变量。 如果将“常规”页上的 **ResultSet** 设置为 **“无”**，将禁用此对话框中的选项。  
  
 有关此任务的详细信息，请参阅 [执行 SQL 任务](control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的结果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)。  
  
## <a name="options"></a>选项  
 **结果名称**  
 通过单击“添加”**** 添加了结果集映射集之后，为结果提供名称。 必须根据结果集类型使用特定的结果名称。  
  
 如果结果集的类型为“单行” ****，则可以使用由查询返回的列的名称，也可以使用代表列在查询所返回列的列表中位置的数字。  
  
 如果结果集类型为“完整结果集” **** 或 **XML**，则必须使用 0 作为结果集名称。  
  
 **相关主题**：[执行 SQL 任务中的结果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
 **变量名称**  
 通过选择变量或单击 \<**New variable...**> 以使用 "**添加变量**" 对话框添加新的变量，将结果集映射到变量。  
  
 **添加**  
 单击此项可以添加结果集映射。  
  
 **删除**  
 在列表中选择结果集映射，再单击“删除”****。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [&#40;"常规" 页上执行 SQL 任务编辑器&#41;](general-page-of-integration-services-designers-options.md)   
 [执行 SQL 任务编辑器 &#40;参数映射页&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Transact-SQL 引用（数据库引擎）](/sql/t-sql/language-reference)  
  
  
