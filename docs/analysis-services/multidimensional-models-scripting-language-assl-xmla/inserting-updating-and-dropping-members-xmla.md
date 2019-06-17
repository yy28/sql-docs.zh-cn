---
title: 插入、 更新和删除成员 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a409e21e925b3912aee5ec751747f61bce05276
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138579"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>插入、更新和删除成员 (XMLA)
  可以使用[插入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)，[更新](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)，并[删除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)命令在 XML for Analysis (XMLA) 分别插入、 更新或删除从启用写操作的维度的成员。 有关启用写操作的维度的详细信息，请参阅[Write-Enabled 维度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="inserting-new-members"></a>插入新成员  
 **插入**命令将新成员插入启用写操作的维度中的指定属性。  
  
 之前构造**插入**命令，您应提供要插入的新成员的以下信息：  
  
-   要在其中插入新成员的维度。  
  
-   要在其中插入新成员的维度特性。  
  
-   新成员的名称，包括该名称的所有适用翻译。  
  
-   新成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
-   不作为该维度内的其他特性实现的所有适用特性属性的值。 此类特性属性包括一元运算符、翻译、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
 **插入**命令具有只有两个属性：  
  
-   [对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性，其中包含成员的维度中要插入的对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   [特性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla)属性，其中包含一个或多个[属性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla)元素用于标识是用来插入成员的特性。 每个**特性**元素标识一个特性并提供名称、 值、 翻译、 一元运算符、 自定义汇总、 自定义汇总属性，跳过要添加到已标识特性的单个成员的级别。  
  
    > [!NOTE]  
    >  所有属性**特性**元素必须包含。 否则，可能会出错。  
  
## <a name="updating-existing-members"></a>更新现有成员  
 **更新**命令更新指定的特性，基于与启用写操作的维度中的其他属性中的其他成员之间的关系中的现有成员。 **更新**命令可以移动成员复制到层次结构中其他级别所包含的维度，并可用于重新构造的父子层次结构由父属性定义。  
  
 之前构造**更新**命令，您应提供要更新的成员的以下信息：  
  
-   要在其中更新现有成员的维度。  
  
-   要在其中更新现有成员的维度特性。  
  
-   现有成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
-   不作为该维度内的其他特性实现的所有适用特性属性的值。 此类特性属性包括一元运算符、翻译、自定义汇总、自定义汇总属性以及已跳过的级别。  
  
 **更新**命令具有只有三个必需的属性：  
  
-   **对象**属性，其中包含成员的维度中要更新的对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   **特性**属性，其中包含一个或多个**属性**元素用于标识是用来更新成员的特性。 **特性**元素标识一个特性并提供名称、 值、 翻译、 一元运算符、 自定义汇总、 自定义汇总属性，并为经过更新以标识特性的单个成员跳过级别。  
  
    > [!NOTE]  
    >  所有属性**特性**元素必须包含。 否则，可能会出错。  
  
-   [其中](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla)属性，其中包含一个或多个**属性**约束是用来更新成员的特性的元素。 **其中**属性，请务必限制**更新**命令到成员的特定实例。 如果**其中**属性未指定，则更新给定成员的所有实例。 例如，有三个客户，您希望将他们的市县名称从 Redmond 更改为 Bellevue。 若要更改市县名称，必须提供**其中**属性，用于标识客户中的三个成员属性的更改市县属性中的成员。 如果不提供此**其中**属性，其市县名称当前为 Redmond 的每位客户将具有后贝尔维尤市/县名称**更新**命令将运行。  
  
    > [!NOTE]  
    >  除了新成员以外**更新**命令只能更新属性中未包括的特性键值**其中**子句。 例如，更新客户时不能更新市县名称；否则，会更改所有客户的市县名称。  
  
### <a name="updating-members-in-parent-attributes"></a>更新父特性中的成员  
 为了支持父特性**更新**命令具有可选[MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)属性。 设置**MoveWithDescendants**属性设为 true 指示该父成员的标识符发生更改时后，还应父成员的后代与父成员中移动。 如果将此值设置为 False，则移动某父成员将导致该父成员的直接后代提升到该父成员先前所处的级别。  
  
 更新父属性中的成员时**更新**命令无法更新其他特性中的成员。  
  
## <a name="dropping-existing-members"></a>删除现有成员  
 之前构造**Drop**命令，您应提供要删除的成员的以下信息：  
  
-   要在其中删除现有成员的维度。  
  
-   要在其中删除现有成员的维度特性。  
  
-   要删除的现有成员的键。 如果某特性使用一个组合键，则该键可能需要多个值。  
  
 **Drop**命令具有只有两个必需的属性：  
  
-   **对象**属性，其中包含成员的维度中的要删除的对象引用。 该对象引用包含维度的数据库标识符、多维数据集标识符和维度标识符。  
  
-   **其中**属性，其中包含一个或多个**属性**要约束是用要删除成员的特性的元素。 **其中**属性，请务必限制**Drop**命令到成员的特定实例。 如果**其中**命令未指定，则给定成员的所有实例将被都删除。 例如，您希望从 Redmond 中删除三个客户。 若要删除这些客户，你必须提供**其中**属性用于标识要删除 Customer 特性中的三个成员并且是要删除的三个客户的 City 特性的 Redmond 成员。 如果**其中**属性仅指定 City 特性的 Redmond 成员，将删除与 Redmond 关联的每位客户**Drop**命令。 如果**其中**属性仅指定 Customer 特性中的三个成员，将完全由删除三个客户**Drop**命令。  
  
    > [!NOTE]  
    >  **特性**元素中包含**Drop**命令必须仅包含**AttributeName**并**密钥**属性。 否则，可能会出错。  
  
### <a name="dropping-members-in-parent-attributes"></a>删除父特性中的成员  
 设置[DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla)属性指示父成员的后代也应删除与父成员。 如果将此值设置为 False，则父成员的直接后代将提升到该父成员先前所处的级别。  
  
> [!IMPORTANT]  
>  用户只需删除父成员的权限，即可删除父成员及其后代。 用户无需删除后代的权限。  
  
## <a name="see-also"></a>请参阅  
 [Drop 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [插入元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Update 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [定义和标识对象&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
