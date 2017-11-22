---
title: "CSDLBI 概念 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 16688e8f3f87e8ca9e2e95e4d2200a3a1bf03342
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="csdlbi-concepts"></a>CSDLBI 概念

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  带 BI 注释的概念性架构定义语言 (CSDLBI) 基于实体数据框架。实体数据框架是一个抽象概念，用于以某种方式表示不同类型的数据，以便能够以编程方式访问、查询或导出不同的数据集。 CSDLBI 用于表示使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建的数据模型，因为它支持丰富的数据驱动的报告和应用程序。  
  
 这部分说明 CSDLBI 表示形式如何映射到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据模型（表格和多维）以及每种模型类型的示例。  
  
 用于说明这些概念的示例取自 Codeplex 上提供的 AdventureWorks 示例数据库。 有关这些示例的详细信息，请参阅[for SQL Server 的 Adventure Works 示例](http://go.microsoft.com/fwlink/?linkID=220093)。  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>CSDLBI 中表格模型的结构  
 描述报表模型及其数据的 CSDLBI 文档以 xsd 语句开头，后跟模型的定义。  
  
 模型是一个命名空间，其中包含以下主要实体、关联和属性：  
  
-   **EntityContainer**列出模型中的表。  
  
-   每个表列出与**EntityContainer**作为**EntitySet**。  
  
-   两个表之间的每个关系描述为**AssociationSet**关系终结点和关系角色定义。  
  
-   **EntityType**元素进行扩展，以 BISM 以提供更多详细信息表和在其中包括属性进行排序的列，并显示目的。  
  
-   **度量值**元素定义模型中可以使用的计算结果。 度量值可以通过添加特殊的显示属性，使用新的一组转换为 KPI **KPI**元素。  
  
-   没有针对透视的单独表示形式。 列和透视中不包含的表都位于但标志，则为 CSDL **Hidden**属性。  
  
### <a name="entities-entitysets-and-entitytypes"></a>实体、EntitySet 和 EntityType  
 已对实体数据框架中的实体概念进行扩展，以便表示数据模型中的列和表。 以下摘录内容中显示的列表**EntitySet**中一个简单元素模型包含只有三个表。  
  
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
  
 **EntitySet**不包含有关列或表中的数据的信息。 EntityType 元素中提供了列及其属性的详细说明。  
  
 **EntitySet**为每个实体 （表） 的元素包括的定义的键列、 数据类型和长度的列，可为 null，排序行为，等的属性集合。 例如，以下 CSDL 摘录描述了 Customer 表中的三列。 第一列是模型在内部使用的特殊隐藏列。  
  
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
  
 若要限制 CSDLBI 文档生成的大小，实体中出现一次以上的属性指定对现有属性的引用，以便为需要一次列出的属性**EntityType**。 客户端应用程序可以获取属性的值，通过查找**EntityType**匹配**OriginEntityType**。  
  
### <a name="relationships"></a>关系  
 在实体数据框架中，关系定义为*关联*实体之间。  
  
 关联始终有两个端点，每个端点指向表中的一个字段或一个列。 因此，两个表之间可以存在多个关系，前提是这些关系具有不同的端点。 将为关联的端点分配角色名称，并指示如何在数据模型的上下文中使用关联。 角色名称的一个示例可能是**ShipTo**，当应用于客户 ID 相关的 Orders 表中的客户 id。  
  
 CSDLBI 模型表示形式还包含对关联来确定如何将实体映射到每个方面的其他特性*多重性*的关联。 多重性指示位于表之间的关系的端点上的属性或列是位于关系的一方还是多方。 没有针对一对一关系的单独的值。 CSDLBI 注释支持多重性为 0（表示实体未与任何对象关联）或为 0..1（表示一对一关系或一对多关系）。  
  
 以下示例表示 Date 表和 ProductInventory 表之间的关系的 CSDLBI 输出，其中这两个表通过 DateAlternateKey 列联接。 请注意，默认情况下，名称**AssociationSet**是关系中涉及的列的完全限定的名称。 但是，可以在设计模型时将此行为更改为使用其他命名格式。  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>可视化效果和导航属性  
 用于定义报告层中的表示形式和导航实体之间的关系的属性是 CSDLBI 注释的一个重要部分。 通常，基于客户端应用程序将指定排序和表示形式的其他详细信息这种假设，在创建数据模型时，您会认为控制数据的排序和分组方式或可能的默认值并不重要。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型设计为可以与 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表客户端集成，并在报表设计图面中包含支持数据模型中的实体的表示形式的属性和特性。  
  
 针对可视化的扩展包括用于以下用途的属性：指定要用于数值数据的默认聚合、指示指向图像的 URL 的文本字段或指定用于为当前字段进行排序的字段。  
  
### <a name="name-properties-and-naming-conventions"></a>名称属性和命名约定  
 CSDLBI 架构规定每个实体具有一个唯一名称和一个可用作密钥的标识符。 此外，某些实体可具有用于显示的标题和随实体的使用位置的不同而不同的上下文名称。  
  
 **文档**元素提供报表设计器，用于完善的实体的说明来帮助了解数据的含义的业务用户的可能性。 某些实体还允许一个或多个**批注**特性，通过应用程序或客户端使用提供额外的元数据。  
  
 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工具生成模型时，为对象创建的名称应遵循对象命名的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 约定和名称唯一性。 但是，由于 CSDLBI 基于实体数据框架 (EDF)，而实体数据框架要求名称遵循 C# 标识符的约定，因此，服务器在为模型创建 CSDLBI 输出时将采用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 架构中使用的名称，并将自动创建符合 EDF 要求的新对象名称。 下表描述了用于生成新名称的操作。  
  
|规则|操作|  
|----------|------------|  
|无禁止字符|禁止字符将由下划线替换。|  
|名称必须是唯一的|如果两个字符串相同，则通过为一个字符串追加下划线和数字使其具有唯一性|  
  
> [!WARNING]  
>  标题和限定符都有对应的译文，而对于某种给定语言，可能只存在二者之一。 这意味着，当限定符与名称或限定符与标题串联时，字符串可用两种不同的语言表示。  
  
## <a name="additions-to-support-multidimensional-models"></a>所增加的用于支持多维模型的内容  
 CSDLBI 注释 1.0 版仅支持表格模型。 在版本 1.1 中，添加了对使用传统 BI 开发工具创建的多维模型（OLAP 多维数据集）的支持。 因此，您现在可以向多维模型发出 XML 请求并接收模型的 CSDLBI 定义，以用于报告。  
  
 **多维数据集：** SQL Server[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]表格数据库可以包含只有一种模式。 相比较而言，每个多维数据库可以包含多个多维数据集，每个数据库与一个默认的多维数据集关联。 因此，当针对多维服务器发出 XML 请求时，需要指定多维数据集；否则，将返回默认多维数据集的 XML。  
  
 多维数据集的表示形式与表格模型数据库的表示形式非常相似。 多维数据集名称和多维数据集分别对应于表格数据库名称和数据库标识符。  
  
 **维度：**维度 CSDLBI 中表示为具有列和属性的实体 （表）。 请注意，即使未包括在透视，模型中包含的维度将表示在 CSDL 输出中，标记为**Hidden**。  
  
 **透视：**客户端可以为单个透视请求 CSDL。 有关详细信息，请参阅[DISCOVER_CSDL_METADATA 行集](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)。  
  
 **层次结构：**层次结构支持的和在 CSDLBI 中表示为一组级别。  
  
 **成员：**对支持已添加的默认成员，默认值会自动添加到 CSDLBI 输出。  
  
 **计算成员：**多维模型支持计算的成员的子级**所有**与单个真实成员。  
  
 **维度属性：**中 CSDLBI 输出，支持的和自动标记为不可聚合维度属性。  
  
 **Kpi:** Kpi CSDLBI 1.1 版中，在受支持，但表示已更改。 以前，KPI 是度量值的属性。 在 1.1 版中，KPI 元素可以添加到度量值  
  
 **新属性：**添加了其他属性，以支持 DirectQuery 模型。  
  
 **限制：**单元安全性不支持。  
  
## <a name="see-also"></a>另请参阅  
 [用于商业智能的 CSDL 批注 (CSDLBI)](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
