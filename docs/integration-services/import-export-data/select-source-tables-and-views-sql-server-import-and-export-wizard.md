---
title: "选择源表和视图 （SQL Server 导入和导出向导） |Microsoft 文档"
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
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 96
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9a0c3c4fc8d41206ea077498dafb755e7b433a78
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>选择源表和源视图（SQL Server 导入和导出向导）
  指定要复制整个表或提供查询之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“选择源表和源视图” 。 在此页上，选择想要复制的现有表和视图。 然后将源表映射到新的或现有的目标表。 或者，还可查看单个列的映射并预览示例数据。

> [!TIP]
> 如果你必须将复制多个 SQL Server 数据库或 SQL Server 数据库对象，而非表和视图，而不是导入和导出向导使用复制数据库向导。 有关详细信息，请参阅 [使用复制数据库向导](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>屏幕快照-如果你要复制表  
 以下屏幕截图显示的示例**选择源表和源视图**以前选中向导页面**将数据从一个或多个表或视图复制**选项**指定表复制或查询**页。 在列表中，可以看到数据源中可用的所有表和视图。
 
在此示例中，**源**列表包含 AdventureWorks 示例数据库中的所有表。 所选的行显示用户想要复制**Sales.Customer**从源到新的表**Sales.CustomerNew**目标位置的表。 
   
 ![选择表导入和导出向导页](../../integration-services/import-export-data/media/select-tables1.png "导入和导出向导的选择表页")
  
## <a name="screen-shot---if-you-provided-a-query"></a>屏幕快照-如果你提供查询  
 以下屏幕截图显示的示例**选择源表和源视图**以前选中向导页面**编写查询以指定要传输的数据**选项**指定表复制或查询**页。 **源**列表包含只有一行，其中的项的名为`[Query]`表示提供的查询**提供源查询**页。
 
在此示例中，用户要将查询结果从源复制到目标上的 **Sales.CustomerNew** 表。  
    
 ![选择表导入和导出向导页](../../integration-services/import-export-data/media/select-tables2.png "导入和导出向导的选择表页")  

## <a name="select-source-and-destination-tables"></a>选择源表和目标表 
**源**  
使用这些复选框，可以从可用表和视图的列表中进行选择，以复制到目标。 默认情况下，可在不更改的情况下复制数据源中的数据。 如果创建新的目标表时，新表-即，列及其属性的列表-的架构的也会复制而不会从数据源的更改。

如果提供查询，该列表包含名为仅一个项`[Query]`。 

**目标**  
 从列表中为每个源表或查询选择目标表，或输入希望向导创建的新表的名称。 如果选择现有目标表，则该表必须具有与源数据兼容的数据类型的列。  

> [!NOTE]
> 如果此时在向导中暂停操作以使用外部工具（如  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]）在目标数据库中手动创建新表，则新表不会立即出现在可用目标表的列表中。 若要刷新目标表的列表，请退回到“选择目标”  页，重新选择目标数据库以刷新可用表和视图的列表，然后再次前进到“选择源表和源视图”  页。  

## <a name="optionally-review-column-mappings-and-preview-data"></a>（可选） 检查列映射和预览数据
**编辑映射**   
（可选） 单击**编辑映射**以显示**列映射**所选表的对话框。 使用“列映射”  对话框可执行以下操作，
-   查看单个列在源与目标之间的映射。
-   通过对不想复制的列选择“忽略”  ，可以仅复制列的子集。

