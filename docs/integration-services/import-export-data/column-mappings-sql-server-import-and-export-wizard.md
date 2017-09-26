---
title: "列映射 （SQL Server 导入和导出向导） |Microsoft 文档"
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
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1ed879f21396c3c8d588307eaf087daea8c44c3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>列映射（SQL Server 导入和导出向导）
  选择现有表和视图进行复制或查看提供的查询之后，如果单击“编辑映射” ，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“列映射”  对话框。 此页上，你指定和配置要接收来自源列中复制的数据的目标列。 通常，你不必更改此页上的任何内容。
  
如果你不想要将所有列都复制所选的表中，你可以在此页执行的一点是排除不需要的列。 选择**忽略**中**目标**列**映射**你不想要复制的列的列表。
 
## <a name="screen-shot-of-the-column-mappings-page"></a>“列映射”页的屏幕截图 
 以下屏幕截图显示的示例**列映射**对话框中的向导。 
 
 在此示例中，由于已选中“创建目标表”  ，因此可看到向导将创建新的目标表。 默认情况下，该向导为相应的源列中为每个新的目标表相同的名称中的列、 数据类型和属性。 
  
 ![导入和导出向导的列映射页](../../integration-services/import-export-data/media/column-mappings.png "导入和导出向导的列映射页")  
  
## <a name="review-the-source-and-destination"></a>查看源和目标 
![列映射页、 源和目标部分](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **数据源**  
 所选的源表、 视图或查询。  
  
 **目标**  
 所选的目标表或视图。  

## <a name="optionally-create-a-new-destination-table"></a>（可选） 创建一个新的目标表
![列映射页，新表部分](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **创建目标表/文件**  
 如果不存在，请创建目标表。    
  
 **编辑 SQL**  
单击“编辑 SQL”  以打开“Create Table SQL 语句”  对话框。 使用自动生成 CREATE TABLE 语句，或对其进行修改您的要求。 如果手动更改此语句，则必须确保列映射的列表可识别更改。 有关详细信息，请参阅 [Create Table SQL 语句](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。  

### <a name="sometimes-these-options-are-disabled"></a>有时禁用了这些选项
**创建目标表/文件**选项和**编辑 SQL**按钮自动启用连接，或者自动禁用。

-   **启用。** 如果你指定**新**上的目标表**选择源表和源视图**页上，**创建目标表**会自动选择选项和**编辑 SQL**按钮处于启用状态。

-   **已禁用。** 如果你选择**现有**上的目标表**选择源表和源视图**页上，**创建目标表**选项和**编辑 SQL**按钮被禁用。 如果你想要创建新的目标表，请返回到**选择源表和源视图**页上，输入名称**新**表中**目标**列。  

## <a name="what-about-existing-data-in-the-destination"></a>目标中的现有数据呢？
![列映射页，选项部分](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **删除目标表/文件中的行**  
 指定在加载新数据之前是否清除现有表的数据。  
  
 **向目标表/文件中追加行**  
 指定是否将新数据追加到现有表的已存在数据中。  
  
 **删除并重新创建目标表**  
 选择此选项可以覆盖目标表。 当向导用于创建目标表时，此选项才可用。 仅当保存的是向导创建的包，然后再次运行该包时，才能删除并重新创建目标表。 当你想要多次测试你的设置时，该选项非常方便。
  
 **启用标识插入**  
 选择此选项可以将源数据中的现有标识值插入到目标表中的标识列。 默认情况下，通常不允许对目标标识列执行此操作。  
  
> [!TIP]
> 如果现有主键位于标识列、自动编号列或等效列中，则通常必须选择此选项以保留现有主键值。  否则目标标识列通常会分配新值。  

## <a name="keep-your-autonumber-or-identity-values"></a>保留自动编号或标识值
如果你要将数据导出具有 autonumber 列或标识列的数据例如，如果你要将数据导出从 Microsoft Access-请确保选择**启用标识插入**上文所述立即。

## <a name="review-column-mappings"></a>检查列映射
![列映射页，映射部分](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **映射**  
 显示数据源映射中的每个列如何映射到目标中列。
 
“映射”  列表包含以下列。  
  
-    **数据源**  
     查看每个源列。  
  
-   **目标**  
    查看映射的目标列或选择不同的列。
    
    你无需从源表中复制的所有列。 选择**忽略**列你想要跳过此列中。 在映射列之前，必须忽略所有不会被映射的列。  
  
-   **类型**  
    查看目标列的数据类型或选择不同的数据类型。
  
-   **可以为 Null**  
    指定目标列是否允许使用 null 值。  
  
-   **大小**  
    指定目标列中的字符数（如果适用）。  
  
-    **精度**  
    指定在目标列的即的数字位数的数字数据的精度，如果适用。  
  
 -   **小数位数**  
    指定在目标列的即的小数位数的数值数据的小数位数，如果适用。  
  
## <a name="whats-next"></a>下一步是什么？  
 查看并配置目标列，以接收来自源列中复制的数据，并单击后**确定**、**列映射**对话框中将返回到**选择源表和视图**页或**配置平面文件目标**页。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 或 [配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
  
 如果在“映射”  列表中指定了一个可能无法成功的映射，则“列映射”  对话框会使你进入“查看数据类型映射”  页。 在此页上，可查看警告、指定转换选项以及指定如何处理错误。 有关详细信息，请参阅 [查看数据类型映射](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


