---
title: CSDLBI 概念 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7bf73822e8872397499bdfbc04bab6747035fbec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62757950"
---
# <a name="csdlbi-concepts"></a>CSDLBI 概念
  带 BI 注释的概念性架构定义语言 (CSDLBI) 基于实体数据框架。实体数据框架是一个抽象概念，用于以某种方式表示不同类型的数据，以便能够以编程方式访问、查询或导出不同的数据集。 CSDLBI 用于表示使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建的数据模型，因为它支持丰富的数据驱动的报告和应用程序。  
  
 这部分说明 CSDLBI 表示形式如何映射到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据模型（表格和多维）以及每种模型类型的示例。  
  
 用于说明这些概念的示例取自 Codeplex 上提供的 AdventureWorks 示例数据库。 有关示例的详细信息，请参阅[SQL Server 的艾德作品示例](https://go.microsoft.com/fwlink/?linkID=220093)。  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>CSDLBI 中表格模型的结构  
 描述报表模型及其数据的 CSDLBI 文档以 xsd 语句开头，后跟模型的定义。  
  
 模型是一个命名空间，其中包含以下主要实体、关联和属性：  
  
-   
  `EntityContainer` 列出了模型中的表。  
  
-   每个表将与 `EntityContainer` 一起作为 `EntitySet` 列出。  
  
-   两个表之间的每个关系均被描述为一个 `AssociationSet`，用于定义关系端点和关系角色。  
  
-   
  `EntityType` 元素针对 BISM 进行了扩展，以提供有关 BISM 中的表和列的其他详细信息，包括用于排序和显示的属性。  
  
-   
  `Measure` 元素定义了可在模型中使用的计算。 可通过使用新的 `KPI` 元素添加一组特殊显示属性来将度量值转换为 KPI。  
  
-   没有针对透视的单独表示形式。 虽然透视中未包含的列和表将用 CSDL 表示，但会由 `Hidden` 属性进行标记。  
  
### <a name="entities-entitysets-and-entitytypes"></a>实体、EntitySet 和 EntityType  
 已对实体数据框架中的实体概念进行扩展，以便表示数据模型中的列和表。 以下摘录显示了仅包含三个表的简单模型中的 `EntitySet` 元素的列表。  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 
  `EntitySet` 不包含表中的列或数据的相关信息。 EntityType 元素中提供了列及其属性的详细说明。  
  
 每个实体（表）的 `EntitySet` 元素包括一个属性集合，这些属性定义键列、列的数据类型和长度、为 null 性、排序行为等。 例如，以下 CSDL 摘录描述了 Customer 表中的三列。 第一列是模型在内部使用的特殊隐藏列。  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 为了限制生成的 CSDLBI 文档的大小，在实体中出现多次的属性将由对某个现有属性的引用指定，这样，只需为 `EntityType` 列出该属性一次。 客户端应用程序可通过查找与 `EntityType` 匹配的 `OriginEntityType` 来获取属性的值。  
  
### <a name="relationships"></a>关系  
 在 Entity Data Framework 中，关系定义为实体之间的*关联*。  
  
 关联始终有两个端点，每个端点指向表中的一个字段或一个列。 因此，两个表之间可以存在多个关系，前提是这些关系具有不同的端点。 将为关联的端点分配角色名称，并指示如何在数据模型的上下文中使用关联。 当应用于与 Orders 表中的客户 ID 相关的客户 ID 时，角色名称的一个示例可能是**ShipTo**的。  
  
 模型的 CSDLBI 表示形式还包含关联上的属性，这些属性确定实体如何根据关联的*重数相互*映射。 多重性指示位于表之间的关系的端点上的属性或列是位于关系的一方还是多方。 没有针对一对一关系的单独的值。 CSDLBI 注释支持多重性为 0（表示实体未与任何对象关联）或为 0..1（表示一对一关系或一对多关系）。  
  
 以下示例表示 Date 表和 ProductInventory 表之间的关系的 CSDLBI 输出，其中这两个表通过 DateAlternateKey 列联接。 请注意，默认情况下，`AssociationSet` 的名称是关系中涉及的列的完全限定名称。 但是，可以在设计模型时将此行为更改为使用其他命名格式。  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>可视化和导航属性  
 用于定义报告层中的表示形式和导航实体之间的关系的属性是 CSDLBI 注释的一个重要部分。 通常，基于客户端应用程序将指定排序和表示形式的其他详细信息这种假设，在创建数据模型时，您会认为控制数据的排序和分组方式或可能的默认值并不重要。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型设计为可以与 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表客户端集成，并在报表设计图面中包含支持数据模型中的实体的表示形式的属性和特性。  
  
 针对可视化的扩展包括用于以下用途的属性：指定要用于数值数据的默认聚合、指示指向图像的 URL 的文本字段或指定用于为当前字段进行排序的字段。  
  
### <a name="name-properties-and-naming-conventions"></a>名称属性和命名约定  
 CSDLBI 架构规定每个实体具有一个唯一名称和一个可用作密钥的标识符。 此外，某些实体可具有用于显示的标题和随实体的使用位置的不同而不同的上下文名称。  
  
 
  `Documentation` 元素使报表设计人员能够提供实体的说明并帮助业务用户了解数据的含义。 某些实体还允许一个或多个 `Annotation` 属性，这些属性提供可由应用程序或客户端使用的额外元数据。  
  
 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工具生成模型时，为对象创建的名称应遵循对象命名的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 约定和名称唯一性。 但是，由于 CSDLBI 基于实体数据框架 (EDF)，而实体数据框架要求名称遵循 C# 标识符的约定，因此，服务器在为模型创建 CSDLBI 输出时将采用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 架构中使用的名称，并将自动创建符合 EDF 要求的新对象名称。 下表描述了用于生成新名称的操作。  
  
|规则|操作|  
|----------|------------|  
|无禁止字符|禁止字符将由下划线替换。|  
|名称必须是唯一的|如果两个字符串相同，则通过为一个字符串追加下划线和数字使其具有唯一性|  
  
> [!WARNING]  
>  标题和限定符都有对应的译文，而对于某种给定语言，可能只存在二者之一。 这意味着，当限定符与名称或限定符与标题串联时，字符串可用两种不同的语言表示。  
  
## <a name="additions-to-support-multidimensional-models"></a>所增加的用于支持多维模型的内容  
 CSDLBI 注释 1.0 版仅支持表格模型。 在版本 1.1 中，添加了对使用传统 BI 开发工具创建的多维模型（OLAP 多维数据集）的支持。 因此，您现在可以向多维模型发出 XML 请求并接收模型的 CSDLBI 定义，以用于报告。  
  
 **多维数据集：** SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]表格数据库只能包含一种模式。 相比较而言，每个多维数据库可以包含多个多维数据集，每个数据库与一个默认的多维数据集关联。 因此，当针对多维服务器发出 XML 请求时，需要指定多维数据集；否则，将返回默认多维数据集的 XML。  
  
 多维数据集的表示形式与表格模型数据库的表示形式非常相似。 多维数据集名称和多维数据集分别对应于表格数据库名称和数据库标识符。  
  
 **维度：** 维度在 CSDLBI 中表示为具有列和属性的实体（表）。 请注意，即使未包括在透视中，模型中包括的维度也将表示为 CSDL 输出（标记为 `Hidden`）。  
  
 **透视：** 客户端可以请求单个透视图的 CSDL。 有关详细信息，请参阅[DISCOVER_CSDL_METADATA 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset)。  
  
 **层次结构：** 层次结构支持并在 CSDLBI 中表示为一组级别。  
  
 **成员：** 已添加对默认成员的支持，并且默认值自动添加到 CSDLBI 输出。  
  
 **计算成员：** 多维模型支持具有单个真实成员的**所有**子级的计算成员。  
  
 **维度属性：** 在 CSDLBI 输出中，支持维度属性，并自动将其标记为不可聚合。  
  
 **Kpi：** CSDLBI 版本1.1 中支持 Kpi，但表示形式已更改。 以前，KPI 是度量值的属性。 在版本1.1 中，可以将 KPI 元素添加到度量值  
  
 **新属性：** 添加了其他属性以支持 DirectQuery 模型。  
  
 **限制：** 不支持单元安全性。  
  
## <a name="see-also"></a>另请参阅  
 [用于商业智能的 CSDL 批注 &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
  
