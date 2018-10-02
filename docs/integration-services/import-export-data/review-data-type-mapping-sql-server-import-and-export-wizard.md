---
title: 查看数据类型映射（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5ef44f25a923471eadbc14abcfb6586606638dd3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637915"
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>查看数据类型映射（SQL Server 导入和导出向导）
如果在“列映射”  对话框的“映射”  列表中指定了一个可能无法成功的数据类型映射， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导将显示“查看数据类型映射”  页。 在此页上，可查看为了使源数据与目标兼容向导必须执行的数据类型转换的相关详细信息。 此信息包括视觉提示，用于区分应成功的数据类型转换与可能导致错误或截断的转换。 对于每个转换，你都可以决定是否接受向导建议的转换，也可以指定如何处理可能发生的错误。   
  
> [!TIP]
> 无法在“查看数据类型映射”  页上更改数据类型映射。 但是，可以单击“后退”  返回到“选择源表和源视图”  页，然后单击“编辑映射”  再次打开“列映射”  对话框。 在“列映射”  对话框中，可以指定更有可能成功的数据类型映射。 若要再次查看“列映射”  对话框，请参阅 [列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>“查看数据类型映射”页的屏幕截图
 以下屏幕截图显示了向导的“查看数据类型映射”页的一个示例。
 
 在此示例中:
 -   用户在“列映射”对话框中指定了可能不成功的映射。
 -   “表”  列表中行上的警告图标指示，在将查询结果中的至少一列数据转换为目标表中的兼容数据类型时出现问题。
 -   “数据类型映射”列表中第一行的警告图标指示，从源列的 int 数据类型映射到目标列的 smalldatetime 数据类型可能会导致数据丢失。
 
 ![导入和导出向导的“查看数据类型映射”页](../../integration-services/import-export-data/media/review-mapping.png "Review Data Type Mapping page of the Import and Export Wizard") 
 
## <a name="review-the-source-and-destination-tables"></a>查看源表和目标表  
 “查看数据类型映射”  页的上半部分是“表”  列表，其中列出了要从源复制到目标的表。 若要查看单个表的转换信息，请在“表”  列表中选择表。 所选表的各列的转换信息显示在“数据类型映射”网格中的下半部分页面。

在本示例中，用户提供的查询的结果将复制到目标的 Sales.CustomerNew2 表中。 警告图标指示，在将查询结果中的至少一列数据转换为目标表中的兼容数据类型时出现问题。

![查看映射 — 表](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 下表对“表”  列表中的列进行了说明。  
  
|“列”|描述|  
|------------|-----------------|  
|（源图标）|指示数据类型转换成功的可能性：<br /> - **绿色** 的复选标记图标指示向导认为此表的所有数据类型转换都将成功。<br />- **黄色** 的警告图标指示你应检查向导将执行的个别转换。 若要检查这些转换，可以选择表，然后在 **“数据类型映射”** 列表中检查单个列的转换。<br />- **红色** 的错误图标指示向导不能可靠地执行对此表的某些转换。|  
|**源**|源表的名称。|  
|（目标图标）|指示目标是已经存在还是将由向导创建：<br /> -   表图标指示目标是一个现有表。<br />-   阳光四射的表图标指示目标是一张新表，需要由向导创建。|  
|**目标**|目标表的名称。|  
  
## <a name="review-the-data-type-mappings"></a>查看数据类型映射  
 “查看数据类型映射”  页的中间部分是“数据类型映射”  列表。 此网格提供有关在上半部分页面的“表”列表中选择的源表中的列的详细转换信息。

在本示例中，源位置的每列都将复制到目标位置名称和数据类型相同的列中。 “数据类型映射”列表中第一行的警告图标指示，从源列的 int 数据类型映射到目标列的 smalldatetime 数据类型可能会导致数据丢失。
 
![查看映射 — 映射](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

下表对“数据类型映射”  列表中的列进行了说明。 

|“列”|描述|  
|------------|-----------------|  
|（转换图标）|指示数据类型转换成功的可能性：<br /> - **绿色** 的复选标记图标指示向导认为此列的数据类型转换会成功。<br />- **黄色** 的警告图标指示你应检查向导将执行的转换。 若要查看转换，请双击该列以查看“列转换详细信息”  对话框。 有关详细信息，请参阅 [“列转换详细信息”对话框](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)。<br />- **红色** 的错误图标指示向导不能可靠地执行转换。|  
|**源列**|源列的名称。|  
|**源类型**|源列的数据类型。|  
|**目标列**|目标列的名称。|  
|**目标类型**|目标列的数据类型。|  
|**转换**|指定是否继续执行计划的转换：<br /> -   选中复选框，可以使向导继续执行计划的转换。<br />-   清除复选框，可以取消数据类型转换。|  
|**出错时**|指定向导处理错误的方式：<br /> -   使用“出错时(全局)”  设置，可在此页的底部指定。<br />-   失败时出现一个错误，并停止导入或导出过程。<br />-   忽略错误。|  
|**截断时**|指定向导处理截断的方式：<br /> -   使用“截断时(全局)”  设置，可在此页的底部指定。<br />-   失败时出现一个错误，并停止导入或导出过程<br />-   忽略截断。|  

> [!TIP]
> 若要查看有关特定数据列转换的详细信息，请双击列表中的任意行。 将打开 **“列转换详细信息”** 对话框，并显示列的更多详细转换信息。 有关详细信息，请参阅 [“列转换详细信息”对话框](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)。
 
## <a name="specify-global-error-handling-options"></a>指定全局错误处理选项  
 “查看数据类型映射”  页的下半部分允许你指定默认应用于所有列的错误处理选项。 这些设置应用于在“数据类型映射”  列表的“出错时”  或“截断时”  列中选择了“使用全局”  的所有转换。   

本示例显示了两个全局错误处理选项的默认值。

![查看映射 — 错误](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **出错时(全局)**  
 指定向导处理错误的方式：  
 -   失败时出现一个错误，并停止导入或导出过程。 这是默认值。
 -   忽略错误并继续导入或导出过程。  
  
 **截断时(全局)**  
 指定向导处理数据截断的方式：  
 -   失败时出现一个错误，并停止导入或导出过程。 这是默认值。
 -   忽略截断并继续导入或导出过程。  
   
## <a name="whats-next"></a>下一步是什么？  
 在你查看警告、指定转换选项并指定如何处理错误之后，“查看数据类型映射”  页将返回到“列映射”  对话框。 有关详细信息，请参阅 [列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

