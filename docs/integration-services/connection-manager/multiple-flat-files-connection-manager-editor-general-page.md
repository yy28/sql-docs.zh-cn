---
title: "多平面文件连接管理器编辑器 （常规页） |Microsoft 文档"
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
- sql13.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84e8e23d349266c6c1195a10410085654548c64f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>多平面文件连接管理器编辑器（“常规”页）
  可以使用 **“多平面文件连接管理器编辑器”** 对话框的 **“常规”** 页，选择一组具有相同数据格式的文件并指定其数据格式。 多平面文件连接使得数据包可以连接到具有相同格式的一组文本文件。  
  
 若要了解有关多平面文件连接管理器的详细信息，请参阅 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
## <a name="options"></a>选项  
 **连接管理器名称**  
 为工作流中的“多平面文件连接”提供一个唯一名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **Description**  
 描述此连接。 最好按照连接的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **文件名**  
 键入要在“多平面文件连接”中使用的路径和文件名。 你可以使用通配符，如示例所示指定多个文件"c:\\*.txt"，或通过使用在竖线字符 (|) 分隔多个文件名称。 所有文件的数据格式必须相同。  
  
 **浏览**  
 通过定位文件来指定要在“多平面文件连接”中使用的文件名。 您可以选择多个文件。 所有文件的数据格式必须相同。  
  
 **区域设置**  
 指定与排序以及日期和时间转换设置相关的区域设置。  
  
 **Unicode**  
 指示是否使用 Unicode。 如果使用 Unicode，将不能指定代码页。  
  
 **代码页**  
 指定非 Unicode 文本的代码页。  
  
 **格式**  
 指示是否使用带分隔符、固定宽度或右边未对齐的格式。 所有文件的数据格式必须相同。  
  
|“值”|Description|  
|-----------|-----------------|  
|带分隔符|各列之间由在 **“列”** 页上指定的分隔符隔开。|  
|固定宽度|列的宽度固定，通过在 **“列”** 页上拖动标记线即可指定列的宽度。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由 **“列”** 页上指定的行分隔符进行分隔。|  
  
 **文本限定符**  
 指定要使用的文本限定符。 例如，您可以指定将文本包含在引号中。  
  
 **标题行分隔符**  
 从标题行的分隔符列表中选择，或输入分隔符文本。  
  
|“值”|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|标题行由回车符和换行符的组合分隔。|  
|**{CR}**|标题行由回车符分隔。|  
|**{LF}**|标题行由换行符分隔。|  
|**分号 {;}**|标题行由分号分隔。|  
|**冒号 {:}**|标题行由冒号分隔。|  
|**逗号 {,}**|标题行由逗号分隔。|  
|**制表符 {t}**|标题行由制表符分隔。|  
|**竖线 {|}。**|标题行由竖线分隔。|  
  
 **要跳过的标题行数**  
 指定要跳过的标题行数（如果有的话）。  
  
 **第一个数据行中的列名称**  
 指示在第一个数据行中是否要求列名或提供列名。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [多个平面文件连接管理器编辑器 &#40;列页&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [多个平面文件连接管理器编辑器 &#40;高级页 &#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [多个平面文件连接管理器编辑器 &#40;预览页&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
