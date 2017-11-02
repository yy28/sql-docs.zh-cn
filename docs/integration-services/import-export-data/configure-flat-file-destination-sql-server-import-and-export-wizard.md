---
title: "配置平面文件目标 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 93fbd5e9429d06e3f011f6f0aff03d76a3db9000
ms.contentlocale: zh-cn
ms.lasthandoff: 10/13/2017

---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>配置平面文件目标（SQL Server 导入和导出向导）
  如果你选择平面文件目标，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导所示**配置平面文件目标**指定你想要将表复制之后，或者在提供的查询。 在此页上，可为目标平面文件指定格式设置选项。 （可选）查看单个列的映射并预览示例数据。  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>“配置平面文件目标”页面的屏幕截图  
 以下屏幕截图显示的示例**配置平面文件目标**向导页。
 
 在此示例中，用户已指定以下选项来创建一个典型的 CSV （逗号分隔值） 文件。
-   **行分隔符**。 在输出中的数据的每一行结尾回车符-换行符组合。
-   **列分隔符**。 用逗号分隔的每个行中的数据列。

 ![配置平面文件导入和导出向导页面](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>选取源表
 **源表或源视图**  
-   如果在前一页中指定你想要将表复制，从下拉列表选择源表或视图。
-   如果你提供一个查询，`"Query"`选择和是唯一的选项。  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>指定输出的行和列分隔符
 **行分隔符**  
 从分隔符的列表中进行选择，在输出中的行分隔符。 没有指定的选项*自定义*行分隔符。  
  
|值|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|使用回车符和换行符的组合分隔行。|  
|**{CR}**|使用回车符分隔行。|  
|**{LF}**|使用换行符分隔行。|  
|**分号 {;}**|使用分号分隔行。|  
|**冒号 {:}**|使用冒号分隔行。|  
|**逗号 {,}**|使用逗号分隔行。|  
|**制表符 {t}**|使用制表符分隔行。|  
|**竖线 {&#124;}**|使用竖线分隔行。|  
  
 **列分隔符**  
 从分隔符的列表中进行选择，用于分隔列在输出中。 没有指定的选项*自定义*列分隔符。  
  
|值|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|使用回车符和换行符的组合分隔列。|  
|**{CR}**|使用回车符分隔列。|  
|**{LF}**|使用换行符分隔列。|  
|**分号 {;}**|使用分号分隔列。|  
|**冒号 {:}**|使用冒号分隔列。|  
|**逗号 {,}**|使用逗号分隔列。|  
|**制表符 {t}**|使用制表符分隔列。|  
|**竖线 {&#124;}**|使用竖线分隔列。|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>（可选） 检查列映射和预览数据

**编辑映射**   
（可选） 单击**编辑映射**以显示**列映射**所选表的对话框。 使用“列映射”  对话框可执行以下操作。
-   查看单个列在源与目标之间的映射。
-   通过对不想复制的列选择“忽略”  ，可以仅复制列的子集。

有关详细信息，请参阅 [列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**预览**  
（可选） 单击**预览**预览中的示例数据的最多 200 行**预览数据**对话框。 这会确认向导将复制你想要复制的数据。 有关详细信息，请参阅 [预览数据](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
预览数据后，你可能想更改之前在向导页面中选择的选项。 若要进行这些更改，请返回到“配置平面文件目标”  页，然后单击“后退”  返回到前面可以更改选项的页面。  

## <a name="whats-next"></a>下一步是什么？  
 为目标平面文件指定格式设置选项之后，一页是“保存并执行包” 。 在此页上，你将指定是否要立即运行操作。 根据您的配置，你还可能无法保存您设置保存为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包以自定义它并以后重复使用它。 有关详细信息，请参阅 [保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  


