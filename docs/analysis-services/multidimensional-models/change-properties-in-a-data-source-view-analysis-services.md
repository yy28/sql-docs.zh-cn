---
title: "更改数据源视图 (Analysis Services) 中的属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- friendly names [Analysis Services]
- names [Analysis Services], data source views
- viewing tables
- displaying tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 4ccdabea-9c4d-460d-ba78-d23068143696
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f17e0880839470e128266ae62993bceeb4457c3e
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="change-properties-in-a-data-source-view-analysis-services"></a>在数据源视图中更改属性 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在使用数据源视图向导定义数据源视图并将表、视图、命名计算和命名查询添加到数据源视图后，可能需要更改与下列各项相关的属性：  
  
-   数据源视图匹配条件  
  
-   高级数据源视图选项  
  
-   对象名  
  
-   对象元数据  
  
 还可以查看从数据源中检索的无法修改的对象元数据。  
  
## <a name="viewing-or-changing-data-source-view-properties"></a>查看或更改数据源视图属性  
 最初定义数据源视图时，数据源视图向导除了设置数据源视图说明之外，还会设置数据源视图属性。 下表列出并说明了数据源视图的属性。  
  
> [!NOTE]  
>  “属性”窗格显示 .dsv 文件以及 DSV 对象的属性。 若要查看对象的属性，请在解决方案资源管理器中双击它。 将更新“属性”窗格以反映您在下表中看到的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|数据源|指定要查看其属性的数据源视图中的数据源|  
|Description|指定数据源视图的说明|  
|名称|指定在解决方案资源管理器或 Analysis Services 数据库中显示的数据源视图的名称。 可以在此或在解决方案资源管理器中更改数据源视图的名称。|  
|NameMatchingCriteria|数据源的名称匹配条件。 如果数据源视图向导检测到主键-外键关系，则默认值为（无）。 无论数据源视图向导是否设置此属性，都可以在此指定一个值。 如果数据库关系存在并指定了名称匹配条件，则可以使用这些关系和条件来推断现有表和新添加的表之间的关系。|  
|RetrieveRelationships|指定是否从数据库中检索关系。 默认值为 True。|  
|SchemaRestriction|指定对从数据源中检索的架构的限制（如果有）。 默认情况下，不存在架构限制。|  
  
## <a name="viewing-or-changing-datatable-properties"></a>查看或更改 DataTable 属性  
 **DataTable** 属性是数据源视图中表、视图和命名查询的属性。 将上述任一对象添加到数据源视图时，便会设置这些属性。 下表列出并说明了数据源视图中 **DataTable** 对象的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|AllowChangesDuringGeneration|指定在重新生成过程中架构生成向导是否有权覆盖数据源视图表。 此属性仅存在于最初由架构生成向导生成的表中。 有关详细信息，请参阅 [了解增量生成](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)。|  
|DataSource|为对象指定数据源。 您无法编辑此属性。|  
|Description|为表、视图或命名查询指定说明。 如果基础数据库表或视图具有存储为扩展属性的说明，则会显示此值。 您可以编辑此属性。|  
|FriendlyName|为表或视图指定更便于用户理解或与主题区域更相关的名称。 默认情况下，表或视图的 **FriendlyName** 属性与表或视图的 **“名称”** 属性相同。 基于表或视图定义对象名时，OLAP 和数据挖掘对象会使用 **FriendlyName** 属性。 您可以编辑此属性。|  
|名称|指定基础表或视图的名称，或者指定命名查询的名称。 基于命名查询定义对象名时，OLAP 和数据挖掘对象会使用 **“名称”** 属性。 只能针对命名查询编辑此属性。|  
|QueryDefinition|指定命名查询定义。 此属性仅适用于命名查询，并且不可直接编辑。 若要编辑此属性，可以编辑命名查询本身。|  
|架构|指定适用于表、视图或命名查询的数据库架构。 此属性不可编辑。|  
|TableType|为表、视图或命名查询指定表的类型。 此属性不可编辑。|  
  
## <a name="viewing-or-changing-datacolumn-properties"></a>查看或更改 DataColumn 属性  
 **DataColumn** 属性是数据源视图的表、视图和命名查询中列的属性。 将上述任一对象从基础表、视图或命名查询添加到数据源视图时，或者上述任一对象在由命名计算定义后添加到数据源视图时，便会设置这些属性。 下表列出并说明了数据源视图中 **DataColumn** 对象的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|AllowNull|基于基础表、值或命名查询中的列指定列的为空性属性。 此属性不可编辑。|  
|DataType|基于基础表、值或命名查询中的列指定列的数据类型。 此属性不可直接编辑。 但是，如果需要更改表或视图中列的数据类型，则使用可将列转换为所需数据类型的命名查询来替换表。|  
|DateTimeMode|为 **DateTime** 列指定数据序列化格式。 默认值为 **UnspecifiedLocal**。 此属性可编辑。|  
|Description|指定列的说明。 如果基础数据库列具有存储为扩展属性的说明，则会显示此值。 您可以编辑此属性。|  
|FriendlyName|为表或视图中的列指定更便于用户理解或与主题区域更相关的名称。 默认情况下，表或视图中列的 **FriendlyName** 属性与列的 **“名称”** 属性相同。 基于表或视图中的列定义属性时，OLAP 和数据挖掘对象会使用 **FriendlyName** 属性。 您可以编辑此属性。|  
|长度|基于基础表或视图的列中的数据指定列的最大长度。|  
|名称|指定基础列的名称，或者指定命名计算的名称。 基于命名计算定义属性时，OLAP 和数据挖掘对象会使用 **“名称”** 属性。 只能针对命名计算编辑此属性。|  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [使用数据源视图设计器 &#40; 中的关系图Analysis Services &#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
