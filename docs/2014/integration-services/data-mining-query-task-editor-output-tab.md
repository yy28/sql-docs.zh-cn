---
title: 数据挖掘查询任务编辑器 ("输出" 选项卡) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- Data Mining Query Task Editor
ms.assetid: 62f9e015-6fe0-4396-ad90-3ad51bf00025
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7b381ec722125bfa6ad8a4b8102e2fa3b7a5c309
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890471"
---
# <a name="data-mining-query-task-editor-output-tab"></a>数据挖掘查询任务编辑器（“输出”选项卡）
  可以使用 **“数据挖掘查询任务编辑器”** 对话框的 **“输出”** 选项卡指定预测查询的目标。  
  
 若要了解有关在包中实现数据挖掘的详细信息，请参阅 [数据挖掘查询任务](control-flow/data-mining-query-task.md) 和 [数据挖掘解决方案](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)。  
  
## <a name="general-options"></a>常规选项  
 **名称**  
 为数据挖掘查询任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入数据挖掘查询任务的说明。  
  
## <a name="output-tab-options"></a>“输出”选项卡选项  
 **“连接”**  
 从列表中选择连接管理器，或单击“新建”以创建新的连接管理器。  
  
 **新建**  
 创建新的连接管理器。 只能使用 ADO.NET 和 OLE DB 连接管理器类型。  
  
 **输出表**  
 指定预测查询要将其结果写入的表。  
  
 **删除并重新创建该输出表**  
 指示预测查询是否应通过删除表后再重新创建表来覆盖目标表中的内容。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [数据挖掘查询任务编辑器（“挖掘模型”选项卡）](../../2014/integration-services/data-mining-query-task-editor-mining-model-tab.md)   
 [数据挖掘查询任务编辑器（“查询”选项卡）](../../2014/integration-services/data-mining-query-task-editor-query-tab.md)   
 [数据挖掘设计器](https://docs.microsoft.com/analysis-services/data-mining/data-mining-designer)  
  
  
