---
title: 脚本转换编辑器（"脚本" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script Transformation Editor
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f172aa778cbaa959671da870521641147186f571
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964037"
---
# <a name="script-transformation-editor-script-page"></a>脚本转换编辑器（“脚本”页）
  可以使用 **“脚本转换编辑器”** 对话框的 **“脚本”** 选项卡指定脚本及相关属性。  
  
 若要了解有关脚本组件的详细信息，请参阅 [Script Component](data-flow/transformations/script-component.md) 和 [Configuring the Script Component in the Script Component Editor](extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。 若要了解如何对脚本组件进行编程，请参阅 [使用脚本组件扩展数据流](extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
## <a name="options"></a>选项  
 **属性**  
 查看和修改脚本转换的属性。 显示的许多属性是只读的。 您可以修改以下属性：  
  
|值|描述|  
|-----------|-----------------|  
|**说明**|说明脚本转换的用途。|  
|**LocaleID**|指定区域设置，以便为排序以及日期和时间转换提供区域特定的信息。|  
|**名称**|为组件键入说明性名称。|  
|**ValidateExternalMetadata**|指示在设计时脚本转换是否要根据外部数据源对列的元数据进行验证。 如果值为 `false`，则会将验证延迟到执行时。|  
|**ReadOnlyVariables**|以逗号分隔的形式键入一列可供脚本转换只读访问的变量。<br /><br /> 注意：变量名称区分大小写。|  
|**ReadWriteVariables**|以逗号分隔的形式键入一列可供脚本转换读/写访问的变量。<br /><br /> 注意：变量名称区分大小写。|  
|**ScriptLanguage**|选择脚本组件要使用的脚本语言。<br /><br /> 若要设置脚本组件和脚本任务的默认脚本语言，请使用 **“选项”** 对话框的 **“常规”** 页上的 **“脚本语言”** 选项。 有关详细信息，请参阅 [General Page](general-page-of-integration-services-designers-options.md)。|  
|**UserComponentTypeName**|指定 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> 类和支持 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 基础结构的 `Microsoft.SqlServer.TxScript` 程序集。|  
  
 **编辑脚本**  
 使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for APPLICATIONS （VSTA）创建或修改脚本。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [选择脚本组件类型](../../2014/integration-services/select-script-component-type.md)   
 [脚本转换编辑器 &#40;输入列 "页&#41;](../../2014/integration-services/script-transformation-editor-input-columns-page.md)   
 [脚本转换编辑器 &#40;"输入和输出" 页&#41;](../../2014/integration-services/script-transformation-editor-inputs-and-outputs-page.md)   
 [脚本转换编辑器 &#40;连接管理器页&#41;](../../2014/integration-services/script-transformation-editor-connection-managers-page.md)   
 [其他脚本组件示例](extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  
