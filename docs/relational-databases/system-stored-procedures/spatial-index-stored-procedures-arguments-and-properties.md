---
title: 空间索引的参数和属性存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31afdbb14229fa7c0eaf13f1b3a215e31356945f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528809"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>空间索引存储过程的参数和属性
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主题介绍空间索引存储过程的参数和属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
 有关特定空间索引存储过程的语法，请参阅下列主题：  
  
-   [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>参数  
`[ @tabname = ] 'tabname'` 是为其指定空间索引的限定或非限定名称。  
  
 仅当指定了限定表时才需要引号。 如果提供的是完全限定名称（包括数据库名称），则数据库名称必须是当前数据库的名称。 *tabname*是**nvarchar**(776)，无默认值。  
  
`[ @indexname = ] 'indexname'` 是指定的空间索引的名称。 *indexname*是**sysname** ，无默认值。  
  
`[ @verboseoutput = ] 'verboseoutput'` 是的属性名称和要返回的值的范围。  
  
 0 = 核心属性  
  
 \>0 = 所有属性  
  
 *verboseoutput*是**tinyint** ，无默认值。  
  
`[ @query_sample = ] 'query_sample'` 是一个有代表性的查询示例，可用于测试索引的有用性。 它可以是一个有代表性的对象或查询窗口。 *query_sample*是**geometry** ，无默认值。  
  
`[ @xml_output = ] 'xml_output'` 集 XML 片段中返回结果的输出参数。 *xml_output*是**xml** ，无默认值。  
  
## <a name="properties"></a>属性  
 设置**@verboseoutput** = 0，以返回下; 表中所示的核心属性**@verboseoutput** > 0，则返回空间索引的所有属性。  
  
 **Base_Table_Rows**  
 基表中的行数 值是**bigint**。  
  
 **Bounding_Box_xmin**  
 边框的空间索引的属性 X 的最小**几何图形**类型。 此属性的值为 NULL **geography**类型。 值是**float**。  
  
 **Bounding_Box_ymin**  
 边框属性的空间索引的 Y 的最小**几何图形**类型。 此属性的值为 NULL **geography**类型。 值是**float**。  
  
 **Bounding_Box_xmax**  
 边框的空间索引的属性 X 的最大**几何图形**类型。 此属性的值为 NULL **geography**类型。 值是**float**。  
  
 **Bounding_Box_ymax**  
 Y 的最大边框的空间索引的属性**几何图形**类型。 此属性的值为 NULL **geography**类型。 值是**float**。  
  
 **Grid_Size_Level_1**  
 空间索引的 1 级网格密度：  
  
 对于 LOW 为 16  
  
 对于 MEDIUM 为 64  
  
 对于 HIGH 为 256  
  
 值是**int**。  
  
 **Grid_Size_Level_2**  
 级别 2 的空间索引的网格密度：  
  
 对于 LOW 为 16  
  
 对于 MEDIUM 为 64  
  
 对于 HIGH 为 256  
  
 值是**int**。  
  
 **Grid_Size_Level_3**  
 空间索引的第三级网格密度：  
  
 对于 LOW 为 16  
  
 对于 MEDIUM 为 64  
  
 对于 HIGH 为 256  
  
 值是**int**。  
  
 **Grid_Size_Level_4**  
 空间索引的级别 4 网格密度：  
  
 对于 LOW 为 16  
  
 对于 MEDIUM 为 64  
  
 对于 HIGH 为 256  
  
 值是**int**。  
  
 **Cells_Per_Object**  
 每个对象的单元格数（索引属性）。 值是**int**。  
  
 **Total_Primary_Index_Rows**  
 索引中的行数。 值是**bigint**。  
  
 **Total_Primary_Index_Pages**  
 索引中的页数。 值是**bigint**。  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 索引行/数字基表行的数量。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 指示有代表性的查询示例是否处于的边界框的外部**几何图形**索引到根单元格 （级别 0 单元格）。 这可以是 0（不在级别 0 单元格中）或 1。 如果在级别 0 单元格中，则所调查的索引不是该查询示例的适当索引。 这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 级别 0 中分割的索引对象的单元格实例的数目 (根单元格，为在范围框之外**几何图形**)。 这是一个核心属性。 值是**bigint**。  
  
 有关**几何图形**索引，这会发生如果索引的边框小于数据域。 如果查询窗口落在了边框之外的次要筛选器，并且会降低索引性能，可能需要大量的级别 0 中的对象 (例如， **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**为 1)。 如果查询窗口落在边框之内，级别 0 中较多的对象数量实际上可能会提高索引的性能。  
  
 NULL 实例和空实例在级别 0 进行计数但是不会影响性能。 级别 0 的单元格数量将与基表处 NULL 实例和空实例的数量一样多。 有关**geography**索引，级别 0 将不多的单元格为 NULL 和空实例 + 1 单元格，因为该查询示例被计数为 1。  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 第 1 级精度进行分割的索引对象的单元格实例数量。 这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 级别 2 精度进行分割的索引对象的单元格实例数量。 这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 级别 3 精度进行分割的索引对象的单元格实例数量。 这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 使用级别 4 精度进行分割的索引对象的单元格实例数量。 这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 被位于分割级别 1 对象完全覆盖，因此都是该对象内部的单元格的数目。 （Cell_attributevalue 为 2。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 被位于分割级别 2 对象完全覆盖，因此都是该对象内部的单元格的数目。 （Cell_attribute 值为 2。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 被位于分割级别 3 某个对象完全覆盖，因此都是该对象内部的单元格的数目。 （Cell_attribute 值为 2。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 单元格的数目，这些单元格将被位于分割级别 4 的一个对象完全覆盖并因此位于该对象内部。 （Cell_attribute 值为 2。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 与位于分割级别 1 对象相交的单元格的数目。 （Cell_attribute 值为 1。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 与位于分割级别 2 对象相交的单元格的数目。 （Cell_attribute 值为 1。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 分割级别 3 处的对象的相交的单元格的数目。 （Cell_attribute 值为 1。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 分割级别 4 中与某个对象相交的单元格的数目。 （Cell_attribute 值为 1。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 指示查询示例是否位于边框之外的根单元格 0 中，但是与其相接触。 这是一个核心属性。 值是**bigint**。  
  
> [!NOTE]  
>  此信息只有在确定是否存在边框可能漏掉的靠近边框的对象时才有用。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 级别 0 中与边框接触的对象的数目。 （Cell_attribute 值为 0。）值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 对象位于分割级别 1 某个网格单元格边界接触的单元格的数目。 （Cell_attribute 值为 0。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 在第 2 级分割某个网格单元格边界接触的对象单元数。 （Cell_attribute 值为 0。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 对象位于分割级别 3 网格单元格边界接触的单元格的数目。 （Cell_attribute 值为 0。）这是一个核心属性。 值是**bigint**。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 分割级别 4 中与某个网格单元格边界接触的对象单元格的数目。 （Cell_attribute 值为 0。）这是一个核心属性。 值是**bigint**。  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 包含被某个对象覆盖的叶单元格的网格的总面积（全部叶单元格）百分比。  
  
 例如，某个对象被分割为位于 4 个不同网格级别的 10 个单元格，其覆盖的面积相当于总共 100 个叶单元格。 假设有 3 个被该对象完全覆盖的内部单元格。 被 3 个内部单元格覆盖的区域相当于 42 个叶单元格。 因此，被覆盖区域的百分比为 42%。 这个百分比很好地表明了索引中对象的破碎程度。  
  
 值是**float**。  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 与相同**Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**，这些是被部分覆盖的单元格。 值是**float**。  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 与相同**Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**只不过这些是边界单元格。 值是**float**。  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 每个标准化为叶网格的对象的平均单元格数 通过它可以了解对象的空间大小，或者说对象究竟有多么大。 值是**float**。  
  
 **Average_Objects_PerLeaf_GridCell**  
 索引的稀疏性。 每个叶单元格的对象的平均数。 值是**float**。  
  
 **Number_Of_SRIDs_Found**  
 索引和列中唯一 SRID 的数量。 值是**int**。  
  
 由于列可以包含多个 SRID，并且具有不同 SRID 的对象永远不相交，所以 SRID 的数量指出了索引的选择性。  
  
 **Width_Of_Cell_In_Level1**  
 索引网格中的单元格的宽度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Width_Of_Cell_In_Level2**  
 索引网格中的单元格的宽度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Width_Of_Cell_In_Level3**  
 索引网格中的单元格的宽度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Width_Of_Cell_In_Level4**  
 索引网格中的单元格的宽度属性。 度量单位由索引提供，并且取决于所索引数据的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level1**  
 索引网格中的单元格的高度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level2**  
 索引网格中的单元格的高度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level3**  
 索引网格中的单元格的高度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Height_Of_Cell_In_Level4**  
 索引网格中的单元格的高度属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level1**  
 索引网格中的单元格的面积属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level2**  
 索引网格中的单元格的面积属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level3**  
 索引网格中的单元格的面积属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **Area_Of_Cell_In_Level4**  
 索引网格中的单元格的面积属性。 度量单位由索引提供，并取决于索引数据的 SRID。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 第 1 级单元格边框的覆盖面积百分比。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 第 2 级单元格边框的覆盖面积百分比。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 第 3 级单元格边框的覆盖面积百分比。 值是**float**。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 级别 4 单元格边框的覆盖面积百分比。 值是**float**。  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 由主要筛选器选择的行数。 这是一个核心属性。 值是**bigint。**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 由内部筛选器选择的行数。 不会为这些行调用次要筛选器。 这是一个核心属性。 值是**bigint。**  
  
 返回的数目是仅适用于**STintersects**。  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 次要筛选器的调用次数。 这是一个核心属性。 值是**bigint。**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 如果在基表中有 N 行，并且被主要筛选器选择了 P 行，则会返回百分比形式的 (N-P)/N。 这是一个核心属性。 值是**float。**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 如果被主要筛选器选择了 P 行，并且被内部筛选器选择了 S 行，则会返回百分比形式的 S/P。 百分比越高，索引就能够越好地避免使用性能开销巨大的次要筛选器。 这是一个核心属性。 值是**float。**  
  
 **Number_Of_Rows_Output**  
 查询输出的行数。 这是一个核心属性。 值是**bigint。**  
  
 **Internal_Filter_Efficiency**  
 如果 O 是输出的行的数目，将返回百分比形式的 S/O。 这是一个核心属性。 值是**float。**  
  
 **Primary_Filter_Efficiency**  
 如果被主要筛选器和 O 选择了 P 行是输出行数，以百分比表示此 returnsO/P。 主要筛选器的效率越高，次要筛选所必须处理的误报就越少。 这是一个核心属性。 值是**float。**  
  
## <a name="permissions"></a>权限  
 用户必须是属于**公共**角色。 需要服务器和对象的 READ ACCESS 权限。 这适用于所有空间索引存储过程。  
  
## <a name="remarks"></a>备注  
 包含 NULL 值的属性未包含在返回集中。  
  
## <a name="examples"></a>示例  
 有关示例，请参阅下列主题：  
  
-   [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>要求  
  
## <a name="see-also"></a>请参阅  
 [空间索引存储过程&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [XQuery 基础知识](../../xquery/xquery-basics.md)   
 [XQuery 语言参考 (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)  
  
  
