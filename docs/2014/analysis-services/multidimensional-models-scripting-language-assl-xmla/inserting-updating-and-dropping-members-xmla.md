---
title: 插入、 更新和删除成员 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98da3e0f7a9b61b178372d9b24b8b595ab6b6626
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155483"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>插入、更新和删除成员 (XMLA)
  可以使用[插入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)，[更新](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)，并[删除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)命令在 XML for Analysis (XMLA) 分别插入、 更新或删除从启用写操作的维度的成员。 有关启用写操作的维度的详细信息，请参阅[Write-Enabled 维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="inserting-new-members"></a>插入新成员  
 `Insert` 命令可将新成员插入启用写操作的维度的指定特性中。  
  
 构造 `Insert` 命令之前，应提供要插入的新成员的以下信息：  
  
-   要在其中插入新成员的维度。  
  
-   要在其中插入新成员的维度特性。  
  
-   新成员的名称，包括该名称的所有适用翻译。  
  
-   新成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
-   不作为该维度内的其他特性实现的所有适用特性属性的值。 此类特性属性包括一元运算符、翻译、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
 `Insert` 命令仅具有两个属性：  
  
-   [对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性，其中包含成员的维度中要插入的对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   [特性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla)属性，其中包含一个或多个[属性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla)元素用于标识是用来插入成员的特性。 每个 `Attribute` 元素都标识一个特性，并为要添加到已标识特性的单个成员提供名称、值、翻译、一元运算符、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
    > [!NOTE]  
    >  必须包括 `Attribute` 元素的所有属性。 否则，可能会出错。  
  
## <a name="updating-existing-members"></a>更新现有成员  
 `Update` 命令可在已启用写操作的维度中根据指定特性中现有成员与其他特性中其他成员的关系更新现有成员。 `Update` 命令可将成员移到维度所包含层次结构中的其他级别，并可用于重新组织父特性所定义的父子层次结构。  
  
 构造 `Update` 命令之前，应提供要更新的成员的以下信息：  
  
-   要在其中更新现有成员的维度。  
  
-   要在其中更新现有成员的维度特性。  
  
-   现有成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
-   不作为该维度内的其他特性实现的所有适用特性属性的值。 此类特性属性包括一元运算符、翻译、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
 `Update` 命令仅具有三个必需属性：  
  
-   `Object` 属性，它包含对要在其中更新成员的维度的对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   `Attributes` 属性，它包含用于标识要在其中更新成员的特性的一个或多个 `Attribute` 元素。 `Attribute` 元素可标识一个特性，并为已标识特性中更新的单个成员提供名称、值、翻译、一元运算符、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
    > [!NOTE]  
    >  必须包括 `Attribute` 元素的所有属性。 否则，可能会出错。  
  
-   [其中](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla)属性，其中包含一个或多个`Attribute`约束是用来更新成员的特性的元素。 `Where`属性，请务必限制`Update`命令到成员的特定实例。 如果`Where`属性未指定，则更新给定成员的所有实例。 例如，有三个客户，您希望将他们的市县名称从 Redmond 更改为 Bellevue。 若要更改市县名称，您必须提供 `Where` 属性，该属性将标识 Customer 特性的三个成员中应更改其 City 特性的成员。 如果您不提供此 `Where` 属性，则运行 `Update` 命令后，其市县名称当前为 Redmond 的每个客户的市县名称都将更改为 Bellevue。  
  
    > [!NOTE]  
    >  除了新成员以外，`Update` 命令只能更新 `Where` 子句中未包括的特性的特性键值。 例如，更新客户时不能更新市县名称；否则，会更改所有客户的市县名称。  
  
### <a name="updating-members-in-parent-attributes"></a>更新父特性中的成员  
 为了支持父特性`Update`命令具有可选[MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)属性。 如果将 `MoveWithDescendants` 属性设置为 True，则表示当父成员的标识符发生更改时，该父成员的后代也应与该父成员一起移动。 如果将此值设置为 False，则移动某父成员将导致该父成员的直接后代提升到该父成员先前所处的级别。  
  
 更新父特性中的成员时，`Update` 命令无法更新其他特性中的成员。  
  
## <a name="dropping-existing-members"></a>删除现有成员  
 构造 `Drop` 命令之前，应该提供要删除的成员的以下信息：  
  
-   要在其中删除现有成员的维度。  
  
-   要在其中删除现有成员的维度特性。  
  
-   要删除的现有成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
 `Drop` 命令仅具有两个必需属性：  
  
-   `Object` 属性，它包含对要在其中删除成员的维度的对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   `Where` 属性，它包含用于约束要在其中删除成员的特性的一个或多个 `Attribute` 元素。 `Where` 属性对于将 `Drop` 命令限制于某成员的特定实例来说至关重要。 如果不指定 `Where` 命令，则将删除给定成员的所有实例。 例如，您希望从 Redmond 中删除三个客户。 若要删除这三个客户，您必须提供 `Where` 属性，该属性将标识 Customer 特性中要删除的三个成员，以及要在其中删除三个客户的 City 特性的 Redmond 成员。 如果 `Where` 属性仅指定 City 特性的 Redmond 成员，则 `Drop` 命令将删除与 Redmond 关联的每个客户。 如果 `Where` 属性仅指定 Customer 特性中的三个成员，则 `Drop` 命令会将这三个客户全部删除。  
  
    > [!NOTE]  
    >  `Attribute` 命令中包含的 `Drop` 元素必须仅包含 `AttributeName` 和 `Keys` 属性。 否则，可能会出错。  
  
### <a name="dropping-members-in-parent-attributes"></a>删除父特性中的成员  
 设置[DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla)属性指示父成员的后代也应删除与父成员。 如果将此值设置为 False，则父成员的直接后代将提升到该父成员先前所处的级别。  
  
> [!IMPORTANT]  
>  用户只需删除父成员的权限，即可删除父成员及其后代。 用户无需删除后代的权限。  
  
## <a name="see-also"></a>请参阅  
 [Drop 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [插入元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Update 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [定义和标识对象&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
