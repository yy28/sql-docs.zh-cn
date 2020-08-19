---
description: 列映射（SQL Server 导入和导出向导）
title: 列映射（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b74aaec705f3de493f105218adedffb173090ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484122"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>列映射（SQL Server 导入和导出向导）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  选择现有表和视图进行复制或查看提供的查询之后，如果单击“编辑映射” ****，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“列映射” **** 对话框。 在此页上，可指定并配置目标列以接收从源列复制的数据。 通常无需在此页上进行任何更改。
  
如果不想复制所选的表中的所有列，可以在此页上排除不需要的列。 对于不想复制的列，选择“映射”列表“目标”列中的“忽略”************。
 
## <a name="screen-shot-of-the-column-mappings-page"></a>“列映射”页的屏幕截图 
 以下屏幕截图显示向导的“列映射”对话框的示例****。 
 
 在此示例中，由于已选中“创建目标表” **** ，因此可看到向导将创建新的目标表。 默认情况下，向导为新目标表中的每个列提供与对应源列相同的名称、数据类型和属性。 
  
 ![“导入和导出向导”的列映射页面](../../integration-services/import-export-data/media/column-mappings.png "“导入和导出向导”的列映射页面")  
  
## <a name="review-the-source-and-destination"></a>查看源和目标 
![列映射页、源和目标部分](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **数据源**  
 所选的源表、视图或查询。  
  
 **目标**  
 所选的目标表或视图。  

## <a name="optionally-create-a-new-destination-table"></a>（可选）创建新目标表
![列映射页、新表部分](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **创建目标表/文件**  
 如果不存在目标表，则创建目标表。    
  
 **编辑 SQL**  
单击“编辑 SQL” **** 以打开“Create Table SQL 语句” **** 对话框。 使用自动生成的 CREATE TABLE 语句或根据用途修改它。 如果手动更改此语句，则必须确保列映射的列表可识别更改。 有关详细信息，请参阅 [Create Table SQL 语句](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。  

### <a name="sometimes-these-options-are-disabled"></a>有时会禁用这些选项
不会自动启用或自动禁用“创建目标表/文件”**** 选项和“编辑 SQL”**** 按钮。

-   **已启用。** 如果指定了“选择源表和视图”页上的新的目标表，则将自动选择“创建目标表”，以及启用“编辑 SQL”按钮   。

-   **已禁用。** 如果选择了“选择源表和视图”页上的现有的目标表，则将禁用“创建目标表”选项和“编辑 SQL”按钮****************。 如果要创建目标表，可后退到“选择源表和源视图”**** 页，在“目标”**** 列中输入新**** 表的名称。  

## <a name="what-about-existing-data-in-the-destination"></a>目标中的现有数据呢？
![列映射页、选项部分](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **删除目标表/文件中的行**  
 指定在加载新数据之前是否清除现有表的数据。  
  
 **向目标表/文件中追加行**  
 指定是否将新数据追加到现有表的已存在数据中。  
  
 **删除并重新创建目标表**  
 选择此选项可以覆盖目标表。 只有在使用该向导创建目标表时，该选项才可用。 仅当保存的是向导创建的包，然后再次运行该包时，才能删除并重新创建目标表。 当你想要多次测试你的设置时，该选项非常方便。
  
 **启用标识插入**  
 选择此选项可以将源数据中的现有标识值插入到目标表中的标识列。 默认情况下，通常不允许对目标标识列执行此操作。  
  
> [!TIP]
> 如果现有主键位于标识列、自动编号列或等效列中，则通常必须选择此选项以保留现有主键值。  否则目标标识列通常会分配新值。  

## <a name="keep-your-autonumber-or-identity-values"></a>保留自动编号或标识值
如果正在导出具有自动编号列或标识列的数据 — 例如，如果正在从 Microsoft Access 导出 — 请确保选择上述的“启用标识插入”****。

## <a name="review-column-mappings"></a>查看列映射
![列映射页、映射部分](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **映射**  
 显示数据源映射中的每个列如何映射到目标中列。
 
“映射” **** 列表包含以下列。  
  
-    **数据源**  
     查看每个源列。  
  
-   **目标**  
    查看映射的目标列或选择不同的列。
    
    不必从源表复制所有列。 针对要跳过的列，选中此列中的“忽略”****。 在映射列之前，必须忽略所有不会被映射的列。  
  
-   **类型**  
    查看目标列的数据类型或选择不同的数据类型。
  
-   **可以为 Null**  
    指定目标列是否允许使用 null 值。  
  
-   **大小**  
    指定目标列中的字符数（如果适用）。  
  
-    **精度**  
    指定目标列中的数值数据的精度（即数字位数）（如果适用）。  
  
 -   **缩放**  
    指定目标列中的数值数据的小数位数（即小数点后的位数）（如果适用）。  
  
## <a name="whats-next"></a>下一步操作  
 查看目标列并将其配置为接收从源列复制的数据之后，单击“确定”****，从“列映射”**** 对话框返回“选择源表和视图”**** 页或返回到“配置平面文件目标”**** 页。 有关详细信息，请参阅 [选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 或 [配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
  
 如果在“映射” **** 列表中指定了一个可能无法成功的映射，则“列映射” **** 对话框会使你进入“查看数据类型映射” **** 页。 在此页上，可查看警告、指定转换选项以及指定如何处理错误。 有关详细信息，请参阅 [查看数据类型映射](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

