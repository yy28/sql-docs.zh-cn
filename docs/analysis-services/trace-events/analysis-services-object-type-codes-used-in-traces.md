---
title: Analysis Services 对象跟踪中使用的类型代码 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4d451b0348604c4b824bb5bf77c0e719990b1643
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34043941"
---
# <a name="analysis-services-object-type-codes-used-in-traces"></a>跟踪中使用的 Analysis Services 对象类型代码
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本页列举了 Analysis Services 数据模型中每个对象的对象类型（6 位数字）。 这些代码显示在跟踪日志中并用于标识与具体锁定关联的对象的类型。 例如，数据库中的锁定超时将指示对象类型 100002，这是数据库对象类型。  
  
> [!NOTE]  
>  下方所列代码的数量超过了实际将出现在跟踪日志中的数量。 下表是每个对象的类型代码的完整列表，但只有使用锁定的对象才会在跟踪日志中显示一个对象类型代码。  
  
## <a name="object-type-reference"></a>对象类型引用  
  
|对象类型|对象名称|  
|-----------------|-----------------|  
|100000|Server|  
|100001|Command|  
|100002|数据库|  
|100003|DataSource|  
|100004|DatabasePermission|  
|100005|角色|  
|100006|维度|  
|100007|DimensionAttribute|  
|100008|层次结构|  
|100009|级别|  
|100010|多维数据集|  
|100011|CubePermission|  
|100012|CubeDimension|  
|100013|CubeAttribute|  
|100014|CubeHierarchy|  
|100016|度量值组|  
|100017|MeasureGroupDimension|  
|100018|MeasureGroupAttribute|  
|100020|度量值|  
|100021|分区|  
|100025|AggregationDesign|  
|100026|AggregationDesignDimension|  
|100027|AggregationDesignAttribute|  
|100028|聚合|  
|100029|AggregationDimension|  
|100030|AggregationAttribute|  
|100032|MiningStructure|  
|100033|MiningStructureColumn|  
|100037|MiningModel|  
|100038|MiningModelColumn|  
|100039|AlgorithmParameter|  
|100041|MiningModelPermission|  
|100042|DimensionPermission|  
|100043|MiningStructurePermission|  
|100044|Assembly|  
|100045|DatabaseRole|  
|100046|AttributePermission|  
|100047|CubeAttributePermission|  
|100048|CellPermission|  
|100049|CubeDimensionPermission|  
|100050|跟踪|  
|100051|ServerAssembly|  
|100052|CubeAssembly|  
|100053|Command|  
|100054|KPI|  
|100055|DataSourceView|  
|100056|透视|  
|100100|CommandCollection|  
|100101|DatabaseCollection|  
|100102|DataSourceCollection|  
|100103|DatabasePermission|  
|100104|RoleCollection|  
|100105|DimensionCollection|  
|100106|DimensionAttributeCollection|  
|100107|HierarchyCollection|  
|100108|LevelCollection|  
|100109|CubeCollection|  
|100110|CubePermissionCollection|  
|100111|CubeDimensionCollection|  
|100112|CubeAttributeCollection|  
|100113|CubeHierarchyCollection|  
|100115|MeasureGroupCollection|  
|100116|MeasureGroupDimensionCollection|  
|100117|MeasureGroupAttributeCollection|  
|100119|MeasureCollection|  
|100120|PartitionCollection|  
|100124|AggregationDesignCollection|  
|100125|AggregationDesignDimensionCollection|  
|100126|AggregationDesignAttributeCollection|  
|100127|AggregationCollection|  
|100128|AggregationDimensionCollection|  
|100129|AggregationAttributeCollection|  
|100131|MiningStructureCollection|  
|100132|MiningStructureColumnCollection|  
|100136|MiningModelCollection|  
|100137|MiningModelColumnCollection|  
|100138|AlgorithmParameterCollection|  
|100140|MiningModelPermissionCollection|  
|100141|DimensionPermissionCollection|  
|100142|MiningStructurePermissionCollection|  
|100143|AssemblyCollection|  
|100144|DatabaseRoleCollecction|  
|100145|AttributePermissionCollection|  
|100146|CubeAttributePermissionCollection|  
|100147|CellPermissionCollection|  
|100148|CubeDimensionPermissionCollection|  
|100149|TraceCollection|  
|100150|ServerAssemblyCollection|  
|100151|CubeAssemblyCollection|  
|100152|CommandCollection|  
|100153|KpiCollection|  
|100154|DataSourceViewCollection|  
|100155|PerspectiveCollection|  
  
  
