---
title: 平面文件连接管理器编辑器 （常规页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8282cf7060f106798f2fa482f474bc5e364492ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768313"
---
# <a name="flat-file-connection-manager-editor-general-page"></a>平面文件连接管理器编辑器（“常规”页）
  可以使用 **“平面文件连接管理器编辑器”** 对话框的 **“常规”** 页选择文件和数据格式。 使用平面文件连接可以将包连接到文本文件。  
  
 若要了解有关平面文件连接管理器的详细信息，请参阅 [Flat File Connection Manager](connection-manager/file-connection-manager.md)。  
  
## <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的平面文件连接提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中显示。  
  
 **说明**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **文件名**  
 键入要在平面文件连接中使用的路径和文件名。  
  
 **“浏览”**  
 定位要在平面文件连接中使用的文件名。  
  
 **区域设置**  
 指定区域设置，以便为排序以及日期和时间格式提供语言特定的信息。  
  
 **Unicode**  
 指示是否使用 Unicode。 如果使用 Unicode，则不能指定代码页。  
  
 **代码页**  
 指定非 Unicode 文本的代码页。  
  
 **格式**  
 指示文件是否使用带分隔符、固定宽度或右边未对齐的格式。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|带分隔符|各列之间由在 **“列”** 页上指定的分隔符隔开。|  
|固定宽度|列的宽度固定。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定。 它由行分隔符分隔。|  
  
 **文本限定符**  
 指定要使用的文本限定符。 例如，可以指定文本字段必须用引号括起来。  
  
> [!NOTE]  
>  选择文本限定符之后，不能重新选择“无”选项。 键入 **None** 以取消选择文本限定符。  
  
 **标题行分隔符**  
 从标题行的分隔符列表中选择，或输入分隔符文本。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|标题行由回车符和换行符的组合分隔。|  
|**{CR}**|标题行由回车符分隔。|  
|**{LF}**|标题行由换行符分隔。|  
|**分号 {;}**|标题行由分号分隔。|  
|**冒号 {:}**|标题行由冒号分隔。|  
|**逗号 {,}**|标题行由逗号分隔。|  
|**制表符 {t}**|标题行由制表符分隔。|  
|**竖线 {&#124;}。**|标题行由竖线分隔。|  
  
 **要跳过的标题行数**  
 指定要跳过的标题行数或初始数据行数（如果有的话）。  
  
 **第一个数据行中的列名称**  
 指示在第一个数据行中是否要求列名或提供列名。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)   
 [平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
