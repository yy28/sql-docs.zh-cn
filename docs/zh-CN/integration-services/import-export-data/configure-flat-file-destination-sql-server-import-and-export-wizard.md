---
title: 配置平面文件目标（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0145a4393465431b68c6fbacfa50a16048384077
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>配置平面文件目标（SQL Server 导入和导出向导）
  如果选择了平面文件目标，则在指定要复制表或提供查询之后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“配置平面文件目标”。 在此页上，可为目标平面文件指定格式设置选项。 （可选）查看单个列的映射并预览示例数据。  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>“配置平面文件目标”页面的屏幕截图  
 以下屏幕截图显示向导“配置平面文件目标”页的示例。
 
 在此示例中，用户已指定以下选项来创建典型的 CSV （逗号分隔的值）文件。
-   **行分隔符**。 输出中的每行数据以回车和换行相结合的方式结尾。
-   **列分隔符**。 每行的数据列用逗号分隔。

 ![配置导入和导出向导的平面文件页](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>选择源表
 **源表或源视图**  
-   如果在前一页上指定了要复制表，从下拉列表选择源表或视图。
-   如果提供了一个查询，则选择 `"Query"` 且为唯一选项。  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>指定输出的行和列分隔符
 **行分隔符**  
 从分隔符的列表中选择，以分隔输出中的行。 没有指定自定义行分隔符的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|使用回车符和换行符的组合分隔行。|  
|**{CR}**|使用回车符分隔行。|  
|**{LF}**|使用换行符分隔行。|  
|**分号 {;}**|使用分号分隔行。|  
|**冒号 {:}**|使用冒号分隔行。|  
|**逗号 {,}**|使用逗号分隔行。|  
|**制表符 {t}**|使用制表符分隔行。|  
|**竖线 {|}**|使用竖线分隔行。|  
  
 **列分隔符**  
 从分隔符列表中进行选择，用于分隔输出中的列。 没有用于指定自定义列分隔符的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|使用回车符和换行符的组合分隔列。|  
|**{CR}**|使用回车符分隔列。|  
|**{LF}**|使用换行符分隔列。|  
|**分号 {;}**|使用分号分隔列。|  
|**冒号 {:}**|使用冒号分隔列。|  
|**逗号 {,}**|使用逗号分隔列。|  
|**制表符 {t}**|使用制表符分隔列。|  
|**竖线 {&#124;}。**|使用竖线分隔列。|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>（可选）查看列映射和预览数据

**编辑映射**   
（可选）对所选表单击“编辑映射”以显示“列映射”对话框。 使用“列映射”  对话框可执行以下操作。
-   查看单个列在源与目标之间的映射。
-   通过对不想复制的列选择“忽略”  ，可以仅复制列的子集。

有关详细信息，请参阅 [列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**预览**  
（可选）单击“预览”以在“预览数据”对话框中预览最多 200 行的示例数据。 这会确认向导将复制你想要复制的数据。 有关详细信息，请参阅 [预览数据](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
预览数据后，你可能想更改之前在向导页面中选择的选项。 若要进行这些更改，请返回到“配置平面文件目标”  页，然后单击“后退”  返回到前面可以更改选项的页面。  

## <a name="whats-next"></a>下一步是什么？  
 为目标平面文件指定格式设置选项之后，一页是“保存并执行包” 。 在此页上，你将指定是否要立即运行操作。 根据配置，或许还可以将设置保存为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，以对其进行自定义并在以后重新使用。 有关详细信息，请参阅 [保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  

