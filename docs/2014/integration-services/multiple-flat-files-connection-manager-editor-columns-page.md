---
title: 多平面文件连接管理器编辑器（"列" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.columns.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: ad0cb668-0df2-4d4e-9a20-d20692a0b67a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 365a22cc515a971ff460a6433973f884c640c973
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950807"
---
# <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>多平面文件连接管理器编辑器（“列”页）
  可以使用 **“多平面文件连接管理器编辑器”** 对话框的 **“列”** 节点指定行和列的信息，以及预览选定的第一个文件。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)。  
  
## <a name="static-options"></a>静态选项  
 **连接管理器名称**  
 为工作流中的“多平面文件连接”提供一个唯一名称。 所提供的名称将在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中显示。  
  
 **说明**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
## <a name="flat-file-format-dynamic-options"></a>平面文件格式动态选项  
  
### <a name="format--delimited"></a>格式 = 带分隔符  
 **行分隔符**  
 从可用行分隔符的列表中选择，或输入分隔符文本。  
  
|值|说明|  
|-----------|-----------------|  
|**回车换行符**|行由回车符和换行符的组合分隔。|  
|**回车**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**跟{,}**|行由逗号分隔。|  
|**选项卡 {t}**|行由制表符分隔。|  
|**竖线 {&#124;}**。|行由竖线分隔。|  
  
 **列分隔符**  
 从可用列分隔符的列表中选择，或输入分隔符文本。  
  
|值|说明|  
|-----------|-----------------|  
|**回车换行符**|列由回车符和换行符的组合分隔。|  
|**回车**|列由回车符分隔。|  
|**{LF}**|列由换行符分隔。|  
|**分号 {;}**|列由分号分隔。|  
|**冒号 {:}**|列由冒号分隔。|  
|**跟{,}**|列由逗号分隔。|  
|**选项卡 {t}**|列由制表符分隔。|  
|**竖线 {&#124;}**。|列由竖线分隔。|  
  
 **重置列**  
 通过单击“重置列”**** 可以删除除原始列之外的所有列。  
  
### <a name="format--fixed-width"></a>格式 = 固定宽度  
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽  
  
 **行宽**  
 为各列添加分隔符之前，先指定行的长度。 或者，拖动预览窗口中的垂直线，以标记行尾。 行宽值将自动更新。  
  
 **重置列**  
 通过单击“重置列”**** 可以删除除原始列之外的所有列。  
  
### <a name="format--ragged-right"></a>格式 = 右边未对齐  
  
> [!NOTE]  
>  右边未对齐是指文件中除最后一列之外每一列的宽度都固定。 它由行分隔符分隔。  
  
 **字体**  
 选择用于显示预览数据的字体。  
  
 **源数据列**  
 通过滑动垂直的行标记可以调整行宽，通过单击预览窗口顶部的标尺可以调整列宽  
  
 **行分隔符**  
 从可用行分隔符的列表中选择，或输入分隔符文本。  
  
|值|说明|  
|-----------|-----------------|  
|**回车换行符**|行由回车符和换行符的组合分隔。|  
|**回车**|行由回车符分隔。|  
|**{LF}**|行由换行符分隔。|  
|**分号 {;}**|行由分号分隔。|  
|**冒号 {:}**|行由冒号分隔。|  
|**跟{,}**|行由逗号分隔。|  
|**选项卡 {t}**|行由制表符分隔。|  
|**竖线 {&#124;}**。|行由竖线分隔。|  
  
 **重置列**  
 通过单击“重置列”**** 可以删除除原始列之外的所有列。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [多平面文件连接管理器编辑器 &#40;常规页面&#41;](general-page-of-integration-services-designers-options.md)   
 [多平面文件连接管理器编辑器 &#40;高级页面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [多平面文件连接管理器编辑器（“预览”页）](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
