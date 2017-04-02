---
title: "列映射（SQL Server 导入和导出向导） | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.columnmapandtransform.f1"
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# 列映射（SQL Server 导入和导出向导）
  选择现有表和视图进行复制或查看提供的查询之后，如果单击“编辑映射”，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“列映射”对话框。 在此页上，可指定并配置目标列以接收复制的数据。  
 
## <a name="screen-shot-of-the-column-mappings-page"></a>“列映射”页的屏幕截图 
 以下屏幕截图显示向导的“列映射”对话框。 
 
 在此示例中，由于已选中“创建目标表”，因此可看到向导将创建新的目标表。 默认情况下，新目标表中的每列都具有与对应源列相同的名称、数据类型和属性。 
  
 ![Column mappings page of the Import and Export Wizard](../../integration-services/import-export-data/media/column-mappings.png "Column mappings page of the Import and Export Wizard")  
  
## <a name="confirm-the-source-and-destination"></a>确认源和目标  
 **源**  
 标识所选的源表、视图或查询。  
  
 **目标**  
 标识所选的目标表或视图。  

## <a name="create-a-new-destination-table"></a>创建新的目标表
 **创建目标表/文件**  
 如果目标表不存在，则创建目标表。    
  
 **编辑 SQL**  
单击“编辑 SQL”以打开“Create Table SQL 语句”对话框。 使用默认 CREATE TABLE 语句或针对你的用途修改它。 如果手动更改此语句，则必须确保列映射的列表可识别更改。 有关详细信息，请参阅 [Create Table SQL 语句](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。  
  
 > [!TIP] 如果在“选择源表和源视图”页上指定了新的目标表，则会自动选择“创建目标表”选项，并且会启用“编辑 SQL”按钮。 否则，如果要创建目标表，则必须后退到“选择源表和源视图”页，在“目标”列中输入**新**表的名称。
>
> 如果“创建目标表”选项和“编辑 SQL”按钮在“列映射”页上处于禁用状态，则后退到“选择源表和源视图”页，在“目标”列中输入**新**表的名称。 指定新的目标表并单击“下一步”之后，会在“列映射”页上自动选择“创建目标表”选项，并且会启用“编辑 SQL”按钮。 选择“编辑 SQL”以显示“Create Table SQL 语句”对话框。  

## <a name="specify-options-for-existing-data-in-the-destination"></a>在目标中指定现有数据的选项
 **删除目标表/文件中的行**  
 指定在加载新数据之前是否清除现有表的数据。  
  
 **向目标表/文件中追加行**  
 指定是否将新数据追加到现有表的已存在数据中。  
  
 **删除并重新创建目标表**  
 选择此选项可以覆盖目标表。 只有在使用该向导创建目标表时，该选项才可用。 仅当保存的是向导创建的包，然后再次运行该包时，才能删除并重新创建目标表。 当你想要多次测试你的设置时，该选项非常方便。
  
 **启用标识插入**  
 选择此选项可以将源数据中的现有标识值插入到目标表中的标识列。 默认情况下，通常不允许对目标标识列执行此操作。  
  
> [!TIP] 如果现有主键位于标识列、自动编号列或等效列中，则通常必须选择此选项以保留现有主键值。  否则目标标识列通常会分配新值。  

## <a name="review-column-mappings-and-destination-data-types"></a>查看列映射和目标数据类型 
 **映射**  
 显示数据源映射中的每个列如何映射到目标中列。
 
 对于不要复制的列，可在“目标”栏中选择“忽略”。 不必复制表中的所有列。  
 
 ![列映射 - 映射](../../integration-services/import-export-data/media/column-mappings-mappings.png)
  
 “映射”列表包含以下列。  
  
-    **源**  
     查看可以在需要时为其指定转换设置的每个源列。  
  
-   **目标**  
    查看映射的目标列或选择不同的列。
    
    指定在复制操作期间是否忽略列。 通过在此栏中对要跳过的列选择“忽略”，可以仅复制列的子集。 在映射列之前，必须忽略所有不会被映射的列。  
  
-   **类型**  
    查看目标列的数据类型或选择不同的数据类型。
  
-   **可以为 Null**  
    指定目标列是否允许使用 null 值。  
  
-   **大小**  
    指定目标列中的字符数（如果适用）。  
  
-    **精度**  
    指定目标列中的数值数据的精度（即数字位数）（如果适用）。  
  
 -   **小数位数**  
    指定目标列中的数值数据的小数位数（即小数点后的位数）（如果适用）。  
  
## <a name="whats-next"></a>下一步是什么？  
 指定并配置目标列以接收复制的数据，以及单击“确定”之后，“列映射”对话框会使你返回到“选择源表和源视图”页或“配置平面文件目标”页。 有关详细信息，请参阅[选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)或[配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
  
 如果在“映射”列表中指定了一个可能无法成功的映射，则“列映射”对话框会使你进入“查看数据类型映射”页。 在此页上，可查看警告、指定转换选项以及指定如何处理错误。 有关详细信息，请参阅[查看数据类型映射](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
