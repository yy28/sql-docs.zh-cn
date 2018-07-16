---
title: Analysis Services 处理任务编辑器 （Analysis Services 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing Task Editor
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
caps.latest.revision: 28
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a131a7a25e9539eac5d7090508e3b67aa79fd9a1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187184"
---
# <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Analysis Services 处理任务编辑器（Analysis Services 页）
  可以使用 **“Analysis Services 处理任务编辑器”** 对话框的 **Analysis Services** 页指定 Analysis Services 连接管理器，选择要处理的分析对象，以及设置处理选项和错误处理选项。  
  
 处理表格模型时，请记住以下事项：  
  
1.  不能对表格模型执行影响分析。  
  
2.  不公开表格模型的一些处理选项，如“处理碎片整理”和“处理重新计算”。 您可以使用执行 DDL 任务来执行这些功能。  
  
3.  提供的一些处理选项（如处理索引）不适用于表格模型，不应使用它们。  
  
4.  对表格模型忽略批处理设置。  
  
 若要了解此任务，请参阅 [Analysis Services Processing Task](control-flow/analysis-services-processing-task.md)。  
  
## <a name="options"></a>“常规”  
 **Analysis Services 连接管理器**  
 从列表中选择现有的 Analysis Services 连接管理器，或单击“新建”以创建新的连接管理器。  
  
 **新建**  
 创建新的 Analysis Services 连接管理器。  
  
 **相关主题：**[Analysis Services 连接管理器](connection-manager/analysis-services-connection-manager.md)、[“添加 Analysis Services 连接管理器”对话框 UI 参考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **对象列表**  
 |“属性”|Description|  
|--------------|-----------------|  
|**Object Name**|列出指定对象的名称。|  
|**类型**|列出指定对象的类型。|  
|**处理选项**|从列表中选择处理选项。<br /><br /> **相关主题**:[多维模型对象处理](../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)|  
|**设置**|列出指定对象的处理设置。|  
  
 **“添加”**  
 将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象添加到列表中。  
  
 **删除**  
 选择对象，再单击“删除”。  
  
 **影响分析**  
 对所选对象进行影响分析。  
  
 **相关主题：**[“影响分析”对话框（Analysis Services - 多维数据）](../../2014/analysis-services/impact-analysis-dialog-box-analysis-services-multidimensional-data.md)  
  
 **批设置摘要**  
 |“属性”|Description|  
|--------------|-----------------|  
|**处理顺序**|指定是按顺序处理对象还是按批处理对象；如果使用并行处理，则指定要并发处理的对象数。|  
|**事务模式**|指定按顺序处理时的事务模式。|  
|**维度错误**|指定在发生错误时的任务行为。|  
|**维度键错误日志路径**|指定记录错误的文件的路径。|  
|**处理受影响的对象**|指示是否还处理依赖对象或受影响的对象。|  
  
 **更改设置**  
 更改处理选项以及对维度键中错误的处理方式。  
  
 **相关主题：**[“更改设置”对话框（Analysis Services - 多维数据）](../../2014/analysis-services/change-settings-dialog-box-analysis-services-multidimensional-data.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 处理任务编辑器&#40;常规页&#41;](general-page-of-integration-services-designers-options.md)   
 [Analysis Services 执行 DDL 任务](control-flow/analysis-services-execute-ddl-task.md)  
  
  