有关详细信息，请参阅 [列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**预览**  
（可选） 单击**预览**预览中的示例数据的最多 200 行**预览数据**对话框。 这会确认向导将复制你想要复制的数据。 有关详细信息，请参阅 [预览数据](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
预览数据后，你可能想更改之前在向导页面中选择的选项。 若要进行这些更改，请返回到“选择源表和源视图”  页，单击“后退”  返回到前面可以更改选项的页面。  

## <a name="select-source-and-destination-tables-for-excel"></a>选择 Excel 的源表和目标表

### <a name="excel-source-tables"></a>Excel 源表
Excel 数据源的源表和视图的列表包括两种类型的 Excel 对象。
-   **工作表**。 工作表名称后跟美元符号 ($) ，例如， **“Sheet1$”**。
-   **命名区域。** 命名区域（如有）按名称列出。

如果想要加载来自特定的、未命名的单元格区域的数据（或将数据加载到其中）- 例如，来自或加载到 **[Sheet1$ A1: B4]**，则必须编写查询。 后退到“指定表复制或查询”  页，选择“编写查询以指定要传输的数据” 。

#### <a name="prepare-the-excel-source-data"></a>准备 Excel 源数据
无论是否将工作表或区域指定为源表，该驱动程序都将读取从工作表或区域左上角第一个非空单元开始的连续  单元块。 因此，源数据中不能有空行。 例如，列标题和数据行之间不能有空行。 如果工作表顶部数据上面的标题后跟有空行，则无法查询该工作表。 在 Excel 中，必须为区域内的数据分配名称，并查询命名区域而非工作表。

### <a name="excel-destination-tables"></a>Excel 目标表
如果将数据导出到 Excel，可以通过以下三种方式之一来指定目标。
-   **工作表。** 若要指定工作表，请将 $ 字符附加到表名称的末尾，并用分隔符包围字符串 - 例如， **[Sheet1$]**。
-   **命名区域。** 若要指定命名区域，只需使用区域名称 - 例如， **MyDataRange**。
-   **未命名区域。** 若要指定未命名的单元格区域，请将 $ 字符附加到表名称的末尾，添加区域说明，并用分隔符包围字符串 - 例如， **[Sheet1$ A1: B4]**。

## <a name="special-considerations-for-excel-sources-and-destinations"></a>Excel 源和目标的特殊注意事项
使用 Excel 作为源或目标时，最好单击“编辑映射”  并在“列映射”  页查看数据类型映射。 

**Excel 工作簿中的数据类型**。 Excel 不是一个典型的数据库。 它的列不具有固定的数据类型。 向导仅能识别 Excel 中一组有限的数据类型 - 数字、货币、布尔值，日期/时间、字符串（最多 255 个字符）和备注（255 个字符以上）。 向导示例一定数量的行 （通过默认情况下前, 八行） 中的现有的 Excel 数据源进行猜测在每个列的数据类型。

当向导必须执行从 Excel 加载或加载到 Excel 的显式数据类型转换时，它通常会显示“查看数据类型映射”  页，你可以在其中查看这些转换。 这些转换可能包括以下内容。
-   双精度 Excel 数值列与其他类型的数值列之间的转换。
-   在 255 个字符的 Excel 字符串列和不同长度的字符串列之间转换。
-   Unicode Excel 字符串列和使用特定的代码页的非 Unicode 字符串列之间的转换。

### <a name="special-considerations-for-excel-sources"></a>Excel 源的特殊注意事项
**导入的数据中的 null 值或缺少值**。 显示 Excel 列以包含采样的向导中的前八行中的混合的数据类型时例如，混合使用文本值的数字值向导选择多数的数据类型作为列的数据类型，并返回该容器的单元格的 null 值其他类型的 n 数据。 无法更改向导的此行为。

**导入的数据中截断的字符串**。 向导在确定 Excel 列是否包含文本数据时，它将基于前 8 行中采样的最长值来选择列的数据类型（字符串或备注）。 如果向导没有在其采样的行中发现任何长于 255 个字符的值，那么它会将该列视为 255 个字符的字符串的列而不是备注列，并截断长于 255 个字符的值。 若要从 memo 列而不发生截断导入数据，你必须确保的 memo 列包含超过 255 个字符由向导采样的前八行中的至少一个值。

### <a name="special-considerations-for-excel-destinations"></a>Excel 目标的特殊注意事项
**指定现有范围**。 如果范围具有更少当现有范围指定为目标时，收到一个错误*列*比源数据。 但是，如果你指定的范围具有更少*行*比源数据，向导将继续编写行，并扩展该范围定义以匹配新的行数。

**保存备注 (ntext) 数据**。 若要将大于 255 个字符的字符串成功地保存到 Excel 列中，向导必须将该目标列的数据类型识别为 **memo** ，而不是 **string**。
-   如果目标表已包含的数据行，通过该向导采样的前八行必须包含至少一个具有超过 255 个字符的 memo 列中值的行。
-   如果目标表创建的向导， **CREATE TABLE**语句必须使用**长文本**（或其同义词之一） 作为数据类型的 memo 列。 检查**CREATE TABLE**语句并对其进行修订，如有必要，通过单击**编辑 SQL**旁边**创建目标表**选项**列映射**页。

## <a name="whats-next"></a>下一步是什么？  
 选择现有表和视图以进行复制并将它们映射到其目标之后，下一页是“保存并运行包” 。 在此页上，你可以指定是否要立即运行复制操作。 根据你的配置，或许还可以保存向导创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，以便对其进行自定义并在以后重新使用。 有关详细信息，请参阅 [保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。
 
 ## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



