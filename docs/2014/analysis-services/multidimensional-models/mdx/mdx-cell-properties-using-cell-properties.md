---
title: 使用单元属性 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- intrinsic cell properties [MDX]
- cells [MDX]
- cell properties [MDX]
- CELL PROPERTIES keyword
ms.assetid: a593c74d-8c5e-485e-bd92-08f9d22451d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b79e568f6dd8a3f0aac8e6f226f2b1719a41ff5
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148242"
---
# <a name="using-cell-properties-mdx"></a>使用单元属性 (MDX)
  多维表达式 (MDX) 中的单元属性包含有关多维数据源（如多维数据集）中的单元的内容和格式的信息。  
  
 MDX 支持使用 MDX SELECT 语句中的 CELL PROPERTIES 关键字来检索内部单元属性。 内部单元属性通常用于协助单元数据的直观显示。  
  
## <a name="cell-properties-keyword-syntax"></a>CELL PROPERTIES 关键字的语法  
 MDX `CELL PROPERTIES` 语句中的 `SELECT` 关键字使用下列语法：  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 下列语法显示了 `<cell_props>` 值的格式，以及此值如何将 `CELL PROPERTIES` 关键字与一个或多个内部单元属性一起使用：  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>支持的内部单元属性  
 下表列出了 `<property>` 值中使用的、支持的内部单元属性。  
  
|“属性”|Description|  
|--------------|-----------------|  
|`ACTION_TYPE`|指示单元中存在何种操作的位掩码。 此属性可以具有下列值之一：<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> 注意：对于在 where 子句中包含集的查询来说，不包含钻取操作。|  
|**BACK_COLOR**|用于显示 `VALUE` 或 `FORMATTED_VALUE` 属性的背景色。 有关详细信息，请参阅 [FORE_COLOR 和 BACK_COLOR 内容 (MDX)](mdx-cell-properties-fore-color-and-back-color-contents.md)。|  
|`CELL_ORDINAL`|数据集中单元的序号。|  
|**FONT_FLAGS**|字体的位掩码细节效果。 例如，值 5 表示粗体 (`MDFF_BOLD`) 和下划线 (`MDFF_UNDERLINE`) 字体效果的组合。 该值是对以下一个或多个常量执行按位 OR 操作的结果：<br /><br /> `MDFF_BOLD` = 1<br /><br /> `MDFF_ITALIC` = 2<br /><br /> `MDFF_UNDERLINE` = 4<br /><br /> `MDFF_STRIKEOUT` = 8|  
|**FONT_NAME**|用来显示 `VALUE` 或 `FORMATTED_VALUE` 属性的字体。|  
|**FONT_SIZE**|用来显示 `VALUE` 或 `FORMATTED_VALUE` 属性的字体大小。|  
|**FORE_COLOR**|用来显示 `VALUE` 或 `FORMATTED_VALUE` 属性的前景色。 有关详细信息，请参阅 [FORE_COLOR 和 BACK_COLOR 内容 (MDX)](mdx-cell-properties-fore-color-and-back-color-contents.md)。|  
|`FORMAT`|与 `FORMAT_STRING` 相同。|  
|`FORMAT_STRING`|用来创建 `FORMATTED_VALUE` 属性值的格式字符串。 有关详细信息，请参阅 [FORMAT_STRING 内容 (MDX)](mdx-cell-properties-format-string-contents.md)。|  
|`FORMATTED_VALUE`|表示 `VALUE` 属性的格式化显示的字符串。|  
|`LANGUAGE`|应用 `FORMAT_STRING` 的区域设置。 `LANGUAGE` 通常用于进行货币转换。|  
|`UPDATEABLE`|指示单元是否可更新的值。 此属性可以具有下列值之一：<br /><br /> `MD_MASK_ENABLED` (0x00000000) 可更新单元。<br /><br /> `MD_MASK_NOT_ENABLED` (0x10000000) 不能更新单元。<br /><br /> `CELL_UPDATE_ENABLED` (0x00000001) 可在单元集中更新单元格。<br /><br /> `CELL_UPDATE_ENABLED_WITH_UPDATE` (0x00000002) 可使用 update 语句更新单元。 如果更新的叶单元未启用写操作，更新可能会失败。<br /><br /> `CELL_UPDATE_NOT_ENABLED_FORMULA` (0x10000001) 不能为该单元格更新，因为该单元格有一个计算的成员在其坐标中;该单元格与一组检索到在 where 子句。 即使公式影响单元值或单元值上存在计算单元（在沿聚合路径的某个位置），仍可以更新单元。 在这种情况下，单元的最终值可能不是更新后的值，因为计算将影响结果。<br /><br /> `CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE` (0x10000002) 不能更新单元，因为不能更新非和度量值 （计数、 最小值、 最大值、 非重复计数、 半累加性）。<br /><br /> `CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE` (0x10000003) 不能更新单元，因为该单元格不存在的度量值的交集处是和与该度量值的度量值组无关的维度成员。<br /><br /> `CELL_UPDATE_NOT_ENABLED_SECURE` (0x10000005) 不能更新单元，因为该单元受保护。<br /><br /> `CELL_UPDATE_NOT_ENABLED_CALCLEVEL` (0x10000006) 保留供将来使用。<br /><br /> `CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE` (0x10000007) 由于内部原因不能更新单元。<br /><br /> `CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE` (0x10000009) 不能更新单元，因为在挖掘模型，间接或数据挖掘维度中不支持更新。|  
|`VALUE`|单元的未格式化值。|  
  
 只有 `CELL_ORDINAL`、`FORMATTED_VALUE` 和 `VALUE` 单元属性是必需的。 所有的单元属性（内部单元属性或特定于提供程序的单元属性）都在 `PROPERTIES` 架构行集中进行定义，包括它们的数据类型和提供程序支持。 有关详细信息`PROPERTIES`架构行集，请参阅[MDSCHEMA_PROPERTIES 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-properties-rowset)。  
  
 默认情况下，如果未使用 `CELL PROPERTIES` 关键字，返回的单元属性为 `VALUE`、`FORMATTED_VALUE` 和 `CELL_ORDINAL`（按这里显示的顺序）。 如果使用了 `CELL PROPERTIES` 关键字，将只返回用该关键字显式声明的那些单元属性。  
  
 下面的示例显示了 `CELL PROPERTIES` 关键字在 MDX 查询中的使用：  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 对于返回简化格式的行集的 MDX 查询，不返回单元属性；这种情况下，每个单元表现为似乎只返回了 `FORMATTED_VALUE` 单元属性。  
  
## <a name="setting-cell-properties"></a>设置单元属性  
 可以在各种位置的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中设置属性。 例如，可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]的多维数据集编辑器的“多维数据集结构”选项卡上为常规度量值设置格式字符串属性；可以为在多维数据集编辑器的“计算”选项卡上的多维数据集上定义的计算度量值设置相同属性；在查询的 WITH 子句中定义的计算度量值也具有其在此处定义的格式字符串。以下查询演示了如何在计算的度量值上设置单元属性：  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 查询基础知识 (Analysis Services)](mdx-query-fundamentals-analysis-services.md)  
  
  
