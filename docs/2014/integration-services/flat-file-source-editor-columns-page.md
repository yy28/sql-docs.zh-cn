---
title: 平面文件源编辑器 （列页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.columns.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f65e6e5dd0561960c36eea953b39b71906981fa9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118727"
---
# <a name="flat-file-source-editor-columns-page"></a>平面文件源编辑器（“列”页）
  可以使用“平面文件源编辑器”对话框的“列”节点，将输出列映射到每个外部（源）列。  
  
> [!NOTE]  
>  `FileNameColumnName`平面文件源的属性和`FastParse`及其输出列的属性中不可用**平面文件源编辑器**，但可以通过使用设置**高级编辑器**. 有关这些属性的详细信息，请参阅 [Flat File Custom Properties](data-flow/flat-file-custom-properties.md)的“平面文件源”部分。  
  
 若要了解有关平面文件源的详细信息，请参阅 [Flat File Source](data-flow/flat-file-source.md)。  
  
## <a name="options"></a>选项  
 **可用外部列**  
 查看数据源中可用外部列的列表。 无法使用此表添加或删除列。  
  
 **“外部列”**  
 按任务读取外部（源）列的顺序查看这些列。 首先清除表中所选的列，然后以不同的顺序从列表中选择外部列，即可更改顺序。  
  
 **输出列**  
 为每个输出列提供唯一的名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 所提供的名称将在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中显示。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [平面文件源编辑器&#40;连接管理器页&#41;](../../2014/integration-services/flat-file-source-editor-connection-manager-page.md)   
 [平面文件源编辑器&#40;错误输出页&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [平面文件连接管理器](connection-manager/file-connection-manager.md)  
  
  
