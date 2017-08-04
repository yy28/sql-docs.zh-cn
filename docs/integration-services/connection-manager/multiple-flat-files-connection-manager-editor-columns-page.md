---
title: "多平面文件连接管理器编辑器 （列页） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multifile.columns.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: ad0cb668-0df2-4d4e-9a20-d20692a0b67a
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f1f2dee040a886d66ffcd5bd3fa3a710a8552b7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>多平面文件连接管理器编辑器（“列”页）
  可以使用 **“多平面文件连接管理器编辑器”** 对话框的 **“列”** 节点指定行和列的信息，以及预览选定的第一个文件。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
## <a name="static-options"></a>静态选项  
 **连接管理器名称**  
 为工作流中的“多平面文件连接”提供一个唯一名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **Description**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
## <a name="flat-file-format-dynamic-options"></a>平面文件格式动态选项  
  
### <a name="format--delimited"></a>格式 = 带分隔符  
 **行分隔符**  
 从可用行分隔符的列表中选择，或输入分隔符文本。  
  
|“值”|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|行由回车符和换行符的组合分隔。|  
|**{CR}**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**逗号 {,}**|行由逗号分隔。|  
|**制表符 {t}**|行由制表符分隔。|  
|**竖线 {|}。**|行由竖线分隔。|  
  
 **列分隔符**  
 从可用列分隔符的列表中选择，或输入分隔符文本。  
  
|“值”|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|列由回车符和换行符的组合分隔。|  
|**{CR}**|列由回车符分隔。|  
|**{LF}**|列由换行符分隔。|  
|**分号 {;}**|列由分号分隔。|  
|**冒号 {:}**|列由冒号分隔。|  
|**逗号 {,}**|列由逗号分隔。|  
|**制表符 {t}**|列由制表符分隔。|  
|**竖线 {|}。**|列由竖线分隔。|  
  
 **重置列**  
 通过单击“重置列”可以删除除原始列之外的所有列。  
  
### <a name="format--fixed-width"></a>格式 = 固定宽度  
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽  
  
 **行宽**  
 为各列添加分隔符之前，先指定行的长度。 或者，拖动预览窗口中的垂直线，以标记行尾。 行宽值将自动更新。  
  
 **重置列**  
 通过单击“重置列”可以删除除原始列之外的所有列。  
  
### <a name="format--ragged-right"></a>格式 = 右边未对齐  
  
> [!NOTE]  
>  右边未对齐是指文件中除最后一列之外每一列的宽度都固定。 它由行分隔符分隔。  
  
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽  
  
 **行分隔符**  
 从可用行分隔符的列表中选择，或输入分隔符文本。  
  
|“值”|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|行由回车符和换行符的组合分隔。|  
|**{CR}**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**逗号 {,}**|行由逗号分隔。|  
|**制表符 {t}**|行由制表符分隔。|  
|**竖线 {|}。**|行由竖线分隔。|  
  
 **重置列**  
 通过单击“重置列”可以删除除原始列之外的所有列。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [多个平面文件连接管理器编辑器 &#40;常规页&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)   
 [多个平面文件连接管理器编辑器 &#40;高级页 &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [多个平面文件连接管理器编辑器 &#40;预览页&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
