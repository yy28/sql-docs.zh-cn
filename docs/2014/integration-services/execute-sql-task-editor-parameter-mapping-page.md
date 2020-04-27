---
title: 执行 SQL 任务编辑器（"参数映射" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7508324be0bef23ba0590bb181135512d75701e7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059043"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>执行 SQL 任务编辑器（“参数映射”页）
  可以使用 **“执行 SQL 任务编辑器”** 对话框的 **“参数映射”** 页，将变量映射到 SQL 语句中的参数。  
  
 若要了解此任务，请参阅 [执行 SQL 任务](control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
## <a name="options"></a>选项  
 **变量名称**  
 通过单击“添加”添加了参数映射之后，请从列表中选择系统变量或用户定义的变量，或单击“\<新建变量...>”以使用“添加变量”对话框添加新变量************。  
  
 **相关主题：** [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)  
  
 **方向**  
 选择参数的方向。 将每个变量映射到输入参数、输出参数或返回代码。  
  
 **数据类型**  
 选择参数的数据类型。 可用数据类型的列表取决于您为任务所用的连接管理器选择的访问接口。  
  
 **参数名称**  
 提供参数名称。  
  
 必须使用数值还是参数名称取决于任务所用的连接管理器类型。 一些连接管理器类型要求，参数名的首字符必须为 \@ 符号（如 \@Param1 等特定名称），或将列名用作参数名。  
  
 **相关主题：** [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **参数大小**  
 提供具有可变长度的参数的大小，如字符串和二进制字段。  
  
 此设置可确保访问接口为长度可变的参数值分配足够的空间。  
  
 **添加**  
 单击此项可添加参数映射。  
  
 **删除**  
 选择列表中的参数映射，再单击“删除”****。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [&#40;"常规" 页上执行 SQL 任务编辑器&#41;](general-page-of-integration-services-designers-options.md)   
 [&#40;"结果集" 页上执行 SQL 任务编辑器&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Transact-SQL 引用（数据库引擎）](/sql/t-sql/language-reference)  
  
  
