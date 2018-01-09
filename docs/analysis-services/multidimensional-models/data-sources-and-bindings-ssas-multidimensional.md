---
title: "数据源和绑定 (SSAS 多维) |Microsoft 文档"
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
- data source views [Analysis Services], bindings
- DSO, bindings
- Analysis Services Scripting Language, data sources
- cubes [Analysis Services], bindings
- OLAP mining models [Analysis Services Scripting Language]
- bindings [Analysis Services Scripting Language]
- rebindings [Analysis Services Scripting Language]
- ASSL, bindings
- relational mining models [ASSL]
- data sources [Analysis Services Scripting Language]
- ASSL, data sources
- dimensions [Analysis Services], bindings
- measures [Analysis Services], bindings
- relational data sources [Analysis Services Scripting Language]
- Analysis Services Scripting Language, bindings
- chaptered rowsets
- granularity
- mining models [Analysis Services], data sources
- inline bindings [ASSL]
- out-of-line bindings
- measure groups [Analysis Services], bindings
- partitions [Analysis Services], bindings
ms.assetid: bc028030-dda2-4660-b818-c3160d79fd6d
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 49a0e62db64a1eb0dc27df9785a90234a4b39207
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>数据源和绑定（SSAS 多维）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]多维数据集、 维度和其他[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象可以绑定到数据源。 数据源可为以下对象之一：  
  
-   关系数据源。  
  
-   可输出行集（或分章节的行集）的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管道。  
  
 数据源的表示方式因数据源类型而异。 例如，关系数据源是通过连接字符串区分的。 有关数据源的详细信息，请参阅 [Data Sources in Multidimensional Models](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)。  
  
 无论使用何种数据源，数据源视图 (DSV) 均包含有数据源的元数据。 因此，多维数据集或其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的绑定都表示为到 DSV 的绑定。 这些绑定可包括到逻辑对象的绑定，如数据源中实际并不存在的视图、计算列和关系等对象。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 要先向 DSV 添加封装表达式的计算列，然后再在 DSV 中将相应的 OLAP 度量值绑定到该计算列。 有关 DSV 的详细信息，请参阅 [Data Source Views in Multidimensional Models](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
 每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象都有其自己绑定到数据源的方式。 此外，这些对象的数据绑定和数据源的定义既可以以内联方式随数据绑定对象（如维度）的定义一起提供，也可以作为单独的定义集以外部方式提供。  
  
## <a name="analysis-services-data-types"></a>Analysis Services 数据类型  
 在绑定中使用的数据类型必须与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所支持的数据类型匹配。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中定义了下列数据类型：  
  
|Analysis Services 数据类型|Description|  
|---------------------------------|-----------------|  
|BigInt|64 位有符号整数。 此数据类型映射到 Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Int64 数据类型和 OLE DB 中的 DBTYPE_I8 数据类型。|  
|Bool|一个布尔值。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Boolean 数据类型和 OLE DB 中的 DBTYPE_BOOL 数据类型。|  
|货币|货币值，范围在 -263（或 -922,337,203,685,477.5808）到 263-1（或 +922,337,203,685,477.5807）之间，精确到货币单位的万分之一。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Decimal 数据类型和 OLE DB 中的 DBTYPE_CY 数据类型。|  
|date|日期数据，以双精度浮点数存储。 整数部分是自 1899 年 12 月 30 日以来的天数，而小数部分是不足一天的部分。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 DateTime 数据类型和 OLE DB 中的 DBTYPE_DATE 数据类型。|  
|双精度|双精度浮点数，范围在 -1.79E +308 到 1.79E +308 之间。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Double 数据类型或 OLE DB 中的 DBTYPE_R8 数据类型。|  
|Integer|32 位有符号整数。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Int32 数据类型和 OLE DB 中的 DBTYPE_I4 数据类型。|  
|Single|单精度浮点数，范围在 -3.40E +38 到 3.40E +38 之间。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Single 数据类型和 OLE DB 中的 DBTYPE_R4 数据类型。|  
|SmallInt|16 位有符号整数。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 Int16 数据类型和 OLE DB 中的 DBTYPE_I2 数据类型。|  
|TinyInt|一个 8 位有符号整数。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 SByte 数据类型和 OLE DB 中 DBTYPE_I1 数据类型。<br /><br /> 注意：如果数据源包含的字段属于 tinyint 数据类型，并且 AutoIncrement 属性设置为 True，则它们会在数据源视图中转换成整数。|  
|UnsignedBigInt|一个 64 位无符号整数。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 UInt64 数据类型和 OLE DB 中的 DBTYPE_UI8 数据类型。|  
|UnsignedInt|32 位无符号整数。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 UInt32 数据类型和 OLE DB 中的 DBTYPE_UI4 数据类型。|  
|UnsignedSmallInt|16 位无符号整数。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 UInt16 数据类型和 OLE DB 中的 DBTYPE_UI2 数据类型。|  
|WChar|Unicode 字符的以 Null 值结束的流。 此数据类型映射到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 String 数据类型和 OLE DB 中的 DBTYPE_WSTR 数据类型。|  
  
 从数据源接收的所有数据都转换为绑定中指定的 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 类型（通常在处理过程中）。 如果无法执行转换（例如，从 String 转换到 Int），则会产生错误。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 通常将绑定中的数据类型设置为与数据源中的源类型最匹配的数据类型。 例如，SQL types Date、DateTime、SmallDateTime、DateTime2、DateTimeOffset 映射到 [!INCLUDE[ssAS](../../includes/ssas-md.md)] Date，SQL type Time 映射到 String。  
  
## <a name="bindings-for-dimensions"></a>维度的绑定  
 维度的每个属性都绑定到 DSV 中的某一列。 虽然一个维度的所有属性必须来自同一个数据源。 但这些属性却可绑定到不同表中的列。 各表之间的关系在 DSV 中定义。 如果同一表中同时存在多个关系集，则可能必须在 DSV 中引入一个命名查询，将其作为“别名”表使用。 在 DSV 中，可使用命名计算和命名查询来定义表达式和筛选器。  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>度量值组、度量值和分区的绑定  
 所有度量值组都具有以下默认绑定：  
  
-   度量值组绑定到 DSV 中的表（例如， **MeasureGroup.Source**）。  
  
-   所有度量值都绑定到该表中的列（例如，**Measure.ValueColumn.Source**）。  
  
-   每个度量值组维度都具有一组定义度量值组粒度的“粒度属性”  。 所有这些属性都必须绑定到包含属性键的事实数据表中的列。 （有关粒度属性的详细信息，请参阅本主题后面的“MeasureGroup 粒度属性”。）  
  
 对于每个分区，都可以有选择地重写这些默认绑定。 每个分区都可以指定不同的数据源、表、查询名称或筛选表达式。 最常见的分区策略是使用相同的数据源，逐个分区重写表。 其他的方法包括对每个分区应用不同的筛选器或更改数据源。  
  
 必须在 DSV 中定义默认数据源，以便提供包括关系的详细信息在内的架构信息。 在分区级别上指定的所有其他表或查询均无需在 DSV 中列出，但它们的架构必须与为该度量值组定义的默认表的架构相同，或者至少必须包含度量值或粒度属性所使用的所有列。 度量值和粒度属性无法在分区级别上重写，它们被假定为与度量值组定义的列相同。 因此，如果分区实际使用的数据源具有不同的架构，则为该分区定义的 **TableDefinition** 查询就必须使用与度量值组所用架构相同的架构。  
  
### <a name="measuregroup-granularity-attributes"></a>MeasureGroup 粒度属性  
 如果度量值组的粒度与数据库中的已知粒度匹配，并且事实数据表与维度表之间具有直接关系，则只需将粒度属性绑定到相应的外键列或事实数据表中的列。 例如，请看下面的事实数据表和维度表：  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 如果通过订购的产品进行分析，则对于销售维度角色的订购产品，应将产品粒度属性绑定到 Sales.OrderedProductID。  
  
 但有时， **GranularityAttributes** 可能不作为事实数据表中的列而存在。 例如，在下列情况中， **GranularityAttributes** 可能不作为列而存在：  
  
-   OLAP 粒度比数据源中的粒度更粗。  
  
-   事实数据表与维度表之间有中间表。  
  
-   维度键与维度表中的主键不相同。  
  
 在所有这些情况中，都必须定义 DSV，以使事实数据表中存在 GranularityAttributes。 例如，可以引入命名查询或计算列。  
  
 例如，在上面的示例表中，如果粒度按类别列出，则可引入销售视图：  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 在这种情况下，GranularityAttribute 类别将绑定到 SalesWithCategory.OrderedProductCategory。  
  
### <a name="migrating-from-decision-support-objects"></a>从决策支持对象迁移  
 决策支持对象 (DSO) 8.0 允许将 **PartitionMeasures** 重新绑定。 因此，这些情况下的迁移策略就是构造相应的查询。  
  
 同样，虽然 DSO 8.0 也支持重新绑定维度属性，但在分区内是无法进行此种重新绑定的。 这些情况下的迁移策略就是在 DSV 中定义必要的命名查询，以使 DSV 中存在的分区的表和列与维度所使用的表和列相同。 这些情况可能需要使用简单的迁移；在简单迁移中，From/Join/Filter 子句将映射到单个命名查询，而不是一组结构化的相关表。 由于即使分区使用同一数据源，DSO 8.0 也支持重新绑定 PartitionDimensions，因此迁移还可能需要同一数据源的多个 DSV。  
  
 在 DSO 8.0 中，有两种表达相应的绑定的方法：绑定到维度表中的主键或绑定到事实数据表中的外键，具体取决于是否使用优化架构。 在 ASSL 中，这两种方法是没有区别的。  
  
 此绑定方法甚至还可用于其所使用的数据源不包含维度表的分区，因为只会绑定到事实数据表中的外键列，而不会绑定到维度表的主键列。  
  
## <a name="bindings-for-mining-models"></a>挖掘模型的绑定  
 挖掘模型分为关系挖掘模型和 OLAP 挖掘模型。 关系挖掘模型的数据绑定与 OLAP 挖掘模型的绑定区别很大。  
  
### <a name="bindings-for-a-relational-mining-model"></a>关系挖掘模型的绑定  
 关系挖掘模型依靠 DSV 中定义的关系来解决列与数据源的绑定配对问题。 在关系挖掘模型中，数据绑定遵循以下规则：  
  
-   每个非嵌套表列绑定到事例表中的列或与事例表有关的表中的列（遵循多对一或一对一关系）。 DSV 定义各表之间的关系。  
  
-   所有嵌套表列绑定到源表。 然后，将嵌套表列所拥有的列绑定到该源表中的列或与该源表相关的表中的列。 （同样，此绑定也遵循多对一或一对一关系。）挖掘模型绑定不提供指向嵌套表的联接路径。 这些信息是由 DSV 中定义的关系提供的。  
  
### <a name="bindings-for-an-olap-mining-model"></a>OLAP 挖掘模型的绑定  
 OLAP 挖掘模型没有功能类似于 DSV 的视图。 因此，数据绑定必须明确确定列与数据源之间的绑定对应关系。 例如，挖掘模型可基于销售多维数据集，列可基于数量、金额和产品名称。 此外，挖掘模型还可基于产品，列还可基于产品名称、产品颜色和含有销售量的嵌套表。  
  
 在 OLAP 挖掘模型中，数据绑定遵循以下规则：  
  
-   每个非嵌套表列绑定到多维数据集的度量值，绑定到该多维数据集维度的属性（指定 **CubeDimension** 以消除维度角色的多义性），或者绑定到维度的属性。  
  
-   每个嵌套表列绑定到 **CubeDimension**。 也就是说，它定义如何从维度导航到相关多维数据集，或如何从多维数据集导航到该多维数据集的一个维度（在出现嵌套表的少数情况下）。  
  
## <a name="out-of-line-bindings"></a>外部绑定  
 外部绑定使您可以临时更改命令持续时间的现有数据绑定。 外部绑定指命令中包含的但不会持久化的绑定。 外部绑定只可在执行特定命令时才能应用。 相比之下，内联绑定包含在 ASSL 对象定义中，会随对象定义在服务器元数据内持久保留。  
  
 ASSL 允许在 **Process** 命令（非批处理中的命令）或 **Batch** 命令中指定外部绑定。 如果在 **Batch** 命令中指定外部绑定，则 **Batch** 命令中指定的所有绑定将创建新的绑定上下文，批处理中的所有 **Process** 命令都将在该上下文中运行。 由于有 **Process** 命令，所以此新绑定上下文会包含间接处理的对象。  
  
 如果在命令中指定外部绑定，则这些绑定将覆盖指定对象的持久化 DDL 中包含的内联绑定。 这些已处理对象既可能包含 **Process** 命令中直接命名的对象，也可能包含随该处理操作自动启动的其他对象。  
  
 外部绑定是通过将可选 **Bindings** 集合对象与处理命令包含在一起而指定的。 可选的 **Bindings** 集合包含以下元素。  
  
|“属性”|基数|类型|Description|  
|--------------|-----------------|----------|-----------------|  
|**Binding**|0-n|**Binding**|提供新绑定的集合。|  
|**DataSource**|0-1|**DataSource**|替换服务器中本应使用的 **DataSource** 。|  
|**DataSourceView**|0-1|**DataSourceView**|替换服务器中本应使用 **DataSourceView** <br /><br /> 。|  
  
 与外部绑定相关的所有元素都是可选的。 对于所有未指定的元素，ASSL 将应用持久化对象的 DDL 中包含的规范。 **DataSource** 命令中的 **DataSourceView** 或 **Process** 的规范是可选的。 如果指定 **DataSource** 或 **DataSourceView** ，则将不对它们进行实例化，并且在 **Process** 命令完成后，不会保留它们。  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>外部绑定类型的定义  
 在外部 **Bindings** 集合内，ASSL 允许将绑定集合用于多个对象，每个对象对应一个 **Binding**。 每个 **Binding** 都有一个扩展的对象引用，该引用与对象引用类似，但它还可以引用次级对象（例如，维度属性和度量值组属性）。 此对象的形式平面的典型**对象**中的元素**过程**命令，除非\<*对象*> \< */对象*> 标记不存在。  
  
 绑定指定为其每个对象由 XML 元素的窗体\<*对象*> ID (例如， **DimensionID**)。 确定该对象后尽可能具体处理该窗体\<*对象*> ID，则标识为其所指定的绑定，这通常是此元素**源**. 有一个常见情况需要注意，即 **Source** 为 **DataItem**的属性，这属于属性中的列绑定。 在这种情况下，您不需要指定 **DataItem** 标记，而只需要简单地指定 **Source** 属性，就如同该属性直接位于要绑定的列上一样。  
  
 **KeyColumns** 由它们在 **KeyColumns** 集合内的顺序标识。 无法只指定属性的第一个键列和第三个键列，因为没有办法指示跳过第二个键列。 所有键列都必须存在于维度属性的外部绑定中。  
  
 虽然**Translations**没有 ID，但仍可以通过其语言对其进行语义标识。 因此， **Translations** 内的 **Binding** 需要包含其语言标识符。  
  
 **Binding** 内允许使用的另一个元素为 **ParentColumnID**，它不直接存在于 DDL 中，可用于嵌套表的数据挖掘。 在这种情况下，需要标识要为其提供绑定的嵌套表中的父列。  
  
  
