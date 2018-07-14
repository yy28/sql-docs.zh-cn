---
title: 分区处理目标编辑器 （连接管理器页） |Microsoft Docs
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
- sql12.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
caps.latest.revision: 26
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 383b28d86ca87457d26446e1bc881ddcda1084f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162968"
---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>分区处理目标编辑器（“连接管理器”页）
  可以使用 **“分区处理目标编辑器”** 对话框的 **“连接管理器”** 页，指定与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例之间的连接。  
  
 若要了解有关分区处理目标的详细信息，请参阅 [Partition Processing Destination](data-flow/partition-processing-destination.md)。  
  
> [!NOTE]  
>  此处所述的任何不适用于 Analysis Services 表格模型。  你无法将输入列映射到表格模型的分区列。 您可以改用 [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) 处理分区。  
  
## <a name="options"></a>“常规”  
 **“ODBC 目标编辑器”**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 通过使用“添加 Analysis Services 连接管理器”对话框创建一个新连接。  
  
 **可用分区列表**  
 选择要处理的分区。  
  
 **处理方法**  
 选择处理方法。 此选项的默认值为 **“完全”**。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|添加(增量式)|对分区执行增量处理。|  
|完全|对分区执行完全处理。|  
|仅限数据|对分区执行更新处理。|  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [分区处理目标编辑器&#40;映射页&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)   
 [分区处理目标编辑器&#40;高级页&#41;](../../2014/integration-services/partition-processing-destination-editor-advanced-page.md)  
  
  
